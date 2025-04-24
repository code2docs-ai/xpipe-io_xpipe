# 基础信息

|      |      |
|------|------|
| 名称 | AppDialog |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/window/AppDialog.java |
| 包名 | io.xpipe.app.core.window |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.base.ModalButton', 'io.xpipe.app.comp.base.ModalOverlay', 'io.xpipe.app.core.AppI18n', 'io.xpipe.app.util.PlatformInit', 'io.xpipe.app.util.PlatformThread', 'io.xpipe.app.util.ThreadHelper', 'javafx.animation.PauseTransition', 'javafx.application.Platform', 'javafx.beans.value.ObservableValue', 'javafx.collections.FXCollections', 'javafx.collections.ListChangeListener', 'javafx.collections.ObservableList', 'javafx.scene.layout.StackPane', 'javafx.scene.text.Text', 'javafx.util.Duration', 'lombok.Getter', 'java.util.concurrent.atomic.AtomicBoolean'] |
| 概述说明 | AppDialog类管理模态对话框，提供显示、关闭、确认等功能，支持多线程操作和国际化文本。 |

# 说明

该代码定义了一个AppDialog类，用于管理模态对话框的显示和交互。主要功能包括：维护一个模态对话框列表，提供显示、关闭、等待关闭等操作。支持同步和异步显示对话框，包含确认对话框功能，可绑定国际化文本。通过PlatformThread处理线程安全，使用ObservableList跟踪对话框状态，并提供文本对话框组件创建方法。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppDialog | class | JavaFX模态对话框工具类，提供显示、关闭、等待及确认功能。 |



## 类 AppDialog

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppDialog |
| 说明 | JavaFX模态对话框工具类，提供显示、关闭、等待及确认功能。 |


### UML类图

```mermaid
classDiagram
    class AppDialog {
        -ObservableList~ModalOverlay~ modalOverlays$
        +closeDialog(ModalOverlay overlay) void
        +waitForAllDialogsClose() void
        -waitForDialogClose(ModalOverlay overlay) void
        +show(ModalOverlay o) void
        +hide(ModalOverlay o) void
        +showAndWait(ModalOverlay o) void
        +show(ModalOverlay o, boolean wait) void
        +dialogTextKey(String s) Comp~?~
        +dialogText(String s) Comp~?~
        +dialogText(ObservableValue~String~ s) Comp~?~
        +confirm(String translationKey) boolean
        +confirm(String titleKey, ObservableValue~String~ content) boolean
        -showMainWindow() void
    }

    class ModalOverlay {
        <<Interface>>
    }

    class PlatformThread {
        <<Static>>
        +runLaterIfNeeded(Runnable r) void
        +runLaterIfNeededBlocking(Runnable r) void
        +enterNestedEventLoop(Object key) void
        +exitNestedEventLoop(Object key) void
    }

    class Comp~T~ {
        <<Generic>>
    }

    class ModalButton {
        <<Static>>
        +cancel() ModalButton
        +ok(Runnable action) ModalButton
    }

    class AppI18n {
        <<Static>>
        +observable(String key) ObservableValue~String~
    }

    AppDialog --> ModalOverlay : 管理
    AppDialog --> PlatformThread : 依赖
    AppDialog --> Comp~?~ : 创建
    AppDialog --> ModalButton : 使用
    AppDialog --> AppI18n : 依赖
```

这段代码定义了一个`AppDialog`类，用于管理JavaFX中的模态对话框。它提供了显示/隐藏对话框、等待对话框关闭、创建对话框文本内容以及确认对话框等功能。类通过`PlatformThread`处理线程安全操作，使用`ModalOverlay`接口表示对话框，并通过`Comp`泛型类构建UI组件。`ModalButton`和`AppI18n`分别用于创建对话框按钮和国际化文本。整个设计采用观察者模式管理对话框状态，并确保线程安全的UI操作。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AppDialog"]
    B["静态属性: ObservableList<ModalOverlay> modalOverlays"]
    C["私有方法: showMainWindow()"]
    D["公有方法: closeDialog(ModalOverlay)"]
    E["公有方法: waitForAllDialogsClose()"]
    F["私有方法: waitForDialogClose(ModalOverlay)"]
    G["公有方法: show(ModalOverlay)"]
    H["公有方法: hide(ModalOverlay)"]
    I["公有方法: showAndWait(ModalOverlay)"]
    J["公有方法: show(ModalOverlay, boolean)"]
    K["公有方法: dialogTextKey(String)"]
    L["公有方法: dialogText(String)"]
    M["公有方法: dialogText(ObservableValue<String>)"]
    N["公有方法: confirm(String)"]
    O["公有方法: confirm(String, ObservableValue<String>)"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    A --> K
    K --> L
    A --> M
    A --> N
    A --> O

    C --> C1["PlatformInit.init(true)"]
    C --> C2["AppMainWindow.init(true)"]
    D --> D1["PlatformThread.runLaterIfNeeded"]
    D1 --> D2["modalOverlays.remove(overlay)"]
    E --> E1["循环检查modalOverlays.isEmpty()"]
    F --> F1["循环检查modalOverlays.contains(overlay)"]
    G --> J
    I --> J
    J --> C
    J --> J1["分支: 非FX线程处理"]
    J1 --> J2["PlatformThread.runLaterIfNeededBlocking"]
    J2 --> J3["modalOverlays.add(o)"]
    J1 --> J4["wait参数为true时调用waitForDialogClose(o)"]
    J --> J5["分支: FX线程处理"]
    J5 --> J6["PlatformThread.runLaterIfNeededBlocking"]
    J6 --> J7["modalOverlays.add(o)"]
    J6 --> J8["添加ListChangeListener"]
    J8 --> J9["监听移除操作并触发事件循环退出"]
    J5 --> J10["wait参数为true时进入事件循环"]
    N --> N1["创建AtomicBoolean confirmed"]
    N --> N2["创建ModalOverlay"]
    N --> N3["添加按钮事件"]
    N --> I
    N --> N4["返回confirmed值"]
    O --> O1["创建AtomicBoolean confirmed"]
    O --> O2["创建ModalOverlay"]
    O --> O3["添加按钮事件"]
    O --> I
    O --> O4["返回confirmed值"]
```

该流程图展示了AppDialog类的完整结构，包含12个主要方法和它们的调用关系。核心逻辑集中在模态对话框的显示/隐藏控制（show/hide/showAndWait方法）和确认对话框功能（confirm方法）。特别注意线程安全处理（synchronized块）和JavaFX线程调度（PlatformThread.runLaterIfNeeded），以及两种不同线程环境下的处理分支。对话框状态通过ObservableList进行监控，并采用事件循环机制实现同步等待功能。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| modalOverlays = FXCollections.observableArrayList() | ObservableList<ModalOverlay> | 私有静态可观察列表modalOverlays存储ModalOverlay实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| dialogTextKey | Comp<?> | 静态方法dialogTextKey返回Comp对象，参数s转换为可观察文本。 |
| show | void | 静态方法show展示模态覆盖层，默认不强制显示。 |
| confirm | boolean | 静态方法确认对话框，返回用户是否点击确认。 |
| show | void | 显示模态窗口，处理线程同步和关闭等待逻辑。 |
| waitForDialogClose | void | 等待模态对话框关闭，检查覆盖层存在时休眠10毫秒。 |
| closeDialog | void | 静态方法关闭模态对话框，移除覆盖层并同步线程。 |
| confirm | boolean | 静态方法确认对话框，返回用户点击确认结果。 |
| hide | void | 隐藏模态覆盖层，从列表中移除指定对象。 |
| waitForAllDialogsClose | void | 等待所有对话框关闭 |
| showMainWindow | void | 初始化平台和主窗口。 |
| showAndWait | void | 静态方法显示模态覆盖层并等待。 |
| dialogText | Comp<?> | 静态方法dialogText创建带样式的文本组件，宽度450。 |
| dialogText | Comp<?> | 静态方法创建绑定文本的对话框组件，宽度450。 |




