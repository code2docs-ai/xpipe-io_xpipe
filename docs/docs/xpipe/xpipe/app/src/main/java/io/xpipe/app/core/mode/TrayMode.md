# 基础信息

|      |      |
|------|------|
| 名称 | TrayMode |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/mode/TrayMode.java |
| 包名 | io.xpipe.app.core.mode |
| 依赖项 | ['io.xpipe.app.core.AppTray', 'io.xpipe.app.issue', 'io.xpipe.app.util.PlatformThread', 'io.xpipe.core.process.OsType', 'java.awt'] |
| 概述说明 | TrayMode类扩展PlatformMode，支持Windows系统托盘功能，包含初始化、切换和错误处理逻辑。 |

# 说明

TrayMode类继承PlatformMode，专为Windows系统设计，需满足桌面和系统托盘支持条件。切换至该模式时初始化并显示托盘图标，切换时隐藏托盘。提供唯一标识符"tray"，错误处理机制确保托盘初始化完成后处理异常，未完成则记录日志并忽略错误。整个过程包含事件跟踪和线程安全操作。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| TrayMode | class | TrayMode类扩展PlatformMode，支持Windows系统托盘功能，包含初始化、切换和错误处理逻辑。 |



## 类 TrayMode

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | TrayMode |
| 说明 | TrayMode类扩展PlatformMode，支持Windows系统托盘功能，包含初始化、切换和错误处理逻辑。 |


### UML类图

```mermaid
classDiagram
    class PlatformMode {
        <<abstract>>
        +boolean isSupported()
        +void onSwitchTo() throws Throwable
        +String getId()
        +void onSwitchFrom()
        +ErrorHandler getErrorHandler()
    }

    class TrayMode {
        +boolean isSupported()
        +void onSwitchTo() throws Throwable
        +String getId()
        +void onSwitchFrom()
        +ErrorHandler getErrorHandler()
    }

    class OsType {
        <<enumeration>>
        WINDOWS
        +static OsType getLocal()
    }

    class Desktop {
        <<Utility>>
        +static boolean isDesktopSupported()
    }

    class SystemTray {
        <<Utility>>
        +static boolean isSupported()
    }

    class AppTray {
        -static AppTray instance
        +static void init()
        +static AppTray get()
        +void show()
        +void hide()
        +ErrorHandler getErrorHandler()
    }

    class PlatformThread {
        <<Utility>>
        +static void runLaterIfNeededBlocking(Runnable~void~ task)
    }

    class TrackEvent {
        <<Utility>>
        +static void info(String message)
    }

    class ErrorHandler {
        <<Interface>>
        +void handle(ErrorEvent event)
    }

    class LogErrorHandler {
        +void handle(ErrorEvent event)
    }

    class SyncErrorHandler {
        -ErrorHandler delegate
        +SyncErrorHandler(ErrorHandler delegate)
        +void handle(ErrorEvent event)
    }

    class ErrorAction {
        <<Utility>>
        +static ErrorHandler ignore()
    }

    TrayMode --|> PlatformMode : 继承
    TrayMode --> OsType : 调用方法
    TrayMode --> Desktop : 调用方法
    TrayMode --> SystemTray : 调用方法
    TrayMode --> AppTray : 依赖
    TrayMode --> PlatformThread : 调用方法
    TrayMode --> TrackEvent : 记录日志
    TrayMode --> ErrorHandler : 使用
    LogErrorHandler ..|> ErrorHandler : 实现
    SyncErrorHandler ..|> ErrorHandler : 实现
    SyncErrorHandler --> LogErrorHandler : 组合
    SyncErrorHandler --> ErrorAction : 调用方法
```

该类图展示了TrayMode继承自PlatformMode的实现细节，包含对系统托盘功能的支持检查、切换操作和错误处理机制。TrayMode通过OsType、Desktop和SystemTray验证Windows平台支持，依赖AppTray管理托盘图标，使用PlatformThread确保线程安全，并通过组合LogErrorHandler和SyncErrorHandler实现多层错误处理。整个设计体现了平台特定功能的模块化实现和健壮的错误处理策略。


### 内部方法调用关系图

```mermaid
graph TD
    A["类TrayMode继承PlatformMode"]
    B["重写方法: boolean isSupported()"]
    C["重写方法: void onSwitchTo()"]
    D["重写方法: String getId()"]
    E["重写方法: void onSwitchFrom()"]
    F["重写方法: ErrorHandler getErrorHandler()"]
    G["条件检查: Windows系统 && 父类支持 && Desktop支持 && SystemTray支持"]
    H["调用父类方法: super.onSwitchTo()"]
    I["平台线程执行: PlatformThread.runLaterIfNeededBlocking"]
    J["初始化托盘: AppTray.init()"]
    K["显示托盘: AppTray.get().show()"]
    L["日志记录: TrackEvent.info"]
    M["隐藏托盘: AppTray.get().hide()"]
    N["创建错误处理器: LogErrorHandler + SyncErrorHandler"]
    O["处理错误: 调用托盘错误处理器 + 日志记录 + 忽略错误"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    B --> G
    C --> H
    C --> I
    I --> J
    I --> K
    I --> L
    E --> M
    E --> L
    F --> N
    N --> O
```

这段代码是TrayMode类的实现，继承自PlatformMode基类。主要功能包括：检查系统托盘支持状态(isSupported)、切换至托盘模式时初始化并显示托盘(onSwitchTo)、退出时隐藏托盘(onSwitchFrom)、提供错误处理机制(getErrorHandler)。核心逻辑通过PlatformThread保证线程安全，使用AppTray管理托盘图标，并通过TrackEvent记录关键操作日志。错误处理采用组合模式，同时调用托盘专属处理器和基础日志处理器。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getId | String | 重写getId方法，返回字符串"tray"。 |
| getErrorHandler | ErrorHandler | 重写getErrorHandler方法，返回同步错误处理器，处理事件时检查托盘初始化并记录日志。 |
| onSwitchTo | void | 切换时初始化托盘并显示，确保线程安全。 |
| onSwitchFrom | void | 重写方法：关闭托盘并记录日志 |
| isSupported | boolean | 检查Windows系统支持且满足父类及桌面、系统托盘支持条件。 |




