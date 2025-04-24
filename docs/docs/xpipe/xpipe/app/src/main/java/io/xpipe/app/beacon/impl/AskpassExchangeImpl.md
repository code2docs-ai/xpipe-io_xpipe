# 基础信息

|      |      |
|------|------|
| 名称 | AskpassExchangeImpl |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/beacon/impl/AskpassExchangeImpl.java |
| 包名 | io.xpipe.app.beacon.impl |
| 依赖项 | ['io.xpipe.app.terminal.TerminalView', 'io.xpipe.app.util.AskpassAlert', 'io.xpipe.app.util.SecretManager', 'io.xpipe.app.util.SecretQueryState', 'io.xpipe.beacon.BeaconClientException', 'io.xpipe.beacon.api.AskpassExchange', 'com.sun.net.httpserver.HttpExchange'] |
| 概述说明 | AskpassExchangeImpl处理密码请求，验证秘密ID并返回响应，必要时聚焦终端。 |

# 说明

AskpassExchangeImpl类继承自AskpassExchange，实现了密码请求处理逻辑。主要功能包括：处理HTTP交换请求，若请求为空则直接查询原始密码；否则通过SecretManager获取密码进度，验证状态后返回处理结果。包含终端聚焦辅助方法，根据进程ID定位并激活对应终端窗口。类重写方法表明无需等待启动完成或启用API即可运行。异常处理涵盖未知请求和密码查询状态错误情况。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AskpassExchangeImpl | class | AskpassExchangeImpl处理密码请求，验证密钥状态并返回响应，必要时聚焦终端。 |



## 类 AskpassExchangeImpl

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AskpassExchangeImpl |
| 说明 | AskpassExchangeImpl处理密码请求，验证密钥状态并返回响应，必要时聚焦终端。 |


### UML类图

```mermaid
classDiagram
    class AskpassExchange {
        <<Interface>>
        +requiresCompletedStartup() boolean
        +handle(HttpExchange exchange, Request msg) Object
        +requiresEnabledApi() boolean
    }

    class AskpassExchangeImpl {
        +handle(HttpExchange exchange, Request msg) Object
        -focusTerminalIfNeeded(long pid) void
        +requiresCompletedStartup() boolean
        +requiresEnabledApi() boolean
    }

    class SecretManager {
        <<Static>>
        +getProgress(Request request) Optional~SecretProgress~
        +getProgress(Request request, String secretId) Optional~SecretProgress~
    }

    class TerminalView {
        <<Static>>
        +get() TerminalView
        +findSession(long pid) Optional~TerminalSession~
        +getTerminalInstances() Collection~TerminalInstance~
        +focus(TerminalInstance instance) void
    }

    AskpassExchangeImpl --|> AskpassExchange : 实现
    AskpassExchangeImpl --> SecretManager : 调用
    AskpassExchangeImpl --> TerminalView : 调用

    class SecretProgress {
        +process(String prompt) Secret
        +getState() SecretQueryState
    }

    class SecretQueryState {
        <<Enum>>
        NORMAL
        +toErrorMessage(SecretQueryState state) String
    }

    class Response {
        +builder() Builder
    }
    class Response.Builder {
        +value(Object value) Builder
        +build() Response
    }
```

这段代码展示了一个实现`AskpassExchange`接口的`AskpassExchangeImpl`类，主要处理密码请求和终端聚焦逻辑。类图清晰地呈现了核心类之间的关系：`AskpassExchangeImpl`通过`SecretManager`查询密码状态，使用`TerminalView`管理终端会话，并依赖`SecretProgress`和`SecretQueryState`枚举处理密码状态转换。整个设计体现了职责分离，接口实现类专注于业务逻辑，静态工具类提供辅助功能。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AskpassExchangeImpl"]
    B["重写方法: boolean requiresCompletedStartup()"]
    C["重写方法: Object handle(HttpExchange, Request)"]
    D["私有方法: void focusTerminalIfNeeded(long)"]
    E["重写方法: boolean requiresEnabledApi()"]
    F["条件分支: msg.getRequest() == null"]
    G["调用: AskpassAlert.queryRaw"]
    H["构建响应: Response.builder().value()"]
    I["条件分支: msg.getSecretId() != null"]
    J["调用: SecretManager.getProgress"]
    K["异常处理: BeaconClientException"]
    L["调用: p.process"]
    M["状态检查: p.getState() != NORMAL"]
    N["调用: focusTerminalIfNeeded"]
    O["构建响应: Response.builder().value()"]
    P["条件分支: TerminalView.get() == null"]
    Q["调用: TerminalView.findSession"]
    R["流处理: filter+findFirst"]
    S["调用: TerminalView.focus"]

    A --> B
    A --> C
    A --> D
    A --> E
    C --> F
    F --是--> G --> H
    F --否--> I
    I --是--> J
    I --否--> J
    J --> K
    J --> L --> M
    M --异常--> K
    M --正常--> N --> O
    D --> P
    P --否--> Q --> R --> S
```

流程图描述：该流程图描述了AskpassExchangeImpl类的核心逻辑流程，主要包括handle请求处理方法的分支决策链。当请求无内容时直接返回密码查询结果，否则通过SecretManager处理密钥状态，异常时抛出错误，正常时聚焦终端窗口并返回处理结果。focusTerminalIfNeeded方法实现了基于PID的终端窗口查找和聚焦逻辑，包含多层空值检查和流式过滤操作。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| handle | Object | 处理HTTP请求，检查请求和密钥状态，返回响应或异常。 |
| requiresCompletedStartup | boolean | 重写方法，启动完成前可执行。 |
| focusTerminalIfNeeded | void | 检查并聚焦指定PID的终端会话。 |
| requiresEnabledApi | boolean | 重写方法，返回false表示无需启用API。 |




