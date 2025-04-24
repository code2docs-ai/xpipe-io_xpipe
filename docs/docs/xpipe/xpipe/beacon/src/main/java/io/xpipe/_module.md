# 基础信息

|      |      |
|------|------|
| 名称 | xpipe |
| 编码语言 | .java |
| 代码路径 | xpipe/beacon/src/main/java/io/xpipe |
| 包名 | xpipe.beacon.src.main.java.io.xpipe |
| 概述说明 | 基于Beacon接口的Java API服务模块，处理连接、文件、终端等系统交互，含多种异常类和配置管理。 |

# 说明

```markdown
## 概述

该代码模块是一个基于Beacon接口的API服务系统，采用Java实现，提供了一套完整的客户端-服务端交互框架。模块核心围绕`BeaconInterface`接口构建，包含多个实现类分别处理不同类型的业务操作。主要特点包括：

1. **架构设计**：采用清晰的接口契约模式，通过定义请求路径和数据结构实现类型安全的交互
2. **技术实现**：
   - 使用Lombok注解（`@Value`、`@Builder`、`@Jacksonized`）简化代码并确保不可变性
   - 支持JSON序列化/反序列化（通过Jackson模块）
   - 提供完善的异常处理体系（5种自定义异常类）
3. **功能范围**：覆盖连接管理、文件操作、终端控制等系统级交互场景

## 主要业务场景

### 核心功能组件
1. **客户端/服务端通信**
   - `BeaconClient`：管理HTTP连接，处理请求/响应序列化
   - `BeaconServer`：守护进程管理，支持调试模式启动
   - 错误处理：`BeaconClientErrorResponse`/`BeaconServerErrorResponse`

2. **配置管理**
   - `BeaconConfig`：集中管理端口号、调试模式等系统配置
   - `BeaconAuthMethod`：认证方式管理（Local/ApiKey）

3. **序列化支持**
   - `BeaconJacksonModule`：注册多态类型处理
   - `BeaconClientInformation`：客户端标识的多态序列化

### 业务操作场景
1. **连接生命周期管理**
   - 全流程控制：从创建(`ConnectionAddExchange`)到销毁(`ConnectionRemoveExchange`)
   - 状态管理：刷新/切换状态/终端交互等专用交换类

2. **文件系统操作**
   - 基础IO：读写操作(`FsReadExchange`/`FsWriteExchange`)
   - 高级处理：脚本执行(`FsScriptExchange`)和二进制数据处理(`FsBlobExchange`)

3. **终端控制**
   - 本地终端：启动/注册/准备全流程
   - 外部终端：专用启动接口(`TerminalExternalLaunchExchange`)

4. **系统管理**
   - 守护进程控制：状态查询/模式切换/版本管理
   - 安全交互：认证握手(`HandshakeExchange`)、密码处理(`AskpassExchange`)

### 异常处理体系
| 异常类型 | 应用场景 |
|---------|---------|
| `BeaconClientException` | 客户端操作错误 |
| `BeaconServerException` | 服务端内部错误 |
| `BeaconConnectorException` | 连接相关故障 |

模块通过严格的接口定义和类型安全的交互模式，为复杂的系统管理操作提供了可靠的基础设施支持。
```


### 包内部结构视图

```mermaid
graph TD
    xpipe --> beacon
    beacon --> api
    beacon --> BeaconClientException.java
    beacon --> BeaconServerException.java
    beacon --> BeaconAuthMethod.java
    beacon --> BeaconConfig.java
    beacon --> BeaconConnectorException.java
    beacon --> BeaconJacksonModule.java
    beacon --> BeaconInterface.java
    beacon --> BeaconClientInformation.java
    beacon --> BeaconServer.java
    beacon --> BeaconClientErrorResponse.java
    beacon --> BeaconClient.java
    beacon --> BeaconServerErrorResponse.java
    api --> CategoryAddExchange.java
    api --> ConnectionInfoExchange.java
    api --> FsReadExchange.java
    api --> TerminalLaunchExchange.java
    api --> TerminalWaitExchange.java
    api --> ConnectionAddExchange.java
    api --> ConnectionBrowseExchange.java
    api --> DaemonFocusExchange.java
    api --> ShellStartExchange.java
    api --> ConnectionRefreshExchange.java
    api --> AskpassExchange.java
    api --> SshLaunchExchange.java
    api --> ShellStopExchange.java
    api --> TerminalExternalLaunchExchange.java
    api --> TerminalRegisterExchange.java
    api --> FsBlobExchange.java
    api --> ConnectionToggleExchange.java
    api --> TerminalPrepareExchange.java
    api --> DaemonOpenExchange.java
    api --> DaemonModeExchange.java
    api --> HandshakeExchange.java
    api --> ConnectionRemoveExchange.java
    api --> DaemonStatusExchange.java
    api --> ConnectionTerminalExchange.java
    api --> ShellExecExchange.java
    api --> FsScriptExchange.java
    api --> FsWriteExchange.java
    api --> DaemonVersionExchange.java
    api --> ConnectionQueryExchange.java
    api --> DaemonStopExchange.java
```

该流程图展示了xpipe/beacon模块的完整层级结构，其中beacon作为根目录包含api子目录和多个客户端/服务端相关类文件，api目录下则集中了30个不同类型的Exchange接口类。整个结构清晰地分为核心功能类与API接口两大分支，体现了模块化设计思想。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [beacon](beacon/_module.md) | package | 基于Beacon接口的Java API服务模块，处理连接、文件、终端等系统交互，含多种异常类和配置管理。 |


