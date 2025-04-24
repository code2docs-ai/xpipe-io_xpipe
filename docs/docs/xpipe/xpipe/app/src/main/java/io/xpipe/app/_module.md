# 基础信息

|      |      |
|------|------|
| 名称 | app |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app |
| 包名 | xpipe.app.src.main.java.io.xpipe.app |
| 概述说明 | 跨平台JavaFX框架，含环境检查、多模式运行、窗口管理、生命周期控制等子系统。 |

# 说明

```markdown
## 概述

该代码模块是XPipe应用程序的核心框架，是一个功能全面的跨平台JavaFX桌面应用解决方案。系统采用模块化分层架构设计，主要包含以下核心子系统：

1. **应用基础框架**：
   - 环境预检系统（50+项系统检查）
   - 多模式运行框架（BACKGROUND/TRAY/GUI）
   - 生命周期管理（启动/更新/重启）
   - 国际化与主题系统

2. **数据管理**：
   - 加密存储系统（本地/远程）
   - 密码管理器集成（KeePassXC/Bitwarden等）
   - 文件浏览器与传输系统

3. **终端管理**：
   - 跨平台终端控制（支持20+终端类型）
   - 终端复用器集成（tmux/screen/zellij）
   - Shell会话管理与命令执行

4. **服务组件**：
   - HTTP信标服务（守护进程）
   - 错误报告系统（Sentry集成）
   - 自动更新机制（GitHub源）

5. **扩展体系**：
   - 模块热加载机制
   - 偏好设置管理系统（300+配置项）
   - 可扩展的UI组件库

核心特点：
- 严格的跨平台兼容性（Windows/macOS/Linux）
- 企业级安全体系（加密存储/密钥管理）
- 响应式UI设计（动态主题/布局）
- 完善的错误处理与日志系统
- 模块化扩展架构

## 主要业务场景

### 1. 应用初始化与管理
- 执行系统环境检查与配置
- 处理多模式运行（GUI/托盘/后台）
- 管理应用生命周期（更新/重启）
- 加载核心扩展模块

### 2. 数据操作
- 加密存储管理（本地/云同步）
- 密码自动填充与安全检索
- 跨平台文件浏览与传输
- 数据存储的导入/导出

### 3. 终端控制
- 创建和管理终端会话
- 执行远程/本地Shell命令
- 终端复用器窗口管理
- 终端主题与提示符定制

### 4. 系统集成
- HTTP守护进程服务
- 错误诊断与报告提交
- 自动检查并安装更新
- 系统通知与交互

### 5. 配置管理
- 偏好设置管理（UI/安全/网络等）
- 主题与外观定制
- 第三方工具集成配置
- 工作区状态管理

### 6. 扩展开发
- 模块热加载与卸载
- 自定义存储类型开发
- Shell控制功能扩展
- 自定义UI组件集成

典型工作流示例：
1. 启动时执行环境检查并加载加密保险库
2. 用户通过文件浏览器选择远程服务器
3. 自动填充SSH密码并建立终端会话
4. 在tmux中执行维护命令并监控输出
5. 错误发生时收集诊断数据并提交报告
6. 后台自动下载更新并在空闲时提示安装
```


### 包内部结构视图

```mermaid
graph TD
    app --> core
    app --> mode
    app --> window
    app --> update
    app --> issue
    app --> icon
    app --> storage
    app --> beacon
    app --> terminal
    app --> util
    app --> ext
    app --> prefs
    app --> browser
    app --> comp
    app --> password
    app --> Main.java
    core --> check
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
    update --> WebtopUpdater.java
    update --> AppInstaller.java
    update --> GitHubUpdater.java
    update --> UpdateChangelogAlert.java
    update --> UpdateAvailableDialog.java
    update --> AppDownloads.java
    update --> CommandUpdater.java
    update --> UpdateNagDialog.java
    update --> UpdateHandler.java
    update --> PortableUpdater.java
    issue --> UserReportComp.java
    issue --> AttachmentHelper.java
    issue --> ErrorHandlerDialog.java
    issue --> ErrorEvent.java
    issue --> GuiErrorHandler.java
    issue --> ErrorAction.java
    issue --> SyncErrorHandler.java
    issue --> ErrorDetailsComp.java
    issue --> ErrorHandlerComp.java
    issue --> TrackEvent.java
    issue --> GuiErrorHandlerBase.java
    issue --> SentryErrorHandler.java
    issue --> EventHandlerImpl.java
    issue --> ErrorHandler.java
    issue --> TerminalErrorHandler.java
    issue --> LogErrorHandler.java
    issue --> EventHandler.java
    icon --> SystemIconSource.java
    icon --> SystemIcon.java
    icon --> SystemIconManager.java
    icon --> SystemIconCache.java
    icon --> SystemIconSourceFile.java
    icon --> SystemIconSourceData.java
    storage --> StorageListener.java
    storage --> DataStorageQuery.java
    storage --> ContextualFileReference.java
    storage --> ImpersistentStorage.java
    storage --> DataStorageSecret.java
    storage --> DataStorageSyncHandler.java
    storage --> DataStoreEntryRef.java
    storage --> StandardStorage.java
    storage --> StorageElement.java
    storage --> DataStorageNode.java
    storage --> DataStoreCategory.java
    storage --> DataStorage.java
    storage --> DataStoreCategoryConfig.java
    storage --> DataStorageUserHandler.java
    storage --> DataStoreEntry.java
    storage --> DataStateProviderImpl.java
    storage --> DataStoreColor.java
    storage --> DataStoreEntryUserScope.java
    beacon --> impl
    impl --> FsWriteExchangeImpl.java
    impl --> TerminalWaitExchangeImpl.java
    impl --> ConnectionAddExchangeImpl.java
    impl --> ShellStopExchangeImpl.java
    impl --> DaemonOpenExchangeImpl.java
    impl --> DaemonFocusExchangeImpl.java
    impl --> ConnectionToggleExchangeImpl.java
    impl --> FsScriptExchangeImpl.java
    impl --> TerminalExternalLaunchExchangeImpl.java
    impl --> DaemonStopExchangeImpl.java
    impl --> DaemonVersionExchangeImpl.java
    impl --> CategoryAddExchangeImpl.java
    impl --> ShellExecExchangeImpl.java
    impl --> FsBlobExchangeImpl.java
    impl --> TerminalPrepareExchangeImpl.java
    impl --> FsReadExchangeImpl.java
    impl --> ConnectionRefreshExchangeImpl.java
    impl --> TerminalLaunchExchangeImpl.java
    impl --> HandshakeExchangeImpl.java
    impl --> AskpassExchangeImpl.java
    impl --> ConnectionRemoveExchangeImpl.java
    impl --> ConnectionTerminalExchangeImpl.java
    impl --> ConnectionQueryExchangeImpl.java
    impl --> DaemonStatusExchangeImpl.java
    impl --> ShellStartExchangeImpl.java
    impl --> ConnectionInfoExchangeImpl.java
    impl --> DaemonModeExchangeImpl.java
    impl --> ConnectionBrowseExchangeImpl.java
    impl --> TerminalRegisterExchangeImpl.java
    impl --> SshLaunchExchangeImpl.java
    beacon --> AppBeaconServer.java
    beacon --> BeaconShellSession.java
    beacon --> BlobManager.java
    beacon --> AppBeaconCache.java
    beacon --> BeaconRequestHandler.java
    beacon --> BeaconSession.java
    terminal --> ExternalTerminalType.java
    terminal --> PwshTerminalType.java
    terminal --> TerminalLauncherManager.java
    terminal --> TmuxTerminalMultiplexer.java
    terminal --> TerminalPromptManager.java
    terminal --> TerminalMultiplexer.java
    terminal --> TermiusTerminalType.java
    terminal --> ClinkHelper.java
    terminal --> CmdTerminalType.java
    terminal --> ScreenTerminalMultiplexer.java
    terminal --> TerminalDockComp.java
    terminal --> ZellijTerminalMultiplexer.java
    terminal --> WarpTerminalType.java
    terminal --> PowerShellTerminalType.java
    terminal --> WindowsTerminalSession.java
    terminal --> OhMyPoshTerminalPrompt.java
    terminal --> TabbyTerminalType.java
    terminal --> AlacrittyTerminalType.java
    terminal --> GnomeTerminalType.java
    terminal --> SecureCrtTerminalType.java
    terminal --> WaveTerminalType.java
    terminal --> TerminalView.java
    terminal --> TerminalMultiplexerManager.java
    terminal --> TerminalLaunchConfiguration.java
    terminal --> TerminalPrompt.java
    terminal --> WezTerminalType.java
    terminal --> CustomTerminalType.java
    terminal --> TerminalLauncher.java
    terminal --> GnomeConsoleType.java
    terminal --> ControllableTerminalSession.java
    terminal --> TerminalLaunchRequest.java
    terminal --> MobaXTermTerminalType.java
    terminal --> TrackableTerminalType.java
    terminal --> PtyxisTerminalType.java
    terminal --> KittyTerminalType.java
    terminal --> TerminalDockModel.java
    terminal --> StarshipTerminalPrompt.java
    terminal --> TerminalLaunchResult.java
    terminal --> OhMyZshTerminalPrompt.java
    terminal --> TerminalOpenFormat.java
    terminal --> ConfigFileTerminalPrompt.java
    terminal --> XShellTerminalType.java
    terminal --> TerminalProxyManager.java
    terminal --> WindowsTerminalType.java
    util --> SecretQueryState.java
    util --> Rect.java
    util --> ContextMenuHelper.java
    util --> PlatformThread.java
    util --> BindingsHelper.java
    util --> StoreStateFormat.java
    util --> BooleanAnimationTimer.java
    util --> CommandSupport.java
    util --> InputHelper.java
    util --> ShellControlCache.java
    util --> SecretQuery.java
    util --> FileOpener.java
    util --> OptionsBuilder.java
    util --> AskpassAlert.java
    util --> FileBridge.java
    util --> ScriptHelper.java
    util --> EncryptionToken.java
    util --> OptionsChoiceBuilder.java
    util --> HttpHelper.java
    util --> DocumentationLink.java
    util --> RdpConfig.java
    util --> MacOsPermissions.java
    util --> MarkdownHelper.java
    util --> GithubReleaseDownloader.java
    util --> SimpleFilterInputStream.java
    util --> DataStoreFormatter.java
    util --> AppJacksonModule.java
    util --> DerivedObservableList.java
    util --> JfxHelper.java
    util --> SecretManager.java
    util --> NativeBridge.java
    util --> FileReference.java
    util --> SecretQueryFilter.java
    util --> FixedHierarchyStore.java
    util --> ShellTemp.java
    util --> ScanDialogBase.java
    util --> SecretRetrievalStrategy.java
    util --> PlatformInit.java
    util --> Translatable.java
    util --> ThreadHelper.java
    util --> SecretQueryFormatter.java
    util --> WindowsRegistry.java
    util --> EncryptedValue.java
    util --> LocalShell.java
    util --> DesktopHelper.java
    util --> CommandDialog.java
    util --> ScanDialog.java
    util --> DesktopShortcuts.java
    util --> ChainedValidator.java
    util --> SimpleValidator.java
    util --> NodeHelper.java
    util --> ModuleAccess.java
    util --> ScanSingleDialogComp.java
    util --> Hyperlinks.java
    util --> DataStoreCategoryChoiceComp.java
    util --> ClipboardHelper.java
    util --> LicensedFeature.java
    util --> CommandView.java
    util --> SecretQueryResult.java
    util --> PasswdFile.java
    util --> SecretRetrievalStrategyHelper.java
    util --> ColorHelper.java
    util --> SshLocalBridge.java
    util --> HumanReadableFormat.java
    util --> LicenseRequiredException.java
    util --> LicenseProvider.java
    util --> ProgressScope.java
    util --> BooleanScope.java
    util --> Validator.java
    util --> NodeCallback.java
    util --> VaultKeySecretValue.java
    util --> PasswordLockSecretValue.java
    util --> ScanMultiDialogComp.java
    util --> EncryptionKey.java
    util --> LabelGraphic.java
    util --> AsktextAlert.java
    util --> PlatformState.java
    util --> ScanDialogAction.java
    util --> Validators.java
    util --> ExclusiveValidator.java
    util --> SecretQueryProgress.java
    util --> FixedSizeInputStream.java
    util --> LocalExec.java
    util --> GlobalTimer.java
    util --> HostHelper.java
    util --> CommandViewBase.java
    util --> BaseElevationHandler.java
    util --> LocalShellCache.java
    ext --> DataStoreProviders.java
    ext --> ActionProvider.java
    ext --> NameableStore.java
    ext --> DataStoreProvider.java
    ext --> ShellControlFunction.java
    ext --> SingletonSessionStoreProvider.java
    ext --> PrefsHandler.java
    ext --> GuiDialog.java
    ext --> PrefsProvider.java
    ext --> DataStoreUsageCategory.java
    ext --> ExtensionException.java
    ext --> ShellSession.java
    ext --> EnabledParentStoreProvider.java
    ext --> ScanProvider.java
    ext --> UserBasedValue.java
    ext --> ContainerImageStore.java
    ext --> UserScopeStore.java
    ext --> ProcessControlProvider.java
    ext --> ContainerStoreState.java
    ext --> ShellControlParentStoreFunction.java
    ext --> LocalStore.java
    ext --> DataStorageExtensionProvider.java
    ext --> PrefsChoiceValue.java
    ext --> DataStoreCreationCategory.java
    ext --> ShellStore.java
    ext --> ConnectionFileSystem.java
    prefs --> AppearanceCategory.java
    prefs --> AppPrefsComp.java
    prefs --> HttpApiCategory.java
    prefs --> RdpCategory.java
    prefs --> EditorCategory.java
    prefs --> AppPrefsStorageHandler.java
    prefs --> ThirdPartyDependency.java
    prefs --> UpdateCheckComp.java
    prefs --> VaultCategory.java
    prefs --> SystemCategory.java
    prefs --> SshCategory.java
    prefs --> SecurityCategory.java
    prefs --> WorkspaceCreationDialog.java
    prefs --> LoggingCategory.java
    prefs --> ExternalApplicationHelper.java
    prefs --> AboutCategory.java
    prefs --> CloseBehaviour.java
    prefs --> TroubleshootCategory.java
    prefs --> StartupBehaviour.java
    prefs --> ExternalRdpClientType.java
    prefs --> ConnectionHubCategory.java
    prefs --> ThirdPartyDependencyListComp.java
    prefs --> CloseBehaviourDialog.java
    prefs --> FileBrowserCategory.java
    prefs --> WorkspacesCategory.java
    prefs --> AppPrefsSidebarComp.java
    prefs --> ExternalApplicationType.java
    prefs --> DeveloperCategory.java
    prefs --> IconsCategory.java
    prefs --> LinksCategory.java
    prefs --> SyncCategory.java
    prefs --> TerminalCategory.java
    prefs --> AppPrefs.java
    prefs --> UpdatesCategory.java
    prefs --> ExternalEditorType.java
    prefs --> AppPrefsCategory.java
    prefs --> SupportedLocale.java
    prefs --> PasswordManagerCategory.java
    browser --> icon
    icon --> BrowserIconFileType.java
    icon --> BrowserIcons.java
    icon --> BrowserIconDirectoryType.java
    icon --> BrowserIconManager.java
    icon --> BrowserIconVariant.java
    browser --> file
    file --> BrowserFileSystemCache.java
    file --> BrowserFileSystemHelper.java
    file --> BrowserConnectionListFilterComp.java
    file --> BrowserFileTransferMode.java
    file --> BrowserQuickAccessContextMenu.java
    file --> BrowserNavBarComp.java
    file --> BrowserFileListNameCell.java
    file --> BrowserFileOpener.java
    file --> BrowserFileSystemTabModel.java
    file --> BrowserTransferProgress.java
    file --> BrowserHistorySavedState.java
    file --> BrowserClipboard.java
    file --> BrowserTransferModel.java
    file --> BrowserContextMenu.java
    file --> BrowserQuickAccessButtonComp.java
    file --> BrowserLocalFileSystem.java
    file --> BrowserAlerts.java
    file --> BrowserFileSystemTabComp.java
    file --> BrowserHistorySavedStateImpl.java
    file --> BrowserOverviewComp.java
    file --> BrowserFileSelectionListComp.java
    file --> BrowserTerminalDockTabModel.java
    file --> BrowserFileListFilterComp.java
    file --> BrowserFileListModel.java
    file --> BrowserBreadcrumbBar.java
    file --> BrowserFileTransferOperation.java
    file --> BrowserConnectionListComp.java
    file --> BrowserFileOverviewComp.java
    file --> BrowserStatusBarComp.java
    file --> BrowserFileSystemHistory.java
    file --> BrowserTransferComp.java
    file --> BrowserHistoryTabModel.java
    file --> BrowserHistoryTabComp.java
    file --> BrowserFileSystemSavedState.java
    file --> BrowserFileListCompEntry.java
    file --> BrowserFileListComp.java
    file --> BrowserGreetingComp.java
    file --> BrowserEntry.java
    browser --> action
    action --> BrowserAction.java
    action --> BrowserApplicationPathAction.java
    action --> BrowserActionFormatter.java
    action --> BrowserBranchAction.java
    action --> BrowserLeafAction.java
    browser --> BrowserFullSessionComp.java
    browser --> BrowserFullSessionModel.java
    browser --> BrowserFileChooserSessionModel.java
    browser --> BrowserStoreSessionTab.java
    browser --> BrowserSessionTabsComp.java
    browser --> BrowserAbstractSessionModel.java
    browser --> BrowserFileChooserSessionComp.java
    browser --> BrowserSessionTab.java
    comp --> base
    base --> PopupMenuButtonComp.java
    base --> FontIconComp.java
    base --> IntegratedTextAreaComp.java
    base --> FileDropOverlayComp.java
    base --> AppMainWindowContentComp.java
    base --> ModalOverlay.java
    base --> LazyTextFieldComp.java
    base --> MarkdownEditorComp.java
    base --> IntroComp.java
    base --> PrettyImageComp.java
    base --> TextFieldComp.java
    base --> SideMenuBarComp.java
    base --> AppLayoutComp.java
    base --> ListBoxViewComp.java
    base --> VerticalComp.java
    base --> ToggleGroupComp.java
    base --> ChoiceComp.java
    base --> LeftSplitPaneComp.java
    base --> DialogComp.java
    base --> PrettyImageHelper.java
    base --> FilterComp.java
    base --> ModalOverlayComp.java
    base --> CountComp.java
    base --> TooltipHelper.java
    base --> TextAreaComp.java
    base --> IntFieldComp.java
    base --> ModalOverlayStackComp.java
    base --> DelayedInitComp.java
    base --> ModalOverlayContentComp.java
    base --> LabelComp.java
    base --> ToggleSwitchComp.java
    base --> ListSelectorComp.java
    base --> ContextualFileReferenceSync.java
    base --> LoadingOverlayComp.java
    base --> StackComp.java
    base --> ChoicePaneComp.java
    base --> ModalButton.java
    base --> HorizontalComp.java
    base --> InputGroupComp.java
    base --> ScrollComp.java
    base --> SecretFieldComp.java
    base --> IntComboFieldComp.java
    base --> ButtonComp.java
    base --> IconButtonComp.java
    base --> OptionsComp.java
    base --> MarkdownComp.java
    base --> ComboTextFieldComp.java
    base --> ContextualFileReferenceChoiceComp.java
    base --> AnchorComp.java
    base --> SimpleTitledPaneComp.java
    base --> ToolbarComp.java
    base --> TileButtonComp.java
    base --> IntroListComp.java
    base --> MultiContentComp.java
    base --> DropdownComp.java
    comp --> store
    store --> StoreCreationConsumer.java
    store --> OsLogoComp.java
    store --> SystemStateComp.java
    store --> StoreCategoryListComp.java
    store --> StoreCreationModel.java
    store --> StoreSectionBaseComp.java
    store --> StoreActiveComp.java
    store --> StoreNotFoundComp.java
    store --> StoreCreationMenu.java
    store --> StoreSectionMiniComp.java
    store --> StoreIntroComp.java
    store --> DenseStoreEntryComp.java
    store --> StoreIdentitiesIntroComp.java
    store --> StoreEntryListOverviewComp.java
    store --> StoreEntryListStatusBarComp.java
    store --> StoreIconComp.java
    store --> StoreChoiceComp.java
    store --> StoreEntryBatchSelectComp.java
    store --> StoreSidebarComp.java
    store --> StoreNotesComp.java
    store --> StoreListChoiceComp.java
    store --> StoreCreationDialog.java
    store --> StoreSectionComp.java
    store --> StoreViewState.java
    store --> StoreScriptsIntroComp.java
    store --> StoreCategoryComp.java
    store --> StoreCategoryWrapper.java
    store --> StoreIconChoiceDialog.java
    store --> StoreLayoutComp.java
    store --> StoreQuickAccessButtonComp.java
    store --> StoreProviderChoiceComp.java
    store --> StoreToggleComp.java
    store --> StoreEntryComp.java
    store --> StoreCreationComp.java
    store --> StoreEntryListComp.java
    store --> StoreSection.java
    store --> StandardStoreEntryComp.java
    store --> StoreNotes.java
    store --> StoreSortMode.java
    store --> StoreEntryWrapper.java
    store --> StoreIconChoiceComp.java
    store --> StoreCategoryConfigComp.java
    comp --> augment
    augment --> Augment.java
    augment -->

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [Main.java](Main.md) | file | Java主类，处理命令行参数version和--help，否则初始化操作模式。 |
| [password](password/_module.md) | package | KeePassXcAssociationKey类含id和key字段，支持建造者模式。TweetNaClHelper实现X25519加密。Bitwarden等类通过CLI管理密码。KeePassXcProxyClient安全通信。WindowsCredentialManager读取凭据。 |
| [comp](comp/_module.md) | package | JavaFX UI组件库，含基础控件、布局容器和主题支持。商店管理系统组件集合，支持CRUD和分类管理。UI增强工具集，含尺寸调整和菜单管理。简单组件结构类封装Region。抽象组件类支持链式配置。模板类强制子类实现Region创建。 |
| [browser](browser/_module.md) | package | 浏览器图标管理系统，支持文件/目录图标动态加载、主题适配和统一尺寸处理。 |
| [prefs](prefs/_module.md) | package | 应用偏好设置类实现，管理外观、终端、安全等配置选项，支持多平台和自定义设置。 |
| [ext](ext/_module.md) | package | DataStoreProviders类管理数据存储提供者初始化和操作。PrefsProvider抽象类管理偏好设置。ShellSession管理ShellControl生命周期。ProcessControlProvider提供进程控制功能。LocalStore实现本地存储接口。ConnectionFileSystem通过ShellControl执行文件操作。 |
| [util](util/_module.md) | package | 多个Java工具类，功能涵盖UI组件、文件操作、加密验证、线程管理等。 |
| [terminal](terminal/_module.md) | package | 多个终端相关类实现，包括PowerShell、Cmd、Tmux等终端类型和管理器，支持启动、配置及会话管理功能。 |
| [beacon](beacon/_module.md) | package | HTTP守护进程框架，提供终端管理、文件操作、连接控制、Shell会话等功能，支持多种Exchange实现类处理请求。 |
| [storage](storage/_module.md) | package | 数据存储相关Java类集合，包含查询、加密、同步、引用等功能模块，管理存储条目、类别及路径处理。 |
| [icon](icon/_module.md) | package | 系统图标管理类，包含源数据、缓存、颜色方案处理及文件路径生成功能。 |
| [issue](issue/_module.md) | package | 用户报告组件处理错误提交Sentry，含邮件、描述和附件功能。压缩工具类递归压缩目录为ZIP。错误处理类显示对话框，含堆栈跟踪和报告按钮。ErrorEvent类构建灵活错误处理。GUI错误处理器结合日志和许可证验证。同步错误处理器确保顺序处理。错误详情组件显示去混淆堆栈跟踪。事件处理器转换错误为跟踪事件并处理。终端错误处理器记录错误并安全退出。日志处理器记录或输出错误信息。事件处理器抽象类集中管理事件处理逻辑。 |
| [update](update/_module.md) | package | WebtopUpdater添加模态按钮。AppInstaller支持多平台安装。GitHubUpdater处理更新操作。UpdateChangelogAlert显示变更日志。UpdateAvailableDialog条件显示更新。AppDownloads管理下载。CommandUpdater执行脚本更新。UpdateNagDialog非强制提醒。UpdateHandler抽象更新流程。PortableUpdater便携版更新处理。 |
| [core](core/_module.md) | package | 系统环境检查工具集，覆盖Shell、目录、平台、安全等验证。多模式运行框架支持后台、托盘、GUI模式切换。窗口管理工具提供跨平台样式控制、对话框和布局管理。字体、缓存、国际化、日志等核心功能模块。应用管理包括启动参数、实例控制、主题、版本等功能。 |


