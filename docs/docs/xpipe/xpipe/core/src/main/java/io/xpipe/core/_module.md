# 基础信息

|      |      |
|------|------|
| 名称 | core |
| 编码语言 | .java |
| 代码路径 | xpipe/core/src/main/java/io/xpipe/core |
| 包名 | xpipe.core.src.main.java.io.xpipe.core |
| 概述说明 | XPipe核心模块：加密、序列化、异常处理、路径管理。  
对话框框架：构建交互式对话框，处理输入、类型转换。  
文件系统管理：跨平台文件操作、路径标准化、状态管理。  
终端处理：Shell控制、进程管理、命令构建。 |

# 说明

## 概述

该代码模块是XPipe核心功能集合，由多个子模块组成，共同提供基础工具、交互界面、存储管理和终端控制等核心能力。模块采用分层设计，底层提供加密安全、数据序列化等基础设施，上层构建对话框、文件系统、终端控制等业务功能。主要特点包括：

1. **安全体系**：完整的加密框架（AES/GCM）和敏感数据处理机制
2. **跨平台支持**：统一的文件系统抽象、路径标准化和Shell方言适配
3. **交互设计**：基于不可变对象的对话框框架，支持复杂用户输入流程
4. **状态管理**：通过多种状态类（`DataStoreState`、`ShellStoreState`等）实现配置持久化
5. **异常处理**：包含堆栈反混淆、验证异常等专业化处理机制

## 主要业务场景

1. **安全数据处理**：
   - 用户凭证加密存储（AES-128/GCM算法）
   - 敏感字段JSON序列化时的自动脱敏
   - 通过`SecretReference`建立安全数据引用链

2. **跨平台文件与存储管理**：
   - 统一路径处理（Windows/Unix格式转换）
   - 文件系统抽象（符号链接解析、元数据读取）
   - 网络隧道会话管理（多跳端口转发）

3. **交互式对话框流程**：
   - 组合式对话框构建（选择框/输入框/标题等元素）
   - 用户输入验证与类型转换（字符串到URI/布尔值等）
   - 条件对话流控制（动态跳过/重试逻辑）

4. **终端与Shell控制**：
   - 跨平台Shell命令执行（支持PowerShell等方言）
   - 进程生命周期管理（输入/输出流监控）
   - 终端初始化配置（清屏、环境检测）

5. **系统状态维护**：
   - 安装路径管理（开发/生产环境区分）
   - 数据状态合并与冲突解决（`useNewer`策略）
   - Shell环境状态持久化

6. **开发支持**：
   - 异常堆栈反混淆（生产环境调试）
   - 桩实现（`StubShellControl`测试支持）
   - 统一序列化配置（Jackson定制化模块）

各子模块通过标准化接口协同工作，如`Session`管理资源生命周期、`DialogElement`构建用户交互、`FileSystem`抽象文件操作，共同支撑XPipe核心业务场景的可靠运行。


### 包内部结构视图

```mermaid
graph TD
    core --> util
    core --> dialog
    core --> store
    core --> process
    util --> AesSecretValue.java
    util --> FailableBiFunction.java
    util --> FailableFunction.java
    util --> SecretReference.java
    util --> FailableBiConsumer.java
    util --> ModuleLayerLoader.java
    util --> SecretValue.java
    util --> JacksonExtension.java
    util --> ValidationException.java
    util --> FailableRunnable.java
    util --> Deobfuscator.java
    util --> Identifiers.java
    util --> XPipeInstallation.java
    util --> InPlaceSecretValue.java
    util --> JacksonMapper.java
    util --> XPipeDaemonMode.java
    util --> DataStateProvider.java
    util --> CoreJacksonModule.java
    util --> StreamCharset.java
    util --> FailableSupplier.java
    util --> NewLine.java
    util --> FailableConsumer.java
    util --> EncryptedSecretValue.java
    util --> UuidHelper.java
    dialog --> DialogReference.java
    dialog --> BusyElement.java
    dialog --> HeaderElement.java
    dialog --> QueryElement.java
    dialog --> Choice.java
    dialog --> DialogMapper.java
    dialog --> BaseQueryElement.java
    dialog --> DialogElement.java
    dialog --> DialogCancelException.java
    dialog --> QueryConverter.java
    dialog --> Dialog.java
    dialog --> ChoiceElement.java
    store --> FileSystem.java
    store --> FileEntry.java
    store --> DataStoreState.java
    store --> InternalCacheDataStore.java
    store --> FileSystemStore.java
    store --> StatefulDataStore.java
    store --> FilePath.java
    store --> LinkFileEntry.java
    store --> FileInfo.java
    store --> FileKind.java
    store --> NetworkTunnelStore.java
    store --> SingletonSessionStore.java
    store --> SessionListener.java
    store --> FixedChildStore.java
    store --> EnabledStoreState.java
    store --> DataStore.java
    store --> FileNames.java
    store --> NetworkTunnelSession.java
    store --> Session.java
    store --> ValidatableStore.java
    store --> ExpandedLifecycleStore.java
    store --> NetworkTunnelSessionChain.java
    store --> StorePath.java
    process --> TerminalInitScriptConfig.java
    process --> CommandControl.java
    process --> ShellDumbMode.java
    process --> LocalProcessInputStream.java
    process --> CommandBuilder.java
    process --> PropertiesFormatsParser.java
    process --> CommandConfiguration.java
    process --> ShellStoreState.java
    process --> ShellOpenFunction.java
    process --> ElevationHandler.java
    process --> ShellDialects.java
    process --> ParentSystemAccess.java
    process --> LocalProcessOutputStream.java
    process --> StubShellControl.java
    process --> ShellView.java
    process --> TerminalLaunchCommandFunction.java
    process --> TerminalInitFunction.java
    process --> ElevationFunction.java
    process --> OsType.java
    process --> ShellTerminalInitCommand.java
    process --> ShellSecurityPolicy.java
    process --> ProcessControl.java
    process --> ProcessOutputException.java
    process --> SystemState.java
    process --> ShellCapabilities.java
    process --> WrapperShellControl.java
    process --> CountDown.java
    process --> ShellScript.java
    process --> WorkingDirectoryFunction.java
    process --> ShellTtyState.java
    process --> ShellDialect.java
    process --> ShellEnvironmentStoreState.java
    process --> ShellLaunchCommand.java
    process --> ShellControl.java
    process --> ShellDialectAskpass.java
    process --> ShellSpawnException.java
```

该流程图展示了xpipe-core项目的模块结构，包含util、dialog、store和process四个主要子模块。其中util模块包含加密工具、函数式接口工具等26个文件；dialog模块处理对话框相关逻辑，包含12个文件；store模块管理数据存储，包含23个文件；process模块处理系统进程，包含31个文件。整个结构清晰地反映了项目的功能划分和层级关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [store](store/_module.md) | package | FileEntry类表示文件系统条目，含路径、日期、大小等属性。DataStoreState是抽象基类，支持构建器模式。FilePath处理路径操作，支持跨平台。LinkFileEntry表示链接文件，含目标条目。EnabledStoreState继承DataStoreState，管理启用状态。FileNames提供路径处理静态方法。NetworkTunnelSession是抽象类，定义端口和Shell控制方法。Session是抽象基类，管理监听器和运行状态。NetworkTunnelSessionChain管理多个会话链。StorePath表示存储路径，支持创建和验证。 |
| [process](process/_module.md) | package | TerminalInitScriptConfig类配置终端初始化脚本，含显示名、清屏控制和终端命令。 |
| [dialog](dialog/_module.md) | package | DialogReference不可变类含dialogId和start。BusyElement表忙碌状态。HeaderElement实现对话框头部。QueryElement处理查询转换验证。Choice类表示可选项。DialogMapper映射对话框元素。BaseQueryElement处理查询操作。DialogElement为抽象基类。DialogCancelException处理取消异常。QueryConverter实现类型转换。Dialog管理对话流程。ChoiceElement处理选择元素。 |
| [util](util/_module.md) | package | AesSecretValue类实现AES加密解密，使用GCM算法128位标签。SecretReference封装秘密ID引用。ValidationException处理验证异常。Deobfuscator反混淆堆栈信息。Identifiers处理字符串组合。XPipeInstallation管理软件安装路径。InPlaceSecretValue生成AES密钥。JacksonMapper配置JSON处理。DataStateProvider管理数据状态。CoreJacksonModule注册序列化器。StreamCharset处理字符集。EncryptedSecretValue抽象类处理加密数据。UuidHelper解析UUID。 |


