# 基础信息

|      |      |
|------|------|
| 名称 | util |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/util |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.util |
| 概述说明 | 多个Java工具类，功能涵盖UI组件、文件操作、加密验证、线程管理等。 |

# 说明

```markdown
## 概述
该代码模块是一个综合性的Java工具库，主要服务于XPipe应用程序，提供跨平台支持、UI组件管理、安全加密、文件操作等核心功能。模块采用模块化设计，包含50+个工具类，覆盖以下关键领域：

1. **UI工具集**：ContextMenuHelper/JfxHelper等提供JavaFX组件构建与事件处理
2. **线程与同步**：PlatformThread/ThreadHelper实现跨线程任务调度
3. **安全体系**：SecretManager/EncryptionToken等构建完整的密钥管理机制
4. **文件处理**：FileBridge/FileOpener支持跨平台文件操作
5. **命令行工具**：CommandSupport/ShellControlCache管理Shell交互
6. **数据绑定**：BindingsHelper/DerivedObservableList实现响应式数据流

核心特点包括：
- 全面的异常处理机制
- 强类型安全设计
- 支持Windows/Linux/macOS三平台
- 基于JavaFX的UI工具链
- 模块间低耦合高内聚

## 主要业务场景
### 1. 安全认证管理
- `SecretManager`集中管理密钥生命周期
- `AskpassAlert`实现密码输入对话框
- `EncryptionToken`处理用户/保险库令牌
- 支持双因素认证和SSH密钥验证

### 2. 跨平台文件操作
- `FileOpener`按系统类型调用默认程序
- `ShellTemp`管理平台差异化的临时目录
- `DesktopShortcuts`生成三系统快捷方式
- `FileBridge`监控文件变更事件

### 3. 命令行工具链
- `CommandSupport`验证程序路径
- `LocalShell`管理本地Shell进程
- `CommandDialog`显示异步命令输出
- `ScriptHelper`生成适配Shell方言的脚本

### 4. 动态UI构建
- `OptionsBuilder`链式配置复杂表单
- `ContextMenuHelper`创建智能右键菜单
- `BooleanAnimationTimer`驱动UI动画
- `ScanDialog`构建可扩展的扫描界面

### 5. 数据序列化
- `AppJacksonModule`定制JSON序列化规则
- `EncryptedValue`处理加密数据存储
- `RdpConfig`解析键值对配置格式
- `StoreStateFormat`标准化状态输出

### 6. 系统集成
- `WindowsRegistry`操作注册表
- `MacOsPermissions`处理权限申请
- `DesktopHelper`打开系统浏览器
- `NativeBridge`加载本地库

典型工作流示例：
1. 用户通过`AskpassAlert`输入密码
2. `SecretManager`缓存加密后的凭证
3. `CommandSupport`验证目标程序路径
4. `LocalShell`执行加密脚本(`ScriptHelper`生成)
5. `PlatformThread`确保UI线程安全更新
6. `FileBridge`监控生成的临时文件
```


### 包内部结构视图

```mermaid
graph TD
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
```

该流程图展示了`util`目录下的所有Java文件层级关系，共包含63个文件节点。这些文件涵盖了工具类、辅助功能、加密处理、平台适配等多样化功能模块，体现了该目录作为核心工具包的高度聚合性。所有文件均直接隶属于`util`节点，无次级目录结构，呈现扁平化组织特征。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [LicenseProvider.java](LicenseProvider.md) | file | 抽象类LicenseProvider提供许可证管理功能，包括获取实例、更新日期、检查许可证状态、获取特征及初始化等。 |
| [DataStoreCategoryChoiceComp.java](DataStoreCategoryChoiceComp.md) | file | 数据存储分类选择组件，含根节点、外部属性和值属性，使用组合框展示分类并处理值变更。 |
| [LocalShellCache.java](LocalShellCache.md) | file | LocalShellCache类继承ShellControlCache，提供获取VS Code CLI路径的方法，支持不同操作系统。 |
| [SecretQueryProgress.java](SecretQueryProgress.md) | file | SecretQueryProgress类处理秘密查询进度，包含请求ID、存储ID、供应商列表、回退查询、过滤器和格式化器，支持交互式操作和状态管理。 |
| [ScanDialogAction.java](ScanDialogAction.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [AsktextAlert.java](AsktextAlert.md) | file | Java类AsktextAlert提供静态方法query，显示带输入框的确认弹窗，返回用户输入文本。 |
| [SecretQuery.java](SecretQuery.md) | file | 输入为空，无法生成概要。请提供具体内容。 |
| [ShellControlCache.java](ShellControlCache.md) | file | ShellControlCache类，含ShellControl和两个Map，提供缓存操作和路径应用检查功能。 |
| [InputHelper.java](InputHelper.md) | file | InputHelper类提供键盘事件处理功能，支持组合键、方向键及导航键监听。 |
| [CommandSupport.java](CommandSupport.md) | file | CommandSupport类提供查找程序路径、检查程序是否在PATH中及相关异常处理功能。 |
| [BooleanAnimationTimer.java](BooleanAnimationTimer.md) | file | 布尔动画计时器，监听布尔值变化，触发延时执行任务。 |
| [StoreStateFormat.java](StoreStateFormat.md) | file | StoreStateFormat类提供格式化shell环境和存储状态的方法，支持许可证检查和状态拼接。 |
| [BindingsHelper.java](BindingsHelper.md) | file | BindingsHelper类提供对象绑定和弱引用管理功能，包含映射、扁平映射及自动垃圾回收机制。 |
| [PlatformThread.java](PlatformThread.md) | file | PlatformThread类提供同步Observable值和列表的方法，确保线程安全并处理事件循环。 |
| [ContextMenuHelper.java](ContextMenuHelper.md) | file | ContextMenuHelper类提供创建、配置和切换上下文菜单的方法，包括自动隐藏、宽度限制和焦点控制。 |
| [Rect.java](Rect.md) | file | 值类Rect定义，含坐标x,y和宽高w,h。 |
| [MacOsPermissions.java](MacOsPermissions.md) | file | 检查MacOS权限，等待辅助功能授权，模拟按键测试权限状态。 |
| [RdpConfig.java](RdpConfig.md) | file | RdpConfig类解析文件内容并存储键值对，支持覆盖、删除和查询操作。 |
| [DocumentationLink.java](DocumentationLink.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [OptionsChoiceBuilder.java](OptionsChoiceBuilder.md) | file | OptionsChoiceBuilder类：通过反射处理子类选项，支持空值绑定与动态属性更新。 |
| [EncryptionToken.java](EncryptionToken.md) | file | 加密令牌类，含用户和保险库令牌管理，支持创建、验证和解密功能。 |
| [ScriptHelper.java](ScriptHelper.md) | file | ScriptHelper类提供脚本处理功能，包括生成脚本哈希、创建本地/远程可执行脚本及终端密码脚本。 |
| [FileBridge.java](FileBridge.md) | file | 文件桥接类，管理临时文件操作和事件处理。 |
| [AskpassAlert.java](AskpassAlert.md) | file | 显示密码输入弹窗，支持特殊提示帮助链接，自动聚焦处理，返回输入结果或取消状态。 |
| [OptionsBuilder.java](OptionsBuilder.md) | file | OptionsBuilder类用于构建选项界面，支持验证器、属性绑定和多种控件类型。 |
| [SecretQueryFilter.java](SecretQueryFilter.md) | file | 输入为空，无法生成概要描述。请提供具体内容。 |
| [NativeBridge.java](NativeBridge.md) | file | NativeBridge类初始化MacOS库，检查条件后加载xpipe_bridge库，提供外观设置接口。 |
| [SecretManager.java](SecretManager.md) | file | SecretManager类管理密钥查询进度和缓存，提供查询、清理和缓存功能，支持交互式处理和特殊提示识别。 |
| [JfxHelper.java](JfxHelper.md) | file | 创建带名称和描述的UI组件，可选图片。 |
| [DerivedObservableList.java](DerivedObservableList.md) | file | DerivedObservableList类提供线程安全、可映射、过滤和排序的列表操作。 |
| [AppJacksonModule.java](AppJacksonModule.md) | file | 自定义Jackson模块，注册子类型及序列化器，处理加密值和文件引用等。 |
| [DataStoreFormatter.java](DataStoreFormatter.md) | file | DataStoreFormatter类提供字符串格式化工具，包括连接、截断、大小写转换等功能。 |
| [SimpleFilterInputStream.java](SimpleFilterInputStream.md) | file | 抽象输入流类，实现读取字节方法，支持单字节和字节数组读取。 |
| [GithubReleaseDownloader.java](GithubReleaseDownloader.md) | file | GitHub发布下载器类，含获取临时文件和下载链接方法。 |
| [LocalShell.java](LocalShell.md) | file | 本地Shell管理类，含初始化、重置、获取Shell及PowerShell功能，支持缓存和异常处理。 |
| [EncryptedValue.java](EncryptedValue.md) | file | 抽象类EncryptedValue定义加密值处理，含CurrentKey和VaultKey子类，支持空值检查、密钥存储及值更新。 |
| [WindowsRegistry.java](WindowsRegistry.md) | file | WindowsRegistry类提供本地和远程注册表操作，包括查询键值、递归搜索等功能。 |
| [SecretQueryFormatter.java](SecretQueryFormatter.md) | file | 输入内容为空，无法生成概要。请提供具体信息以便总结。 |
| [ThreadHelper.java](ThreadHelper.md) | file | 线程辅助类，封装虚拟/平台线程创建、调试跟踪、异常处理及并发加载功能。 |
| [Translatable.java](Translatable.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [PlatformInit.java](PlatformInit.md) | file | 平台初始化类，同步异步加载，异常处理，多线程控制。 |
| [SecretRetrievalStrategy.java](SecretRetrievalStrategy.md) | file | 当前输入内容为空，无法生成概要描述。请提供具体信息以便提炼关键点。 |
| [ScanDialogBase.java](ScanDialogBase.md) | file | 扫描对话框基类，含展开选项、关闭操作、扫描动作及数据存储条目处理。 |
| [ShellTemp.java](ShellTemp.md) | file | ShellTemp类提供跨平台临时目录管理，支持Linux用户隔离，检查权限并创建子目录。 |
| [Hyperlinks.java](Hyperlinks.md) | file | Hyperlinks类包含XPipe项目文档、GitHub、翻译、Discord等链接及打开方法。 |
| [ScanSingleDialogComp.java](ScanSingleDialogComp.md) | file | 扫描对话框组件，继承ModalOverlayContentComp，包含初始存储、属性绑定和基础操作。 |
| [ModuleAccess.java](ModuleAccess.md) | file | ModuleAccess类通过反射动态导出和开放模块包访问权限。 |
| [NodeHelper.java](NodeHelper.md) | file | 检查节点是否为父节点，支持单节点和集合。 |
| [SimpleValidator.java](SimpleValidator.md) | file | Java验证器类，管理检查项并跟踪验证结果和错误状态。 |
| [ChainedValidator.java](ChainedValidator.md) | file | 链式验证器类，管理多个验证器，聚合验证结果和错误状态。 |
| [DesktopShortcuts.java](DesktopShortcuts.md) | file | 为不同操作系统创建桌面快捷方式：Windows用PowerShell生成.lnk，Linux写.desktop文件，MacOS构建.app包。 |
| [ScanDialog.java](ScanDialog.md) | file | 扫描对话框类，支持单条和多条数据扫描，含异步处理和模态窗口交互。 |
| [CommandDialog.java](CommandDialog.md) | file | 异步执行命令并显示输出，支持单命令和批量处理，格式化长文本，异常捕获和模态框展示。 |
| [LicenseRequiredException.java](LicenseRequiredException.md) | file | 自定义异常类，检查许可证功能是否授权。 |
| [HumanReadableFormat.java](HumanReadableFormat.md) | file | HumanReadableFormat类提供日期、字节大小和持续时间的格式化方法。 |
| [SshLocalBridge.java](SshLocalBridge.md) | file | SSH本地桥接类，管理密钥、配置和端口，支持单例模式与远程命令执行。 |
| [ColorHelper.java](ColorHelper.md) | file | ColorHelper类提供颜色转换和透明度调整功能。 |
| [SecretRetrievalStrategyHelper.java](SecretRetrievalStrategyHelper.md) | file | SecretRetrievalStrategyHelper类提供三种密码策略：本地存储、密码管理器、自定义命令，并支持策略选择和绑定。 |
| [PasswdFile.java](PasswdFile.md) | file | 解析PasswdFile类，加载用户信息并提供UID查询功能。 |
| [SecretQueryResult.java](SecretQueryResult.md) | file | SecretQueryResult包含secret和state两个字段。 |
| [CommandView.java](CommandView.md) | file | 抽象类CommandView实现AutoCloseable，含构建命令、获取Shell控制及启动方法，关闭时自动释放Shell资源。 |
| [LicensedFeature.java](LicensedFeature.md) | file | 输入内容为空，无法生成概要。请提供具体信息以便总结。 |
| [ClipboardHelper.java](ClipboardHelper.md) | file | 复制密码和文本到剪贴板，15秒后自动清除密码。 |
| [PlatformState.java](PlatformState.md) | file | 输入内容为空，无法生成概要。 |
| [LabelGraphic.java](LabelGraphic.md) | file | 抽象类LabelGraphic定义图形标签，包含无图形、图标、图片、组件和节点五种实现。 |
| [EncryptionKey.java](EncryptionKey.md) | file | 加密密钥生成类，含三种方法：安全密钥生成、旧版密钥生成、保险库密钥生成，均基于PBKDF2算法。 |
| [ScanMultiDialogComp.java](ScanMultiDialogComp.md) | file | ScanMultiDialogComp继承ModalOverlayContentComp，包含扫描对话框基础功能，支持完成操作和状态管理。 |
| [PasswordLockSecretValue.java](PasswordLockSecretValue.md) | file | 密码锁密值类，继承AES加密，含构造器、密钥获取及字符串转换方法。 |
| [VaultKeySecretValue.java](VaultKeySecretValue.md) | file | VaultKeySecretValue类继承AesSecretValue，提供加密值存储和密钥管理功能。 |
| [NodeCallback.java](NodeCallback.md) | file | 监控JavaFX节点线程访问，确保UI操作在主线程执行。 |
| [Validator.java](Validator.md) | file | 当前输入内容为空，请提供需要总结的具体信息。 |
| [BooleanScope.java](BooleanScope.md) | file | BooleanScope类实现AutoCloseable，用于布尔属性线程安全操作，支持独占执行和自动关闭。 |
| [ProgressScope.java](ProgressScope.md) | file | ProgressScope类实现进度管理，支持平台线程强制更新和自动关闭。 |
| [BaseElevationHandler.java](BaseElevationHandler.md) | file | BaseElevationHandler类实现ElevationHandler接口，处理请求和获取密钥引用。 |
| [CommandViewBase.java](CommandViewBase.md) | file | 抽象类CommandViewBase继承CommandView，含ShellControl成员和构造方法，定义抽象方法build。 |
| [HostHelper.java](HostHelper.md) | file | HostHelper类提供随机端口生成、本地端口查找和本地主机判断功能。 |
| [GlobalTimer.java](GlobalTimer.md) | file | 全局定时器类，提供初始化、重置、定时任务调度及异步延迟执行功能。 |
| [LocalExec.java](LocalExec.md) | file | 执行本地命令并返回标准输出，失败返回空。 |
| [FixedSizeInputStream.java](FixedSizeInputStream.md) | file | 固定大小输入流，限制读取字节数，超限返回-1。 |
| [ExclusiveValidator.java](ExclusiveValidator.md) | file | ExclusiveValidator根据输入值选择对应验证器并代理其方法。 |
| [Validators.java](Validators.md) | file | 验证工具类，检查类型、非空及非空字符串。 |
| [DesktopHelper.java](DesktopHelper.md) | file | 跨平台桌面工具类，支持打开URL、获取桌面/下载目录路径及浏览文件路径。 |
| [FixedHierarchyStore.java](FixedHierarchyStore.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息。 |
| [FileReference.java](FileReference.md) | file | 文件引用类，包含文件系统和路径，支持本地文件操作。 |
| [MarkdownHelper.java](MarkdownHelper.md) | file | Java类MarkdownHelper将Markdown转HTML，支持扩展和自定义样式。 |
| [HttpHelper.java](HttpHelper.md) | file | 创建HTTP客户端，可选禁用SSL认证。 |
| [FileOpener.java](FileOpener.md) | file | 文件操作类，提供文本编辑器打开、默认应用打开及字符串读写功能，支持多平台错误处理。 |
| [SecretQueryState.java](SecretQueryState.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |


