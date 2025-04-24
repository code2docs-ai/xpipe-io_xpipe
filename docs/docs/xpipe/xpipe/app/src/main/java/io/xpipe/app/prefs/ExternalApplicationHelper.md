# 基础信息

|      |      |
|------|------|
| 名称 | ExternalApplicationHelper |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/prefs/ExternalApplicationHelper.java |
| 包名 | io.xpipe.app.prefs |
| 依赖项 | ['io.xpipe.app.issue.TrackEvent', 'io.xpipe.app.util.LocalShell', 'io.xpipe.core.process.CommandBuilder', 'java.util.Arrays', 'java.util.Locale', 'java.util.stream.Collectors'] |
| 概述说明 | 替换变量并启动异步命令的工具类。 |

# 说明

ExternalApplicationHelper类提供两个核心功能：replaceVariableArgument方法用于替换字符串中的变量参数，支持大小写转换和引号处理；startAsync方法用于异步执行外部命令，支持解析带引号的命令路径和参数，并通过CommandBuilder构建最终命令。方法内部使用LocalShell执行命令，并记录调试事件。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ExternalApplicationHelper | class | 替换变量并异步执行命令的工具类。 |



## 类 ExternalApplicationHelper

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ExternalApplicationHelper |
| 说明 | 替换变量并异步执行命令的工具类。 |


### UML类图

```mermaid
classDiagram
    class ExternalApplicationHelper {
        <<static>>
        +replaceVariableArgument(String format, String variable, String value) String
        +startAsync(String raw) void
        +startAsync(CommandBuilder b) void
    }

    class CommandBuilder {
        <<static>>
        +of() CommandBuilder
        +addFile(String file) CommandBuilder
        +add(String args) CommandBuilder
        +buildFull(ShellContext sc) String
    }

    class LocalShell {
        <<static>>
        +getShell() ShellContext
    }

    class ShellContext {
        +start() ShellContext
        +getShellDialect() ShellDialect
        +command(CommandBuilder cmd) CommandExecutor
    }

    class ShellDialect {
        <<Interface>>
        +launchAsnyc(CommandBuilder b) CommandBuilder
    }

    class CommandExecutor {
        +start() CommandExecutor
        +discardOrThrow() void
    }

    class TrackEvent {
        <<static>>
        +withDebug(String message) TrackEvent
        +tag(String key, String value) TrackEvent
        +handle() void
    }

    ExternalApplicationHelper --> CommandBuilder : 使用
    ExternalApplicationHelper --> LocalShell : 依赖
    ExternalApplicationHelper --> TrackEvent : 使用
    LocalShell --> ShellContext : 返回
    ShellContext --> ShellDialect : 调用
    ShellContext --> CommandExecutor : 创建
    CommandBuilder --> ShellContext : 依赖
```

这段代码展示了一个外部应用助手类，主要提供变量替换和异步启动外部程序的功能。类图清晰地展示了核心类之间的关系：ExternalApplicationHelper通过CommandBuilder构造命令，依赖LocalShell获取ShellContext来执行命令，使用TrackEvent记录调试信息。ShellContext负责与底层ShellDialect交互并创建CommandExecutor执行命令。整个设计体现了分层和职责分离的思想，静态方法的使用简化了调用方式。


### 内部方法调用关系图

```mermaid
graph TD
    A["类ExternalApplicationHelper"]
    B["静态方法: replaceVariableArgument"]
    C["步骤: 变量标准化处理"]
    D["步骤: 处理含空格的值"]
    E["步骤: 替换变量占位符"]
    F["静态方法: startAsync(String raw)"]
    G["步骤: 空值检查"]
    H["步骤: 参数分割处理"]
    I["分支: 带引号参数解析"]
    J["分支: 普通参数解析"]
    K["调用: startAsync(CommandBuilder)"]
    L["静态方法: startAsync(CommandBuilder)"]
    M["步骤: 获取Shell实例"]
    N["步骤: 构建异步命令"]
    O["步骤: 事件跟踪"]
    P["步骤: 执行命令并处理结果"]

    A --> B
    B --> C["变量转大写"]
    B --> D["添加值引号"]
    B --> E["双重替换逻辑"]
    A --> F
    F --> G["检查raw==null"]
    F --> H["分割参数"]
    F --> I["提取带引号命令"]
    F --> J["提取普通命令"]
    F --> K["转CommandBuilder调用"]
    A --> L
    L --> M["获取LocalShell"]
    L --> N["构建异步命令"]
    L --> O["记录调试事件"]
    L --> P["执行并丢弃输出"]
```

```mermaid
sequenceDiagram
    participant Caller
    participant ExternalApplicationHelper
    participant LocalShell
    participant CommandBuilder
    participant TrackEvent

    Caller->>ExternalApplicationHelper: replaceVariableArgument(format,var,val)
    ExternalApplicationHelper->>ExternalApplicationHelper: 变量标准化处理
    ExternalApplicationHelper->>ExternalApplicationHelper: 值引号处理
    ExternalApplicationHelper-->>Caller: 返回替换后字符串

    Caller->>ExternalApplicationHelper: startAsync(raw)
    alt 空值检查
        ExternalApplicationHelper-->>Caller: 直接返回
    else 参数解析
        ExternalApplicationHelper->>CommandBuilder: 创建并填充参数
        ExternalApplicationHelper->>ExternalApplicationHelper: startAsync(builder)
    end

    ExternalApplicationHelper->>LocalShell: 获取Shell实例
    LocalShell-->>ExternalApplicationHelper: shell实例
    ExternalApplicationHelper->>LocalShell: 构建异步命令
    ExternalApplicationHelper->>TrackEvent: 记录执行事件
    ExternalApplicationHelper->>LocalShell: 执行命令
    LocalShell-->>ExternalApplicationHelper: 执行结果
```

该流程图展示了ExternalApplicationHelper类的三个核心方法调用链。replaceVariableArgument方法处理字符串模板中的变量替换，包含大小写标准化和引号处理逻辑；startAsync(String)方法实现命令行参数解析，区分带引号和普通参数两种情况；startAsync(CommandBuilder)方法通过LocalShell执行异步命令，包含完整的命令构建、事件跟踪和执行结果处理流程。时序图则详细描述了跨组件的交互过程，特别是与LocalShell和CommandBuilder的协作关系。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| startAsync | void | 静态方法startAsync处理字符串输入，解析命令和参数后异步执行。 |
| replaceVariableArgument | String | 替换字符串中的变量参数，处理大小写和引号。 |
| startAsync | void | 异步启动本地命令，跟踪执行事件，捕获异常。 |




