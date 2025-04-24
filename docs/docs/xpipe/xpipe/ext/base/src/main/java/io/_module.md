# 基础信息

|      |      |
|------|------|
| 名称 | io |
| 编码语言 | .java |
| 代码路径 | xpipe/ext/base/src/main/java/io |
| 包名 | xpipe.ext.base.src.main.java.io |
| 概述说明 | 身份管理核心模块，含存储、验证策略、数据转换和GUI组件。服务框架管理存储、组和控制，支持自定义服务。脚本系统管理存储、执行和编辑，支持多Shell类型。存储基础功能提供启停暂停操作。文件浏览器支持跨平台操作。桌面应用管理配置和启动。数据存储操作框架支持多种功能。 |

# 说明

## 概述

该代码模块是一个综合性的系统管理框架，主要提供身份管理、服务管理、脚本管理、存储操作和文件浏览等核心功能。模块基于Java构建，采用分层设计和面向对象编程原则，使用Lombok简化代码，Jackson处理序列化。各子模块通过统一的接口和抽象类实现松耦合，同时保持功能完整性。主要特点包括：

1. **模块化设计**：各功能领域（身份/服务/脚本等）有独立实现但共享基础架构
2. **策略模式**：在身份验证、服务控制等场景中广泛应用策略模式
3. **GUI集成**：统一提供配置对话框、操作按钮等可视化组件
4. **跨平台支持**：特别是文件浏览器模块实现多平台适配
5. **生命周期管理**：贯穿存储、服务、脚本等各个模块的统一管理范式

## 主要业务场景

### 1. 身份认证与管理
- **多模式身份存储**：本地存储(`LocalIdentityStore`)与同步存储(`SyncedIdentityStore`)双体系
- **SSH认证策略**：支持密钥文件、代理转发、PKCS11等多种认证方式
- **密码管理**：加密存储和检索密码凭证
- **数据迁移**：处理旧版身份数据的JSON结构迁移和格式转换

### 2. 服务管理与控制
- **服务类型管理**：自定义服务、固定服务和映射服务的统一管理
- **服务组操作**：批量启停、状态刷新和层级关系维护
- **端口转发**：本地与远程端口映射配置
- **权限提升**：通过脚本实现服务控制时的权限管理

### 3. 脚本管理与执行
- **脚本层次管理**：通过`ScriptGroupStore`实现脚本组嵌套结构
- **生命周期控制**：从存储初始化到运行时执行的全流程管理
- **依赖处理**：循环引用检测和拓扑排序
- **多类型支持**：Shell脚本、初始化脚本、可执行文件等

### 4. 存储系统操作
- **基础操作**：启动、停止、暂停、重启等存储生命周期管理
- **批量处理**：支持对多个存储执行统一操作
- **异常容错**：无效存储状态下的操作处理
- **UI规范**：统一的Material Design图标和国际化

### 5. 文件系统管理
- **跨平台浏览**：Windows/Unix/macOS多平台文件操作
- **高级操作**：压缩解压、权限管理、批量命令执行
- **系统集成**：本地管理器打开、终端启动、路径复制
- **导航控制**：历史记录、多标签页、符号链接追踪

### 6. 桌面应用集成
- **应用配置**：主机、路径、启动参数的可视化配置
- **命令构建**：生成完整的可执行命令
- **存储管理**：桌面应用程序条目的创建与维护

该模块典型应用于：
- 需要统一认证管理的SSH客户端工具
- 服务治理和自动化运维平台
- 跨平台文件管理工具
- 脚本化任务执行环境
- 桌面应用启动器和管理系统


### 包内部结构视图

```mermaid
graph TD
    base --> identity
    base --> service
    base --> script
    base --> store
    base --> browser
    base --> desktop
    base --> action
    base --> SelfReferentialStore.java
    base --> GroupStore.java
    identity --> IdentityStore.java
    identity --> LocalIdentityConvertAction.java
    identity --> SshIdentityStrategy.java
    identity --> IdentityValue.java
    identity --> SyncedIdentityStoreProvider.java
    identity --> IdentityChoice.java
    identity --> SshIdentityStrategyHelper.java
    identity --> IdentityMigrationDeserializer.java
    identity --> LocalIdentityStoreProvider.java
    identity --> LocalIdentityStore.java
    identity --> SshIdentityStateManager.java
    identity --> IdentitySelectComp.java
    identity --> SyncedIdentityStore.java
    identity --> IdentityStoreProvider.java
    service --> CustomServiceStore.java
    service --> FixedServiceCreatorStore.java
    service --> MappedServiceStoreProvider.java
    service --> CustomServiceStoreProvider.java
    service --> AbstractServiceGroupStore.java
    service --> CustomServiceGroupStore.java
    service --> ServiceCopyAddressAction.java
    service --> AbstractServiceStoreProvider.java
    service --> ServiceRefreshAction.java
    service --> AbstractServiceGroupStoreProvider.java
    service --> FixedServiceGroupStore.java
    service --> FixedServiceStoreProvider.java
    service --> MappedServiceStore.java
    service --> AbstractServiceStore.java
    service --> FixedServiceGroupStoreProvider.java
    service --> FixedServiceStore.java
    service --> ServiceControlSession.java
    service --> ServiceProtocolType.java
    service --> ServiceControlStore.java
    service --> ServiceControlStoreProvider.java
    service --> CustomServiceGroupStoreProvider.java
    service --> ServiceProtocolTypeHelper.java
    script --> ScriptTargetType.java
    script --> ScriptGroupStore.java
    script --> ScriptDataStorageProvider.java
    script --> ScriptStoreSetup.java
    script --> SimpleScriptStoreProvider.java
    script --> ScriptStore.java
    script --> SimpleScriptQuickEditAction.java
    script --> SimpleScriptStore.java
    script --> RunScriptAction.java
    script --> PredefinedScriptStore.java
    script --> PredefinedScriptGroup.java
    script --> ScriptGroupStoreProvider.java
    script --> ScriptHierarchy.java
    store --> PauseableStore.java
    store --> StoppableStore.java
    store --> StorePauseAction.java
    store --> StartableStore.java
    store --> StoreStartAction.java
    store --> ShellStoreProvider.java
    store --> StoreStopAction.java
    store --> StoreRestartAction.java
    browser --> compress
    browser --> FileTypeAction.java
    browser --> ChmodAction.java
    browser --> CopyPathAction.java
    browser --> OpenDirectoryInNewTabAction.java
    browser --> OpenTerminalAction.java
    browser --> NewItemAction.java
    browser --> MultiExecuteSelectionAction.java
    browser --> BrowseInNativeManagerAction.java
    browser --> EditFileAction.java
    browser --> RefreshDirectoryAction.java
    browser --> ChgrpAction.java
    browser --> OpenFileDefaultAction.java
    browser --> DeleteAction.java
    browser --> ExecuteApplicationAction.java
    browser --> ChownAction.java
    browser --> CopyAction.java
    browser --> FollowLinkAction.java
    browser --> DownloadAction.java
    browser --> ForwardAction.java
    browser --> MultiExecuteAction.java
    browser --> JavaAction.java
    browser --> RenameAction.java
    browser --> RunAction.java
    browser --> JavapAction.java
    browser --> PasteAction.java
    browser --> ToFileCommandAction.java
    browser --> OpenFileWithAction.java
    browser --> JarAction.java
    browser --> BackAction.java
    browser --> DeleteLinkAction.java
    browser --> OpenNativeFileDetailsAction.java
    browser --> OpenDirectoryAction.java
    compress --> DirectoryCompressAction.java
    compress --> UnzipDirectoryUnixAction.java
    compress --> UnzipDirectoryWindowsAction.java
    compress --> FileCompressAction.java
    compress --> UntarGzHereAction.java
    compress --> BaseCompressAction.java
    compress --> UntarGzDirectoryAction.java
    compress --> UntarDirectoryAction.java
    compress --> BaseUnzipWindowsAction.java
    compress --> UntarHereAction.java
    compress --> BaseUnzipUnixAction.java
    compress --> BaseUntarAction.java
    compress --> UnzipHereWindowsAction.java
    compress --> UnzipHereUnixAction.java
    desktop --> DesktopApplicationStoreProvider.java
    desktop --> DesktopApplicationStore.java
    desktop --> DesktopBaseStore.java
    action --> LaunchStoreAction.java
    action --> CloneStoreAction.java
    action --> BrowseStoreAction.java
    action --> RunScriptActionMenu.java
    action --> ShareStoreAction.java
    action --> EditScriptStoreAction.java
    action --> EditStoreAction.java
    action --> SampleStoreAction.java
    action --> ScanStoreAction.java
    action --> RefreshChildrenStoreAction.java
    action --> XPipeUrlAction.java
    action --> ChangeStoreIconAction.java
```

该流程图展示了xpipe/ext/base模块的完整层级结构，从base根目录开始，向下展开为8个主要子模块：identity、service、script、store、browser、desktop、action以及两个独立文件。每个子模块又进一步细分为具体的实现类，其中browser模块包含compress压缩操作子模块。整个结构清晰地呈现了代码库的功能划分，包含身份管理、服务控制、脚本处理、存储操作、浏览器功能、桌面应用、动作执行等核心功能组件。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [xpipe](xpipe/_module.md) | package | 身份管理核心模块，含存储、验证策略、数据转换和GUI组件。服务框架管理存储、组和控制，支持自定义服务。脚本系统管理存储、执行和编辑，支持多Shell类型。存储基础功能提供启停暂停操作。文件浏览器支持跨平台操作。桌面应用管理配置和启动。数据存储操作框架支持多种功能。 |


