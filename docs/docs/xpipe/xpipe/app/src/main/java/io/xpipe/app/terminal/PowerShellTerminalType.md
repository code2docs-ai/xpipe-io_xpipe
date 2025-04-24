# 基础信息

|      |      |
|------|------|
| 名称 | PowerShellTerminalType |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/terminal/PowerShellTerminalType.java |
| 包名 | io.xpipe.app.terminal |
| 依赖项 | ['io.xpipe.app.ext.ProcessControlProvider', 'io.xpipe.core.process.CommandBuilder', 'io.xpipe.core.process.ShellDialects', 'java.nio.charset.StandardCharsets', 'java.util.Base64'] |
| 概述说明 | PowerShell终端类，不支持转义，新建窗口启动，根据脚本类型执行不同命令。 |

# 说明

PowerShellTerminalType类继承自ExternalTerminalType.SimplePathType并实现TrackableTerminalType接口。该类不支持转义字符，推荐设置为false，且不使用彩色标题。构造函数初始化名称为"app.powershell"和"powershell"。打开终端格式为NEW_WINDOW。根据当前本地方言是否为PowerShell调整进程层次偏移量。toCommand方法根据配置生成命令：若脚本方言为PowerShell则执行指定文件，否则生成Base64编码的UTF-16LE命令。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| PowerShellTerminalType | class | PowerShell终端类，不支持转义，新建窗口启动，执行策略Bypass，处理脚本或编码命令。 |



## 类 PowerShellTerminalType

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | PowerShellTerminalType |
| 说明 | PowerShell终端类，不支持转义，新建窗口启动，执行策略Bypass，处理脚本或编码命令。 |


### UML类图

```mermaid
classDiagram
    class ExternalTerminalType {
        <<abstract>>
    }
    
    class ExternalTerminalType.SimplePathType {
        <<abstract>>
    }
    
    class TrackableTerminalType {
        <<Interface>>
    }
    
    class PowerShellTerminalType {
        +PowerShellTerminalType()
        +boolean supportsEscapes()
        +TerminalOpenFormat getOpenFormat()
        +int getProcessHierarchyOffset()
        +boolean isRecommended()
        +boolean useColoredTitle()
        -CommandBuilder toCommand(TerminalLaunchConfiguration configuration)
    }
    
    ExternalTerminalType <|-- ExternalTerminalType.SimplePathType
    ExternalTerminalType.SimplePathType <|-- PowerShellTerminalType
    PowerShellTerminalType ..|> TrackableTerminalType
    
    // PowerShellTerminalType 继承自 ExternalTerminalType.SimplePathType
    // 并实现了 TrackableTerminalType 接口
    // 主要负责处理 PowerShell 终端类型的特定逻辑
```

这段代码展示了一个 PowerShell 终端类型类，它继承自抽象类 ExternalTerminalType.SimplePathType 并实现了 TrackableTerminalType 接口。该类封装了与 PowerShell 终端相关的各种行为，包括命令构建、进程层次偏移量计算以及终端格式设置等核心功能。通过重写父类方法，它提供了 PowerShell 特有的实现逻辑，如处理不同的脚本方言、设置执行策略以及编码命令等操作，体现了对 Windows PowerShell 环境的专门适配。


### 内部方法调用关系图

```mermaid
graph TD
    A["类PowerShellTerminalType"]
    B["继承: ExternalTerminalType.SimplePathType"]
    C["实现: TrackableTerminalType"]
    D["方法: boolean supportsEscapes()"]
    E["构造方法: PowerShellTerminalType()"]
    F["方法: TerminalOpenFormat getOpenFormat()"]
    G["方法: int getProcessHierarchyOffset()"]
    H["方法: boolean isRecommended()"]
    I["方法: boolean useColoredTitle()"]
    J["方法: CommandBuilder toCommand(TerminalLaunchConfiguration)"]
    K["条件分支: if (configuration.getScriptDialect().equals(ShellDialects.POWERSHELL))"]
    L["构建命令: CommandBuilder.of()"]
    M["Base64编码处理"]
    N["返回默认命令构造"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    J --> K
    K -->|是| L
    L -->|添加参数| "-ExecutionPolicy Bypass -File"
    K -->|否| M
    M -->|UTF_16LE编码| "Base64.getEncoder()"
    M -->|包装引号| "\"" + base64 + "\""
    M --> N
    N -->|添加参数| "-ExecutionPolicy Bypass -EncodedCommand"
```

这段代码流程图展示了PowerShellTerminalType类的完整结构，该类继承自ExternalTerminalType.SimplePathType并实现TrackableTerminalType接口。核心逻辑集中在toCommand方法，该方法根据脚本方言类型（PowerShell或其他）采用不同参数构建策略：对于PowerShell方言直接执行脚本文件，否则对命令进行Base64编码处理。流程图中清晰呈现了条件分支、字符串编码处理和两种命令构建路径，体现了终端配置的灵活处理机制。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getProcessHierarchyOffset | int | 方法判断当前Shell是否为PowerShell，是则返回-1，否则返回0。 |
| getOpenFormat | TerminalOpenFormat | 重写方法返回新窗口打开格式。 |
| supportsEscapes | boolean | Java方法重写，不支持转义字符。 |
| isRecommended | boolean | 重写方法isRecommended，固定返回false。 |
| useColoredTitle | boolean | 覆盖方法，返回false禁用彩色标题。 |
| toCommand | CommandBuilder | 根据脚本类型生成PowerShell命令，支持文件或编码执行。 |




