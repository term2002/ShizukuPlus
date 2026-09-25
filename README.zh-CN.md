<div align="center">

# Shizuku+

面向 Android 的进阶特权进程管理器。

[English](README.md) | **简体中文**

它是 [Shizuku](https://github.com/RikkaApps/Shizuku) 的增强版本，基于 [thedjchi/Shizuku](https://github.com/thedjchi/Shizuku) 构建，带来了易用性改进、向下移植的优化以及独占的 Plus API。

Shizuku 让普通应用可以通过由 adb 或 root 启动的特权进程直接使用系统级 API。Shizuku+ 在保持完全兼容的同时，为高级用户和开发者增加了更多功能。

[![Stars](https://img.shields.io/github/stars/thejaustin/ShizukuPlus?style=for-the-badge&color=bfb330&labelColor=807820)](https://github.com/thejaustin/ShizukuPlus/stargazers)
[![Downloads](https://img.shields.io/github/downloads/thejaustin/ShizukuPlus/total?style=for-the-badge&color=bf7830&labelColor=805020)](https://github.com/thejaustin/ShizukuPlus/releases)
[![Latest Release](https://img.shields.io/github/v/release/thejaustin/ShizukuPlus?style=for-the-badge&color=3060bf&labelColor=204080&label=Latest)](https://github.com/thejaustin/ShizukuPlus/releases/latest)

</div>

> **欢迎贡献者！** 如果你发现了缺陷，或希望改进代码库，请提交 issue 或 pull request —— 本项目正在积极寻找贡献者与协作者。

## ⬇️ 下载

请从 [GitHub Releases](https://github.com/thejaustin/ShizukuPlus/releases) 获取最新版本，最新变更请查阅那里的版本说明。

## ✨ Shizuku+ 核心功能

*   **统一特权提供者**：为 **Root**、**ADB Shell** 和 **Dhizuku（设备所有者）** 提供统一接口。
*   **OneUI 8+ 主题修复**：让 Hex Installer、Substratum 等主题引擎在 Android 16/17 和 OneUI 8+ 上继续可用。
*   **Dhizuku 模式**：将系统设备所有者的 Binder 共享给任何已获 Shizuku 权限的应用——通过 ADB 设置，无需 root。
*   **可定制手势**：左滑、右滑和长按操作，可按应用分别配置。
*   **应用内更新日志**：无需离开应用即可查看更新内容。
*   **批量管理**：多选应用，一键授予/撤销权限或将其隐藏。
*   **活动日志**：API 调用与 `su` 桥接命令的审计记录，带应用图标并实时更新。
*   **Root 兼容性中心**：面向旧式 root 应用的控制面板，支持细粒度模块控制（Magisk 模拟、自动授权、文件拦截器等）。
*   **通用 SU 自动化**：一键“一键配置”，让所有已安装的 root 应用都指向 Shizuku+ SU 桥接。
*   **服务诊断**：诊断并修复服务启动问题（已涵盖三星自动拦截器）。
*   **集成功能指南**：每个 Plus 功能都配有信息图标，用通俗语言说明其作用。
*   **快捷设置磁贴**：可在通知面板中查看并切换服务状态。

## 🚀 Plus API 功能

Shizuku+ 为高级自动化与工具提供独占的系统接口——这些在原版 Shizuku 中均不存在：

*   **AICore+ 自动化桥接**：面向 AI 驱动工具的特权 UI 自动化（层级转储、点按/滑动）——无需 root。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/e9bd1187)）
*   **AVF（虚拟机）管理器**：运行带 GPU 加速的隔离 Linux/Microdroid 虚拟机。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/c8e962f6)）
*   **特权存储代理**：为备份与文件管理提供对受限路径的鉴权访问。`/data/app/` 和外部 `/Android/data/` 在 ADB 模式下即可工作；`/data/data/` 需要 root（服务端必须以 UID 0 运行才能跨越应用私有目录边界）。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/c8e962f6)）
*   **设备模拟**（设置中的*模拟设备身份*）：呈现不同的设备身份，以绕过针对特定机型的限制。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/11867f44)）
*   **智能桥接**（*AI Core Plus*）：特权 NPU 调度与屏幕上下文智能。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/e9bd1187)）
*   **窗口管理器 Plus**：强制自由窗口缩放、管理气泡栏，以及更稳健的悬浮层。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/e9bd1187)）
*   **系统主题桥接**（*Overlay Manager Plus*）：面向免 root 主题化的特权叠加层管理（例如 Hex Installer）。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/55f6b7c7)）
*   **网络与 DNS 管理**：为免 root 广告拦截管理私人 DNS 与防火墙路由。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/55f6b7c7)）
*   **深度进程控制**（*Activity Manager Plus*）：让进程管理类应用能更激进地结束应用并设置待机分组。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/55f6b7c7)）
*   **连续性桥接**：在 Shizuku+ 设备之间安全地移交状态与任务。（[已加入](https://github.com/thejaustin/ShizukuPlus/commit/20cf14f7)）

## 🛠️ 向下移植与优化

Shizuku+ 让常规 Shizuku 应用无需任何代码改动即可更快、更兼容：

*   **透明 Shell 拦截器**：将常见的 `pm`、`am` 和 `settings` 命令改走更快的原生 API。
*   **本地 ADB 代理**：在端口 15555 上模拟一个 ADB 服务，让旧式应用无需保持无线 ADB 常开即可使用 Shizuku。
*   **SU 桥接**：为支持自定义 root 路径的未 root 应用提供由 Shizuku 支撑的 `su` 替代品。在 shell UID 允许的范围内，常见 root 命令会被转换为真实的框架操作——`iptables --uid-owner` 的按应用阻断会变成实时的 `NetworkPolicy` 限制，`resetprop` 会读写真实的系统属性，`chmod`/`chown` 会真正生效——只有当某项操作确实需要 root 时（例如刷写分区或加载内核模块）才回退为模拟成功。
*   **`plus` CLI 辅助工具**：一个特权命令行工具，可在 `rish` 中使用。
*   **动态应用数据库**：从 GitHub 保持界面中的应用说明与建议为最新状态。

## ⚙️ 模块化控制

Shizuku+ 中的一切都是可选的。使用设置中的 **Plus 功能**分类来开关：
*   透明 Shell 拦截
*   各项 Plus API（AVF、存储、智能等）
*   主页卡片可见性
*   活动日志记录

## 🔌 第三方应用兼容性

Shizuku+ 以独立包名 (`af.shizuku.plus.api`) 安装，因此可与原版 Shizuku 共存。由于大多数感知 Shizuku 的应用会专门查找 `moe.shizuku.privileged.api` 包名，Shizuku+ 附带了一个轻量的 **兼容中心（Compat Hub）**——一个极小的配套应用，它注册该包名并将 binder/权限请求转发给 Shizuku+。

**如果第三方应用无法检测到 Shizuku+：**
1. 启动 Shizuku+ 服务（ADB 或 root）。
2. 在主页使用 **兼容中心** 卡片安装配套应用（它已内置于应用中；安装过程经由正在运行的服务完成，因此请先启动服务）。
3. 重新打开第三方应用——它现在应当能检测到 Shizuku 并接收服务 binder。

或者，安装 **drop-in** 构建版本，它会直接注册为 `moe.shizuku.privileged.api`（请勿与原版 Shizuku 一同安装）。

## ☑️ 系统要求

**最低：Android 7+ · 完整支持至 Android 17 (SDK 37)**
- **Root 模式：** 需要已 root 的设备
- **无线调试模式：** Android 11+ 以及所有 Android TV
- **电脑模式：** 所有设备
- **开机自启动：** 仅在无线调试或 Root 模式下可用

在 **Android 16+** 上，Shizuku+ 会请求新的本地网络保护权限，以保证无线调试的发现与配对继续可用；在 **Android 17** 上，它会透明地处理隐藏 API 的 `deviceId` 变更，使已授权应用仍能显示并让权限授予继续生效。

## 📱 开发者指南

关于独占 Plus API 的文档，请参阅 [Shizuku+-API](https://github.com/thejaustin/ShizukuPlus-API) 仓库。

## 🙏 致谢与许可

Shizuku+ 是一个社区驱动的增强项目，fork 自 [thedjchi/Shizuku](https://github.com/thedjchi/Shizuku)，而后者本身又 fork 自原版 [RikkaApps/Shizuku](https://github.com/RikkaApps/Shizuku)。本项目与原 RikkaApps 团队无隶属关系。

感谢以下上游贡献者与项目，是他们的工作让 Shizuku+ 成为可能：

- **[RikkaApps / Rikka](https://github.com/RikkaApps)** —— 奠定了 Shizuku 项目及其优雅的 API 设计。
- **[thedjchi](https://github.com/thedjchi)** —— 提供了中间 fork 与易用性改进，并承担了 **Android 17 (SDK 37) 兼容性**工作，Shizuku+ 的 A17 支持正是由此改编而来。
- **[kerneldroid / Nightzuku](https://github.com/kerneldroid/Nightzuku)** —— Android 17 隐藏 API `deviceId` 兼容方案（即 `Android17Compat` / `InstalledPackagesCompat` 反射层）与本地网络保护处理的源头，本 fork 的 A17 支持由此衍生。
- **[LandonMoran](https://github.com/LandonMoran)** —— 将 Nightzuku 的 Android 17 支持移植到 thedjchi fork，并在**真实的 Android 17 设备上完成端到端验证**（配对、服务启动以及已授权应用列表），为 Shizuku+ 的移植提供了实地验证基础。
- **[Muntashir Akon](https://github.com/MuntashirAkon)** —— 提供 aShell You 代码库，启发了终端与 shell 自动化功能。
- **[iamr0s](https://github.com/iamr0s)** —— 提供 Dhizuku，实现了统一的设备所有者特权模式；以及 AndroidAppProcess，用于独立 Java 进程执行。
- **[pascua28](https://github.com/pascua28)** —— 提供三星系统 UID 1000 提权的原生集成。
- **[kerneldroid](https://github.com/kerneldroid)** —— 提供 Nightzuku fork，启发了我们对 Android 16/17 (SDK 37) 隐藏 API 的韧性处理（应对 `deviceId`）以及界面现代化。
- **[ShizukuExt-SystemUID](https://github.com/ShizukuExt)** —— 提出了超越标准限制的系统性 UID 1000 提权构想。

### 上游项目

| 项目 | 作者 | 许可 | 作用 |
|---------|--------|---------|------|
| [Shizuku](https://github.com/RikkaApps/Shizuku) | RikkaApps / Rikka | Apache 2.0 | 奠定特权进程架构基础 |
| [Shizuku（fork）](https://github.com/thedjchi/Shizuku) | thedjchi | Apache 2.0 | 带易用性改进的中间 fork；承担了 Shizuku+ 所改编的 Android 17 兼容工作 |
| [Nightzuku](https://github.com/kerneldroid/Nightzuku) | kerneldroid | Apache 2.0 | Android 17 隐藏 API `deviceId` + 本地网络保护兼容方案的源头 |
| [Shizuku（fork）](https://github.com/pascua28/Shizuku) | pascua28 | Apache 2.0 | 三星 UID 1000 系统级执行漏洞利用 |
| [Nightzuku](https://github.com/kerneldroid/Nightzuku) | kerneldroid | Apache 2.0 | Android 16/17 API 韧性与界面现代化 |
| [ShizukuExt-SystemUID](https://github.com/ShizukuExt) | ShizukuExt 团队 | Apache 2.0 | 系统 UID 提权构想 |
| [Dhizuku](https://github.com/iamr0s/Dhizuku) | iamr0s | Apache 2.0 | 设备所有者 binder 共享（Dhizuku 模式） |
| [AndroidAppProcess](https://github.com/iamr0s/AndroidAppProcess) | iamr0s | LGPL-3.0 | 独立的高权限 Java 进程封装 |

### 开源库

| 库 | 作者 | 许可 |
|---------|--------|---------|
| [AndroidX Jetpack](https://developer.android.com/jetpack) | Google / AOSP | Apache 2.0 |
| [Material Components](https://github.com/material-components/material-components-android) | Google | Apache 2.0 |
| [Material Symbols](https://fonts.google.com/icons) | Google | Apache 2.0 |
| [Kotlin / Coroutines / Serialization](https://github.com/JetBrains/kotlin) | JetBrains | Apache 2.0 |
| [RikkaX Libraries](https://github.com/RikkaApps)（appcompat、material、insets、html、recyclerview、preference、lifecycle、parcelablelist） | Rikka | Apache 2.0 |
| [Hidden API / Refine](https://github.com/RikkaApps/HiddenApiCompat) | Rikka | Apache 2.0 |
| [Mavericks (MvRx)](https://github.com/airbnb/mavericks) | Airbnb | Apache 2.0 |
| [Lottie](https://github.com/airbnb/lottie-android) | Airbnb | Apache 2.0 |
| [Coil](https://github.com/coil-kt/coil) | Coil 贡献者 | Apache 2.0 |
| [Koin](https://github.com/InsertKoinIO/koin) | Koin 贡献者 | Apache 2.0 |
| [Timber](https://github.com/JakeWharton/timber) | Jake Wharton | Apache 2.0 |
| [libsu](https://github.com/topjohnwu/libsu) | topjohnwu | Apache 2.0 |
| [AndroidHiddenApiBypass](https://github.com/LSPosed/AndroidHiddenApiBypass) | LSPosed | Apache 2.0 |
| [libcxx](https://github.com/lsposed/libcxx) | LSPosed / LLVM | Apache 2.0 + LLVM Exception |
| [AppIconLoader](https://github.com/zhanghai/AppIconLoader) | Zhang Hai | Apache 2.0 |
| [BoringSSL (NDK)](https://github.com/vvb2060/ndk-boringssl) | vvb2060 / Google | Apache 2.0 / ISC |
| [Gson](https://github.com/google/gson) | Google | Apache 2.0 |
| [LeakCanary](https://github.com/square/leakcanary) | Square | Apache 2.0 |
| [AboutLibraries](https://github.com/mikepenz/AboutLibraries) | Mike Penz | Apache 2.0 |
| [Bouncy Castle](https://www.bouncycastle.org/) | Legion of Bouncy Castle | MIT |
| [Sentry Android SDK](https://github.com/getsentry/sentry-java) | Sentry | MIT |
| [SQLite（C 恢复 API / CLI）](https://sqlite.org/) | D. Richard Hipp / SQLite Consortium | Public Domain |

完整许可文本与各库详情：[OPEN_SOURCE_LICENSES.md](OPEN_SOURCE_LICENSES.md) | [NOTICE](NOTICE)

## 📃 许可

[Apache 2.0](LICENSE)

### 贡献者

感谢每一位为 Shizuku+ 贡献代码、翻译与测试的人：

**代码贡献者**

| 贡献者 | 贡献内容 |
|-------------|--------------|
| [thejaustin](https://github.com/thejaustin) | 项目发起人与主要维护者——所有核心 Plus 功能、界面/体验与基础设施 |
| [thedjchi](https://github.com/thedjchi) | 中间 fork 基础；Android 17 (SDK 37) 兼容性奠基工作 |
| [Kevin Doremy](https://github.com/doremylover) | 无用代码清理、未使用导入清理、布局与类重构 |
| [Ryfter](https://github.com/Ryfter) | mDNS 超时改进、前台服务子类型重构、通知体验 |
| [vvb2060](https://github.com/vvb2060) | AGP 构建系统更新、LTO 优化、许可说明澄清 |
| [Haruue Icymoon](https://github.com/haruue) | 文档与 README 改进 |

**翻译贡献者**

| 语言 | 贡献者 |
|----------|-------------|
| 巴西葡萄牙语 | [odorizzioficial](https://github.com/odorizzioficial) |
| 法语 | [Ryfter](https://github.com/Ryfter)、[T. Clement](https://github.com/thibaultclement) |
| 越南语 | [ThePrimalPea](https://github.com/ThePrimalPea) |
| 菲律宾语 | [IverCoder](https://github.com/IverCoder) |
| 意大利语 | [Dany-coder778](https://github.com/Dany-coder778) |
| 日语 | [MES-mitutti](https://github.com/MES-mitutti) |

*还有更多通过 Weblate 参与社区翻译的贡献者——感谢所有译者！*

### 鸣谢
- 特别感谢 **AkayamiShurui42** 主动开展的安全研究与稳定性补丁（参考：#239）。
- 感谢 **AlexeiCrystal** 定位 MIUI 崩溃缺陷，并为旧式应用提出兼容中心解决方案（#241、#242）。
- 感谢 **ddnexus** 和 **kai-bash** 指出设备所有者恢复出厂设置的陷阱与 Google 备份冲突（#237）。
- 感谢 **Kevinco1** 就 root 兼容应用检测问题提供的反馈（#243）。
- 感谢 **aragortsantiago6-beep**、**Scoop2389**（Pixel 9a）和 **ConversionRituals**（小米）在 Android 16/17 上的真机测试、崩溃报告与日志，推动了 SDK 37 隐藏 API 与本地网络保护兼容性修复（#317、#323）。
- 感谢 **gmm96** 在多个构建版本上进行多轮详尽的 logcat 调试，最终定位了缓存应用冻结器的 binder 投递缺陷（#371）。
- 感谢 **[odorizzioficial](https://github.com/odorizzioficial)** 完成整套巴西葡萄牙语翻译（#409），并就三星“休眠应用”导致看门狗冻结提供了详尽报告（#415）。
