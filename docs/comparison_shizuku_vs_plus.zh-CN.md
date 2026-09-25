# Shizuku 与 Shizuku+ 架构对比

Shizuku+ 是对基础版 Shizuku 项目的全面增强。它在与现有 Shizuku 应用保持 100% 兼容的同时，引入了面向下一代 Android 高级用户工具的现代化模块化架构。

## 1. 核心特权架构

| 特性 | 原版 Shizuku | Shizuku+ |
|---------|------------------|----------|
| **主要后端** | Root / ADB Shell | Root / ADB Shell / **Dhizuku（设备所有者）** |
| **服务进程** | `shizuku_server` | `shizuku_plus_server`（优化后的原生桥接） |
| **Binder 接口** | 标准 IShizuku | 扩展的 IShizukuPlus，带细粒度能力标志 |
| **多用户** | 基础支持 | 稳健的跨用户 binder 共享（例如安全文件夹） |

### 统一后端
原版 Shizuku 主要依赖通过 ADB 启动的 `shizuku_server`，而 Shizuku+ 集成了 **Dhizuku 模式**。这允许 Shizuku+ 管理器自身被设为**设备所有者**，从而为系统特权提供一个持久、免 root 的锚点，可在重启后继续有效（在受支持的配置下）。

### 兼容层（包名检测与 Binder 投递）
Shizuku+ 以自身的应用 ID (`af.shizuku.plus.api`) 安装，因此可与原版 Shizuku 共存；但感知 Shizuku 的应用传统上会查找固定的 `moe.shizuku.privileged.api` 包名。Shizuku+ 通过两个独立的层来解决这一问题：

*   **检测：** 内置的 **兼容中心（Compat Hub）** 配套应用（`compat` 模块，包名 `moe.shizuku.privileged.api`）可满足第三方的 `isInstalled` 检查，并将旧式的 `REQUEST_BINDER` 广播转发给真正的管理器。另一种 **drop-in** 版本则直接以 `moe.shizuku.privileged.api` 安装。
*   **投递：** 服务通过 ContentProvider 的 `sendBinder` 调用将特权 binder 交给每个已授权应用，并携带面向全部三个 API 命名空间（`af.shizuku`、`rikka.shizuku`、`moe.shizuku`）的 `BinderContainer` 数据包。只有兼容中心和该握手都成功，应用才会将 Shizuku+ 视为“正在运行”。

## 2. Plus API 生态

Shizuku+ 不止于简单的 shell 执行，它向 Android 内部系统服务暴露了稳定、版本无关的桥接接口。

### Overlay Manager Plus (OMP)
*   **问题所在：** Android 14+ 和 OneUI 8+ 对标准的 `OverlayManager` 系统服务引入了严格限制，破坏了免 root 主题化。
*   **解决方案：** Shizuku+ 使用专有的 `OverlayManagerTransaction` 桥接，让主题方案（Substratum、Hex Installer）能够在无需完整系统 root 的情况下，安全且持久地应用叠加层。

### AICore+ 自动化桥接
*   **能力：** 提供特权的 `AccessibilityService` 代理。
*   **功能：**
    *   `dumpHierarchy()`：将完整 UI 树导出为 XML（比 `uiautomator` 更快）。
    *   `performTap/Swipe()`：在内核/硬件抽象层模拟物理输入。
*   **应用场景：** 让进阶的 AI 驱动自动化（如 Tasker + GPT）无需 root 即可与任意应用交互。

### Root 兼容性中心（SU 桥接）
Shizuku+ 为旧式应用充当转换层。
*   **SU 包装器：** 提供 `/system/bin/su` 的替代品，将命令路由到 Shizuku binder。
*   **模块模拟：** 可让应用误以为已安装 Magisk 或 BusyBox，从而解锁旧式工具中的进阶功能。

## 3. 性能与稳定性改进

### 透明 Shell 拦截器
原版 Shizuku 应用常会执行 shell 命令（例如 `pm install`）。由于需要 fork 新进程，这些操作很慢。
*   **Shizuku+ 的优化：** 拦截这些调用，并在已有的特权进程内将其路由到直接的 Java/原生 API（如 `IPackageManager`）。
*   **效果：** 对 MacroDroid 或终端模拟器这类重度依赖 shell 的应用，执行速度最高提升 10 倍。

### 服务诊断
实时诊断引擎，可监测各厂商特有的“应用查杀”机制（如三星自动拦截器或 Oppo 电池守卫），并提供一键修复以保持 Shizuku 服务存活。

### 看门狗韧性
三层独立的恢复机制，每一层都覆盖了其他层无法触及的缺口：用于快速恢复的进程内崩溃监听器、以防看门狗服务自身死亡的周期性 WorkManager 兜底，以及基于 `AlarmManager` 的外部重新唤醒机制——即使某个厂商冻结策略（例如三星 One UI 的“休眠应用”）在锁屏时杀死了*整个*应用进程，它仍能重启一切，而这正是进程内任何机制都无法自我察觉的唯一失效场景。详见 [Service Connection 维基页面](https://github.com/thejaustin/ShizukuPlus/wiki/Service-Connection#watchdog)。

## 4. 界面与体验优化
*   **Material 3 表达性设计：** 采用最新的 M3 设计语言，带弹性动画与自适应形状。
*   **应用内更新日志：** 更新后可直接查看版本说明。
*   **批量管理：** 为拥有数百个应用的高级用户提供工业级权限管理。

---
*如需将 Plus API 集成到你自己的应用中，请参阅 [Shizuku+-API](https://github.com/thejaustin/ShizukuPlus-API) 仓库。关于 Shizuku+ 申请的每一项权限及其原因的完整说明，请参阅 [Permissions 维基页面](https://github.com/thejaustin/ShizukuPlus/wiki/Permissions)。*
