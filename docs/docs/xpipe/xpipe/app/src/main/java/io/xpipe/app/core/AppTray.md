# 基础信息

|      |      |
|------|------|
| 名称 | AppTray |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/AppTray.java |
| 包名 | io.xpipe.app.core |
| 依赖项 | ['io.xpipe.app.issue.ErrorEvent', 'io.xpipe.app.issue.ErrorHandler', 'javafx.application.Platform', 'lombok.Getter', 'lombok.SneakyThrows', 'java.awt', 'java.time.Duration', 'java.time.Instant'] |
| 概述说明 | AppTray类实现系统托盘图标管理，包含错误处理和显示控制功能。 |

# 说明

该代码定义了一个单例类AppTray，用于管理系统托盘图标和错误处理。类中包含私有静态实例INSTANCE、托盘图标icon和错误处理器errorHandler。构造函数初始化这两个成员，其中错误处理器使用内部类TrayErrorHandler实现。提供静态方法init初始化实例，get获取实例。show和hide方法控制图标显示隐藏，会检查系统托盘支持。TrayErrorHandler处理错误事件，过滤已忽略错误，生成错误标题和描述，限制10秒内不重复显示，最终通过托盘图标展示错误信息。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppTray | class | AppTray单例类，管理托盘图标和错误处理，支持显示/隐藏及错误提示。 |



## 类 AppTray

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppTray |
| 说明 | AppTray单例类，管理托盘图标和错误处理，支持显示/隐藏及错误提示。 |


### UML类图

```mermaid
classDiagram
    class AppTray {
        -static AppTray INSTANCE
        -AppTrayIcon icon
        +ErrorHandler errorHandler
        -AppTray()
        +static void init()
        +static AppTray get()
        +void show()
        +void hide()
    }

    class AppTrayIcon {
        +void show()
        +void hide()
        +void showErrorMessage(String title, String desc)
    }

    class ErrorHandler {
        <<Interface>>
        +void handle(ErrorEvent event)
    }

    class TrayErrorHandler {
        -Instant lastErrorShown
        +void handle(ErrorEvent event)
    }

    AppTray --> AppTrayIcon : 包含
    AppTray --> TrayErrorHandler : 包含
    TrayErrorHandler ..|> ErrorHandler : 实现
```

```mermaid
flowchart TD
    A["AppTray.init()"] --> B["创建AppTray实例"]
    B --> C["初始化AppTrayIcon"]
    B --> D["初始化TrayErrorHandler"]
    E["AppTray.get()"] --> F["返回INSTANCE"]
    G["AppTray.show()"] --> H{"SystemTray是否支持?"}
    H -->|是| I["调用icon.show()"]
    H -->|否| J["直接返回"]
    K["TrayErrorHandler.handle()"] --> L{"错误是否被忽略?"}
    L -->|是| M["直接返回"]
    L -->|否| N["准备错误信息"]
    N --> O{"距离上次显示\n是否超过10秒?"}
    O -->|是| P["更新lastErrorShown\n调用icon.showErrorMessage()"]
    O -->|否| Q["直接返回"]
```

这段代码实现了一个系统托盘应用的单例管理类，包含错误处理功能。AppTray通过静态方法提供单例访问，内部维护AppTrayIcon用于托盘图标显示，以及TrayErrorHandler实现ErrorHandler接口处理错误事件。流程图展示了初始化、获取实例、显示托盘和错误处理的完整流程，特别注意了错误显示的频率控制（10秒间隔）和系统托盘支持的运行时检查。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AppTray"]
    B["静态属性: AppTray INSTANCE"]
    C["属性: AppTrayIcon icon"]
    D["属性: ErrorHandler errorHandler"]
    E["私有构造方法: AppTray()"]
    F["静态方法: init()"]
    G["静态方法: get()"]
    H["方法: show()"]
    I["方法: hide()"]
    J["内部类: TrayErrorHandler"]
    K["内部属性: Instant lastErrorShown"]
    L["内部方法: handle(ErrorEvent event)"]
    M["检查: SystemTray.isSupported()"]
    N["调用: icon.show()"]
    O["调用: icon.hide()"]
    P["调用: icon.showErrorMessage(title, finalDesc)"]

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
    J --> L
    H --> M
    M --"true"--> N
    I --> O
    L --> P
```

```mermaid
sequenceDiagram
    participant A as Client
    participant B as AppTray
    participant C as AppTrayIcon
    participant D as TrayErrorHandler

    A->>B: init()
    B->>B: new AppTray()
    B->>C: new AppTrayIcon()
    B->>D: new TrayErrorHandler()
    A->>B: get()
    B-->>A: INSTANCE
    A->>B: show()
    B->>SystemTray: isSupported()
    alt 支持系统托盘
        B->>C: show()
    end
    A->>B: hide()
    B->>C: hide()
    Note over D: 错误处理流程
    D->>D: handle(event)
    D->>Platform: runLater()
    Platform->>D: 延迟执行
    D->>C: showErrorMessage(title, desc)
```

这段代码实现了一个系统托盘应用的单例模式，包含图标显示/隐藏功能和错误处理机制。流程图展示了类结构关系，其中核心是AppTray单例类，通过内部类TrayErrorHandler处理错误事件，并依赖AppTrayIcon实现托盘图标操作。时序图则演示了初始化、显示/隐藏托盘以及错误处理的完整调用链，特别注意错误处理采用了Platform.runLater()实现线程安全的消息延迟展示。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| icon | AppTrayIcon | 私有成员变量icon，类型为AppTrayIcon。 |
| INSTANCE | AppTray | 单例模式下的静态实例变量。 |
| errorHandler | ErrorHandler | 私有终态错误处理器，通过Getter访问。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| hide | void | 隐藏图标。 |
| init | void | 静态方法初始化应用托盘实例。 |
| get | AppTray | 获取AppTray单例实例。 |
| show | void | 方法检查系统托盘支持，不支持则退出，支持则显示图标。 |




