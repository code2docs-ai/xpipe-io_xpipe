# 基础信息

|      |      |
|------|------|
| 名称 | impl |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/beacon/impl |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.beacon.impl |
| 概述说明 | FsWriteExchangeImpl处理HTTP请求，管理Shell会话和文件传输。TerminalWaitExchangeImpl处理终端启动请求。ConnectionAddExchangeImpl管理连接添加和验证。ShellStopExchangeImpl关闭Shell会话。DaemonOpenExchangeImpl处理守护进程启动。DaemonFocusExchangeImpl切换至GUI模式。ConnectionToggleExchangeImpl管理连接状态切换。FsScriptExchangeImpl处理脚本执行。TerminalExternalLaunchExchangeImpl处理外部终端启动。DaemonStopExchangeImpl异步关闭守护进程。DaemonVersionExchangeImpl返回版本信息。CategoryAddExchangeImpl管理类目添加。ShellExecExchangeImpl执行Shell命令。FsBlobExchangeImpl处理文件存储。TerminalPrepareExchangeImpl准备终端信息。FsReadExchangeImpl读取文件。ConnectionRefreshExchangeImpl刷新连接。TerminalLaunchExchangeImpl启动终端。HandshakeExchangeImpl处理认证握手。AskpassExchangeImpl处理密码请求。ConnectionRemoveExchangeImpl删除连接。ConnectionTerminalExchangeImpl打开终端。ConnectionQueryExchangeImpl查询连接。DaemonStatusExchangeImpl返回守护状态。ShellStartExchangeImpl启动Shell会话。ConnectionInfoExchangeImpl返回连接信息。DaemonModeExchangeImpl切换守护模式。ConnectionBrowseExchangeImpl浏览文件系统。TerminalRegisterExchangeImpl注册终端进程。SshLaunchExchangeImpl处理SSH启动。 |

# 说明

```markdown
## 概述

该代码模块是一个基于HTTP交换的守护进程服务框架，主要提供终端管理、文件系统操作、连接管理、Shell会话控制等核心功能。模块通过多个Exchange实现类处理不同类型的HTTP请求，涉及会话管理、数据存储、权限验证、异常处理等机制。所有实现类均继承自特定基础Exchange类，遵循统一的请求-响应模式，部分功能需要与GUI界面交互。

## 主要业务场景

### 1. 终端管理
- **终端启动与注册**：通过`TerminalLaunchExchangeImpl`和`TerminalRegisterExchangeImpl`处理终端启动请求和进程注册
- **终端准备与等待**：`TerminalPrepareExchangeImpl`检查终端支持特性，`TerminalWaitExchangeImpl`处理等待逻辑
- **外部终端启动**：`TerminalExternalLaunchExchangeImpl`处理带权限验证的外部终端启动

### 2. 文件系统操作
- **文件读写**：`FsReadExchangeImpl`和`FsWriteExchangeImpl`分别处理文件读取和写入，支持大文件分块传输
- **脚本处理**：`FsScriptExchangeImpl`将请求数据转换为可执行脚本文件
- **二进制数据处理**：`FsBlobExchangeImpl`处理大文件和小文件的不同存储策略

### 3. 连接管理
- **连接增删改查**：
  - `ConnectionAddExchangeImpl`处理连接添加与验证
  - `ConnectionRemoveExchangeImpl`处理连接删除
  - `ConnectionRefreshExchangeImpl`处理连接刷新
  - `ConnectionQueryExchangeImpl`实现连接查询
- **连接信息获取**：`ConnectionInfoExchangeImpl`提供连接详细信息
- **连接终端操作**：`ConnectionTerminalExchangeImpl`处理连接终端会话
- **连接状态切换**：`ConnectionToggleExchangeImpl`管理连接启动/停止状态

### 4. Shell会话控制
- **会话启停**：`ShellStartExchangeImpl`和`ShellStopExchangeImpl`管理Shell会话生命周期
- **命令执行**：`ShellExecExchangeImpl`执行Shell命令并捕获输出
- **SSH启动**：`SshLaunchExchangeImpl`处理特定SSH命令

### 5. 守护进程管理
- **状态控制**：
  - `DaemonOpenExchangeImpl`处理守护进程打开请求
  - `DaemonStopExchangeImpl`异步停止守护进程
  - `DaemonStatusExchangeImpl`获取运行状态
  - `DaemonModeExchangeImpl`管理运行模式切换
- **版本信息**：`DaemonVersionExchangeImpl`提供版本信息查询
- **窗口聚焦**：`DaemonFocusExchangeImpl`切换至GUI模式并聚焦窗口

### 6. 认证与会话
- **握手认证**：`HandshakeExchangeImpl`处理初始认证和会话令牌生成
- **密码管理**：`AskpassExchangeImpl`处理密码请求和验证

### 7. 分类管理
- **分类操作**：`CategoryAddExchangeImpl`处理分类添加和验证

### 8. 浏览器集成
- **文件浏览**：`ConnectionBrowseExchangeImpl`打开文件系统浏览器会话
```


### 包内部结构视图

```mermaid
graph TD
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

该流程图展示了xpipe项目中beacon模块的实现类结构，所有实现类均位于impl目录下，包含30个不同的Exchange实现类，涉及文件操作、终端控制、连接管理、守护进程交互等功能模块。这些实现类共同构成了beacon模块的核心功能体系，每个类负责处理特定类型的交互请求。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [TerminalWaitExchangeImpl.java](TerminalWaitExchangeImpl.md) | file | 终端等待交换实现类，处理HTTP请求并返回响应，无需启用API。 |
| [ConnectionToggleExchangeImpl.java](ConnectionToggleExchangeImpl.md) | file | 处理连接切换请求，检查存储类型并控制会话启停。 |
| [DaemonFocusExchangeImpl.java](DaemonFocusExchangeImpl.md) | file | DaemonFocusExchangeImpl类处理HTTP请求，切换至GUI模式并聚焦主窗口。 |
| [DaemonOpenExchangeImpl.java](DaemonOpenExchangeImpl.md) | file | DaemonOpenExchangeImpl类处理HTTP请求，初始化平台并根据参数切换操作模式或处理应用启动参数。 |
| [ShellStopExchangeImpl.java](ShellStopExchangeImpl.md) | file | ShellStopExchangeImpl类处理关闭Shell会话并清理缓存。 |
| [ConnectionRefreshExchangeImpl.java](ConnectionRefreshExchangeImpl.md) | file | ConnectionRefreshExchangeImpl类处理连接刷新，验证或更新存储数据，同步对象为DataStorage。 |
| [FsReadExchangeImpl.java](FsReadExchangeImpl.md) | file | FsReadExchangeImpl类处理文件读取请求，检查文件存在性及大小，分大小传输文件内容。 |
| [TerminalPrepareExchangeImpl.java](TerminalPrepareExchangeImpl.md) | file | 终端处理类，检查终端类型支持Unicode和转义序列，返回响应配置。无需启用API。 |
| [FsBlobExchangeImpl.java](FsBlobExchangeImpl.md) | file | FsBlobExchangeImpl处理HTTP请求，存储大文件或小文件数据块，返回包含ID的响应。 |
| [ShellExecExchangeImpl.java](ShellExecExchangeImpl.md) | file | ShellExecExchangeImpl类处理HTTP请求，执行命令并返回输出、错误和退出码。 |
| [CategoryAddExchangeImpl.java](CategoryAddExchangeImpl.md) | file | 类处理添加分类逻辑，检查父类存在性及名称重复，返回新分类ID或现有ID。 |
| [DaemonVersionExchangeImpl.java](DaemonVersionExchangeImpl.md) | file | Daemon版本交换实现类，返回版本、构建、JVM及授权信息。 |
| [DaemonStopExchangeImpl.java](DaemonStopExchangeImpl.md) | file | DaemonStopExchangeImpl类实现守护进程停止功能，异步关闭操作模式，无需完成启动或启用API。 |
| [TerminalExternalLaunchExchangeImpl.java](TerminalExternalLaunchExchangeImpl.md) | file | 终端外部启动实现类，处理连接查询、权限检查及执行命令。 |
| [FsScriptExchangeImpl.java](FsScriptExchangeImpl.md) | file | FsScriptExchangeImpl类处理HTTP请求，执行脚本并返回结果路径。 |
| [DaemonModeExchangeImpl.java](DaemonModeExchangeImpl.md) | file | DaemonModeExchangeImpl处理HTTP请求，验证并切换操作模式，返回当前模式。无需启用API。 |
| [ConnectionInfoExchangeImpl.java](ConnectionInfoExchangeImpl.md) | file | 处理HTTP请求，获取连接信息并构建响应列表。 |
| [ShellStartExchangeImpl.java](ShellStartExchangeImpl.md) | file | ShellStartExchangeImpl处理HTTP请求，验证连接并管理Shell会话，返回控制信息和状态。 |
| [DaemonStatusExchangeImpl.java](DaemonStatusExchangeImpl.md) | file | DaemonStatusExchange实现类，返回操作模式，无需启动完成和API启用。 |
| [ConnectionQueryExchangeImpl.java](ConnectionQueryExchangeImpl.md) | file | Java类实现查询处理，返回过滤结果UUID列表，同步对象为DataStorage。 |
| [ConnectionTerminalExchangeImpl.java](ConnectionTerminalExchangeImpl.md) | file | 处理HTTP交换，验证连接并启动终端会话。同步对象为数据存储。 |
| [ConnectionRemoveExchangeImpl.java](ConnectionRemoveExchangeImpl.md) | file | 处理HTTP请求删除连接，验证并删除数据存储条目，返回空响应。同步对象为数据存储实例。 |
| [AskpassExchangeImpl.java](AskpassExchangeImpl.md) | file | AskpassExchangeImpl处理密码请求，验证秘密ID并返回响应，必要时聚焦终端。 |
| [HandshakeExchangeImpl.java](HandshakeExchangeImpl.md) | file | HandshakeExchangeImpl处理握手请求，验证本地或API密钥认证，成功则创建并返回会话令牌。 |
| [SshLaunchExchangeImpl.java](SshLaunchExchangeImpl.md) | file | SshLaunchExchangeImpl处理SSH请求，验证参数并返回响应，支持终端启动和命令执行。 |
| [TerminalRegisterExchangeImpl.java](TerminalRegisterExchangeImpl.md) | file | 终端注册交换实现类，处理请求并打开终端视图，注册进程ID，无需启用API。 |
| [ConnectionBrowseExchangeImpl.java](ConnectionBrowseExchangeImpl.md) | file | 处理HTTP请求，验证连接类型为文件系统后打开目录并返回响应。同步对象为DataStorage。 |
| [TerminalLaunchExchangeImpl.java](TerminalLaunchExchangeImpl.md) | file | 终端启动交换实现类，处理HTTP请求并返回目标文件响应，无需启用API。 |
| [ConnectionAddExchangeImpl.java](ConnectionAddExchangeImpl.md) | file | 处理HTTP请求，管理数据存储条目，验证并返回连接响应。 |
| [FsWriteExchangeImpl.java](FsWriteExchangeImpl.md) | file | FsWriteExchangeImpl类处理文件写入请求，通过BlobManager和ConnectionFileSystem实现数据传输。 |


