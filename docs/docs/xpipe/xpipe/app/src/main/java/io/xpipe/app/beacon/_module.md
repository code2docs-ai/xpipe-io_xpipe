# 基础信息

|      |      |
|------|------|
| 名称 | beacon |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/beacon |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.beacon |
| 概述说明 | HTTP守护进程框架，提供终端管理、文件操作、连接控制、Shell会话等功能，支持多种Exchange实现类处理请求。 |

# 说明

```markdown
## 概述

该代码模块是一个基于HTTP的守护进程服务框架，主要用于实现终端管理、文件系统操作、连接管理、Shell会话控制等核心功能。模块采用单例模式设计，通过AppBeaconServer类管理本地HTTP信标服务器，支持多线程处理各类HTTP请求。核心组件包括会话管理(BeaconSession)、二进制数据存储(BlobManager)、Shell会话缓存(AppBeaconCache)等，所有请求处理均通过统一的BeaconRequestHandler进行路由和验证。

## 主要业务场景

### 1. HTTP信标服务管理
- **服务器生命周期**：通过`AppBeaconServer`实现服务器的启动、停止和状态管理
- **请求处理**：`BeaconRequestHandler`统一处理HTTP请求，包括认证、错误处理和响应生成
- **会话管理**：`BeaconSession`维护客户端信息和会话令牌

### 2. 终端会话管理
- **Shell会话控制**：`BeaconShellSession`封装Shell会话数据和操作接口
- **会话缓存**：`AppBeaconCache`通过UUID管理活跃的Shell会话

### 3. 二进制数据存储
- **Blob管理**：`BlobManager`提供内存和文件系统两种存储方式
  - 内存存储使用ConcurrentHashMap
  - 文件存储使用临时目录下的UUID命名文件
- **数据存取**：支持通过UUID获取Blob输入流，实现高效数据检索

### 4. 请求处理流程
- **认证验证**：支持Bearer令牌验证和API状态检查
- **数据解析**：处理原始数据和JSON格式的请求体
- **同步处理**：实现请求的同步处理和响应生成
- **错误处理**：包含详细的错误日志记录和事件跟踪机制

### 5. 系统集成
- **配置管理**：支持通过系统属性配置服务器端口
- **临时文件管理**：自动创建和清理临时目录
- **异常处理**：记录错误事件但保持程序持续运行
```


### 包内部结构视图

```mermaid
graph TD
    beacon --> impl
    beacon --> AppBeaconServer.java
    beacon --> BeaconShellSession.java
    beacon --> BlobManager.java
    beacon --> AppBeaconCache.java
    beacon --> BeaconRequestHandler.java
    beacon --> BeaconSession.java
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
```

该流程图展示了beacon模块的层级结构，包含一个impl子目录和多个直接位于beacon目录下的文件。impl子目录下包含28个具体的实现类文件，这些文件可能对应不同的功能接口实现。顶层beacon目录则包含6个核心类文件，涉及服务器、会话管理、缓存处理等基础功能组件。整个结构清晰地反映了模块化设计思想，将核心功能与具体实现分离。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [BeaconRequestHandler.java](BeaconRequestHandler.md) | file | Beacon请求处理器，处理HTTP请求，验证权限并返回响应。 |
| [AppBeaconCache.java](AppBeaconCache.md) | file | AppBeaconCache类管理BeaconShellSession集合，提供按UUID查找会话功能，找不到时抛出异常。 |
| [BlobManager.java](BlobManager.md) | file | BlobManager管理内存和文件二进制数据，提供存储和读取功能。 |
| [BeaconShellSession.java](BeaconShellSession.md) | file | BeaconShellSession类包含DataStoreEntry和ShellControl两个成员变量。 |
| [AppBeaconServer.java](AppBeaconServer.md) | file | AppBeaconServer类管理HTTP服务器，处理端口设置、会话和认证，支持启动、停止和重置操作。 |
| [BeaconSession.java](BeaconSession.md) | file | BeaconSession类包含客户端信息和令牌字段。 |
| [impl](impl/_module.md) | package | FsWriteExchangeImpl处理HTTP请求，管理Shell会话和文件传输。TerminalWaitExchangeImpl处理终端启动请求。ConnectionAddExchangeImpl管理连接添加和验证。ShellStopExchangeImpl关闭Shell会话。DaemonOpenExchangeImpl处理守护进程启动。DaemonFocusExchangeImpl切换至GUI模式。ConnectionToggleExchangeImpl管理连接状态切换。FsScriptExchangeImpl处理脚本执行。TerminalExternalLaunchExchangeImpl处理外部终端启动。DaemonStopExchangeImpl异步关闭守护进程。DaemonVersionExchangeImpl返回版本信息。CategoryAddExchangeImpl管理类目添加。ShellExecExchangeImpl执行Shell命令。FsBlobExchangeImpl处理文件存储。TerminalPrepareExchangeImpl准备终端信息。FsReadExchangeImpl读取文件。ConnectionRefreshExchangeImpl刷新连接。TerminalLaunchExchangeImpl启动终端。HandshakeExchangeImpl处理认证握手。AskpassExchangeImpl处理密码请求。ConnectionRemoveExchangeImpl删除连接。ConnectionTerminalExchangeImpl打开终端。ConnectionQueryExchangeImpl查询连接。DaemonStatusExchangeImpl返回守护状态。ShellStartExchangeImpl启动Shell会话。ConnectionInfoExchangeImpl返回连接信息。DaemonModeExchangeImpl切换守护模式。ConnectionBrowseExchangeImpl浏览文件系统。TerminalRegisterExchangeImpl注册终端进程。SshLaunchExchangeImpl处理SSH启动。 |


