# 基础信息

|      |      |
|------|------|
| 名称 | core |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.core |
| 概述说明 | 系统环境检查工具集，覆盖Shell、目录、平台、安全等验证。多模式运行框架支持后台、托盘、GUI模式切换。窗口管理工具提供跨平台样式控制、对话框和布局管理。字体、缓存、国际化、日志等核心功能模块。应用管理包括启动参数、实例控制、主题、版本等功能。 |

# 说明

```markdown
## 概述

该代码模块是一个跨平台的JavaFX应用程序框架，提供从系统环境检查到用户界面管理的完整解决方案。模块采用分层架构设计，主要包含以下核心子系统：

1. **环境预检系统**：包含Shell环境验证、系统目录检查、平台特定问题检测等50+检查项
2. **多模式运行框架**：支持BACKGROUND/TRAY/GUI三种运行模式，带优雅切换和异常恢复
3. **现代化窗口管理**：封装原生API实现跨平台窗口控制，支持Mica/Acrylic等特效
4. **应用基础设施**：包含国际化、缓存管理、字体处理、主题系统等基础服务
5. **生命周期管理**：处理启动参数、实例控制、重启更新等全生命周期操作

模块特点：
- 严格的单例模式管理关键组件
- 全面的跨平台兼容性处理（Windows/macOS/Linux）
- 企业级的错误处理和日志系统
- 响应式设计（主题/字体/布局动态更新）
- 模块化扩展架构（通过AppExtensionManager）

## 主要业务场景

1. **应用启动与初始化**
   - 执行50+项环境检查（`AppShellChecker`等）
   - 加载核心配置（`AppProperties`）
   - 初始化国际化系统（`AppI18n`）
   - 显示首次运行配置（`AppConfigurationDialog`）

2. **多模式运行管理**
   - 根据系统能力自动选择初始模式（`OperationMode`）
   - 处理模式间切换（GUI↔TRAY）
   - 系统托盘集成（`AppTray`/`AppTrayIcon`）
   - 后台服务管理

3. **用户界面呈现**
   - 主窗口生命周期管理（`AppMainWindow`）
   - 跨平台窗口样式控制（`NativeMacOsWindowControl`）
   - 主题系统切换（`AppTheme`）
   - 字体管理系统（`AppFont`/`AppFontSizes`）

4. **系统集成**
   - 文件监视（`AppFileWatcher`）
   - 剪贴板动作处理（`AppActionLinkDetector`）
   - 系统休眠唤醒监听（`AppDesktopIntegration`）
   - Windows关机钩子（`AppWindowsShutdown`）

5. **维护与扩展**
   - 模块热加载（`AppExtensionManager`）
   - 缓存管理（`AppCache`）
   - 错误收集与日志（`AppLogs`）
   - 应用重启更新（`AppRestart`）

6. **特殊流程处理**
   - EULA确认（`AppGreetingsDialog`）
   - 单实例控制（`AppInstance`）
   - 命令行参数解析（`AppArguments`）
   - 布局状态持久化（`AppLayoutModel`）
```


### 包内部结构视图

```mermaid
graph TD
    core --> check
    core --> mode
    core --> window
    core --> AppFont.java
    core --> AppCache.java
    core --> AppFontSizes.java
    core --> AppActionLinkDetector.java
    core --> App.java
    core --> AppLayoutModel.java
    core --> AppI18nData.java
    core --> AppProperties.java
    core --> AppExtensionManager.java
    core --> AppDesktopIntegration.java
    core --> AppPreloader.java
    core --> AppInstance.java
    core --> AppStyle.java
    core --> AppLogs.java
    core --> AppConfigurationDialog.java
    core --> AppTrayIcon.java
    core --> AppArguments.java
    core --> AppTheme.java
    core --> AppVersion.java
    core --> AppWindowsShutdown.java
    core --> AppDistributionType.java
    core --> AppRestart.java
    core --> AppGreetingsDialog.java
    core --> AppFileWatcher.java
    core --> AppDataLock.java
    core --> AppOpenArguments.java
    core --> AppI18n.java
    core --> AppSid.java
    core --> AppTray.java
    check --> AppShellChecker.java
    check --> AppShellCheck.java
    check --> AppTempCheck.java
    check --> PtbDialog.java
    check --> AppTestCommandCheck.java
    check --> AppCertutilCheck.java
    check --> AppJavaOptionsCheck.java
    check --> AppUserDirectoryCheck.java
    check --> AppDebugModeCheck.java
    check --> AppPathCorruptCheck.java
    check --> AppRosettaCheck.java
    check --> AppAvCheck.java
    check --> AppGpuCheck.java
    check --> AppHomebrewCoreutilsCheck.java
    check --> AppSystemFontCheck.java
    mode --> OperationMode.java
    mode --> BaseMode.java
    mode --> PlatformMode.java
    mode --> TrayMode.java
    mode --> GuiMode.java
    window --> NativeMacOsWindowControl.java
    window --> ModifiedStage.java
    window --> NativeWinWindowControl.java
    window --> AppMainWindow.java
    window --> AppDialog.java
    window --> AppWindowBounds.java
    window --> AppWindowHelper.java
```

该流程图展示了xpipe应用核心模块的完整结构，包含check、mode、window三个子目录及35个核心类文件。其中check目录下集中了16种系统检查组件，mode目录包含5种运行模式实现，window目录管理7个窗口控制类，其余为独立的核心功能类如字体管理、缓存控制、国际化等。层级关系清晰展现了模块化设计思想，核心类直接归属于core节点，子模块通过二级节点组织相关功能组件。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [AppFont.java](AppFont.md) | file | 初始化字体加载，包括ikonli和捆绑字体，忽略加载失败。 |
| [App.java](App.md) | file | Java应用类，单例模式，含启动方法和静态获取实例方法。 |
| [AppActionLinkDetector.java](AppActionLinkDetector.md) | file | 检测剪贴板动作并处理，支持焦点和粘贴触发，含确认提示。 |
| [AppFontSizes.java](AppFontSizes.md) | file | Java类AppFontSizes管理字体大小，支持多尺寸和操作系统适配。 |
| [AppCache.java](AppCache.md) | file | AppCache类提供静态方法管理缓存文件，支持清除、读写和查询修改时间。 |
| [AppLogs.java](AppLogs.md) | file | AppLogs类管理日志记录，支持文件和控制台输出，提供日志级别控制和异常处理。 |
| [AppStyle.java](AppStyle.md) | file | 管理样式表、字体和主题的JavaFX工具类。 |
| [AppInstance.java](AppInstance.md) | file | 检查应用实例是否运行，锁定数据目录或连接现有实例，失败则退出。 |
| [AppPreloader.java](AppPreloader.md) | file | AppPreloader类在非Linux系统跳过，Linux下设置JavaFX应用名称并记录事件。 |
| [AppDesktopIntegration.java](AppDesktopIntegration.md) | file | 桌面应用集成类，处理系统休眠唤醒、MacOS偏好设置、URI打开及任务栏图标设置。 |
| [AppExtensionManager.java](AppExtensionManager.md) | file | App扩展管理器，单例模式，加载模块并处理依赖。 |
| [AppProperties.java](AppProperties.md) | file | 应用配置类，包含版本、构建、数据目录等属性，支持开发和生产环境设置。 |
| [AppDistributionType.java](AppDistributionType.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [AppWindowsShutdown.java](AppWindowsShutdown.md) | file | Windows关机钩子注册与处理，监听WM_QUERYENDSESSION和WM_ENDSESSION消息，支持关键关机即时退出。 |
| [AppVersion.java](AppVersion.md) | file | AppVersion类实现版本号解析、比较和字符串化，支持主次补丁号。 |
| [AppTheme.java](AppTheme.md) | file | 应用主题管理类，支持亮暗模式切换及自定义主题。 |
| [AppArguments.java](AppArguments.md) | file | 解析命令行参数，处理属性设置和异常，返回处理结果。 |
| [AppTrayIcon.java](AppTrayIcon.md) | file | AppTrayIcon类实现系统托盘图标功能，支持不同操作系统图标、菜单操作及错误提示。 |
| [AppI18n.java](AppI18n.md) | file | 国际化工具类，支持多语言切换和本地化字符串获取。 |
| [AppOpenArguments.java](AppOpenArguments.md) | file | 处理应用启动参数，支持缓冲、解析和执行文件浏览等操作。 |
| [AppDataLock.java](AppDataLock.md) | file | AppDataLock类通过文件锁实现单例应用控制，提供lock()和unlock()方法管理锁状态。 |
| [AppGreetingsDialog.java](AppGreetingsDialog.md) | file | 创建欢迎对话框，包含介绍和EULA，需用户同意才能继续。 |
| [AppTray.java](AppTray.md) | file | AppTray类实现系统托盘图标管理，包含错误处理和显示控制功能。 |
| [AppSid.java](AppSid.md) | file | 检查系统setsid命令，若无则尝试调用c函数设置进程sid，开发环境除外。 |
| [AppFileWatcher.java](AppFileWatcher.md) | file | 单例文件监视器，支持多目录递归监听文件增删改事件，异步处理异常。 |
| [AppRestart.java](AppRestart.md) | file | 生成应用重启命令，支持终端和后台模式，适配不同操作系统和Shell方言。 |
| [AppConfigurationDialog.java](AppConfigurationDialog.md) | file | 首次启动时显示配置对话框，包含语言、主题、终端和编辑器选项，宽度650，带确定按钮。 |
| [AppI18nData.java](AppI18nData.md) | file | 国际化数据类，含翻译和文档加载功能，支持变量替换。 |
| [AppLayoutModel.java](AppLayoutModel.md) | file | 单例模式管理应用布局，包含状态、条目列表和选择属性。 |
| [window](window/_module.md) | package | 跨平台窗口管理工具集，含Mac/Win原生控制、样式调整、对话框管理、边界处理等功能，支持多主题和国际化。 |
| [mode](mode/_module.md) | package | OperationMode定义三种运行模式及管理逻辑，子类BaseMode、PlatformMode、TrayMode、GuiMode分别实现初始化、切换和关闭功能。 |
| [check](check/_module.md) | package | AppShellChecker检查shell功能，异常回退处理。AppShellCheck检测系统shell问题。AppTempCheck验证临时目录。PtbDialog显示版本警告。AppTestCommandCheck检查系统环境。AppCertutilCheck检查certutil工具。AppJavaOptionsCheck检查环境变量。AppUserDirectoryCheck验证目录权限。AppDebugModeCheck打印调试警告。AppPathCorruptCheck检查PATH变量。AppRosettaCheck检测运行环境。AppAvCheck检测杀毒软件。AppGpuCheck检查GPU支持。AppHomebrewCoreutilsCheck检测coreutils。AppSystemFontCheck检查Linux字体。 |


