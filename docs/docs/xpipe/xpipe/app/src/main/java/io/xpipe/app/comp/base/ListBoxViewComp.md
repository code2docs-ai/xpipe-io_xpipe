# 基础信息

|      |      |
|------|------|
| 名称 | ListBoxViewComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/base/ListBoxViewComp.java |
| 包名 | io.xpipe.app.comp.base |
| 依赖项 | ['io.xpipe.app.browser.BrowserFullSessionModel', 'io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.CompStructure', 'io.xpipe.app.comp.SimpleCompStructure', 'io.xpipe.app.comp.store.StoreViewState', 'io.xpipe.app.core.AppLayoutModel', 'io.xpipe.app.util.DerivedObservableList', 'javafx.animation.AnimationTimer', 'javafx.application.Platform', 'javafx.beans.binding.Bindings', 'javafx.beans.property.SimpleBooleanProperty', 'javafx.collections.ListChangeListener', 'javafx.collections.ObservableList', 'javafx.css.PseudoClass', 'javafx.scene.Node', 'javafx.scene.control.ScrollBar', 'javafx.scene.control.ScrollPane', 'javafx.scene.layout.Region', 'javafx.scene.layout.VBox', 'lombok.Setter', 'java.util', 'java.util.concurrent.atomic.AtomicBoolean', 'java.util.function.Function'] |
| 概述说明 | 列表视图组件，支持动态刷新、滚动条控制和可见性管理。 |

# 说明

这是一个名为ListBoxViewComp的JavaFX组件类，用于管理可滚动列表视图。它支持动态内容更新、奇偶行样式标记、首尾行标记，以及可选的滚动条控制。组件通过缓存机制优化性能，并提供了可视性控制功能，可根据滚动位置动态显示或隐藏列表项。核心功能包括监听数据变化自动刷新视图、处理滚动事件、管理组件可见性，以及维护样式状态。该类设计用于处理大量数据，通过延迟渲染和局部更新提高效率。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ListBoxViewComp | class | 列表视图组件，支持动态刷新、滚动条控制和可见性管理。 |



## 类 ListBoxViewComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ListBoxViewComp |
| 说明 | 列表视图组件，支持动态刷新、滚动条控制和可见性管理。 |


### UML类图

```mermaid
classDiagram
    class ListBoxViewComp~T~ {
        -PseudoClass ODD
        -PseudoClass EVEN
        -PseudoClass FIRST
        -PseudoClass LAST
        -ObservableList~T~ shown
        -ObservableList~T~ all
        -Function~T, Comp~?~~ compFunction
        -boolean scrollBar
        -boolean visibilityControl
        +ListBoxViewComp(ObservableList~T~ shown, ObservableList~T~ all, Function~T, Comp~?~~ compFunction, boolean scrollBar)
        +CompStructure~ScrollPane~ createBase()
        -void registerVisibilityListeners(ScrollPane scroll, VBox vbox)
        -boolean isVisible(ScrollPane pane, VBox box, Node node)
        -void updateVisibilities(ScrollPane scroll, VBox vbox)
        -void refresh(ScrollPane scroll, VBox listView, List~? extends T~ shown, List~? extends T~ all, Map~T, Region~ cache, boolean refreshVisibilities)
    }

    class ScrollPane {
        <<JavaFX>>
    }

    class VBox {
        <<JavaFX>>
    }

    class Comp~T~ {
        <<Interface>>
        +CompStructure~T~ createBase()
    }

    class CompStructure~T~ {
        <<Interface>>
    }

    class SimpleCompStructure~T~ {
        +SimpleCompStructure(T node)
    }

    class ObservableList~T~ {
        <<Interface>>
    }

    class Function~T, R~ {
        <<Interface>>
        +R apply(T t)
    }

    class Region {
        <<JavaFX>>
    }

    class Node {
        <<JavaFX>>
    }

    ListBoxViewComp --> ScrollPane : 包含
    ListBoxViewComp --> VBox : 包含
    ListBoxViewComp --> Comp : 实现
    CompStructure <|.. SimpleCompStructure
    Comp <|.. ListBoxViewComp
    ListBoxViewComp --> ObservableList : 使用
    ListBoxViewComp --> Function : 使用
    ScrollPane --> Node : 继承
    VBox --> Region : 继承
    Region --> Node : 继承
```

类图描述：
ListBoxViewComp是一个泛型组件类，用于管理可滚动列表视图，继承自Comp接口并实现其createBase方法。核心功能包括动态刷新列表内容、处理可见性控制、管理样式状态(奇偶行/首尾项)。通过ObservableList跟踪数据，使用Function生成子组件，依赖JavaFX的ScrollPane和VBox实现布局。包含复杂的可见性计算逻辑和异步更新机制，支持滚动条控制和多种场景下的数据同步。


### 内部方法调用关系图

```mermaid
graph TD
    A["类ListBoxViewComp<T>"]
    B["静态常量: ODD, EVEN, FIRST, LAST"]
    C["属性: ObservableList<T> shown"]
    D["属性: ObservableList<T> all"]
    E["属性: Function<T, Comp<?>> compFunction"]
    F["属性: boolean scrollBar"]
    G["属性: boolean visibilityControl"]
    H["构造方法: ListBoxViewComp(...)"]
    I["方法: createBase()"]
    J["方法: registerVisibilityListeners(ScrollPane, VBox)"]
    K["方法: isVisible(ScrollPane, VBox, Node)"]
    L["方法: updateVisibilities(ScrollPane, VBox)"]
    M["方法: refresh(ScrollPane, VBox, List<T>, List<T>, Map<T, Region>, boolean)"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    I --> J
    I --> M
    J --> K
    J --> L
    M --> L
```

```mermaid
sequenceDiagram
    participant Main
    participant ListBoxViewComp
    participant ScrollPane
    participant VBox
    participant ObservableList
    participant Platform

    Main->>ListBoxViewComp: 创建实例(shown, all, compFunction, scrollBar)
    Main->>ListBoxViewComp: createBase()
    ListBoxViewComp->>VBox: 创建VBox实例
    ListBoxViewComp->>ScrollPane: 创建ScrollPane实例
    ListBoxViewComp->>ListBoxViewComp: refresh(scroll, vbox, shown, all, cache, false)
    ListBoxViewComp->>ScrollPane: 监听sceneProperty变化
    ScrollPane->>ListBoxViewComp: scene变化时回调
    ListBoxViewComp->>ListBoxViewComp: refresh(scroll, vbox, shown, all, cache, true)
    ListBoxViewComp->>ObservableList: 添加shown监听器
    ObservableList->>Platform: 数据变化时调用runLater
    Platform->>ListBoxViewComp: 执行refresh(scroll, vbox, c.getList(), all, cache, true)
    ListBoxViewComp->>ScrollPane: 设置滚动条策略
    ListBoxViewComp->>ListBoxViewComp: registerVisibilityListeners(scroll, vbox)
    ListBoxViewComp->>ScrollPane: 监听vvalueProperty变化
    ListBoxViewComp->>ScrollPane: 监听heightProperty变化
    ListBoxViewComp->>VBox: 监听heightProperty变化
    ListBoxViewComp->>VBox: 监听sceneProperty变化
    ListBoxViewComp->>Main: 返回SimpleCompStructure(scroll)
```

流程图描述：该流程图展示了ListBoxViewComp类的结构和主要方法调用关系。类包含静态常量、属性和构造方法，核心方法是createBase()，它会创建VBox和ScrollPane实例，并调用refresh()初始化内容。registerVisibilityListeners()方法负责设置各种监听器，包括滚动位置、高度变化等，并触发updateVisibilities()更新可见性。refresh()方法会更新列表内容并应用样式类。整个流程实现了可滚动列表的动态更新和可见性控制功能。

时序图描述：该时序图描述了ListBoxViewComp从创建到初始化的完整过程。首先创建实例并调用createBase()，初始化VBox和ScrollPane，首次刷新内容。随后设置scene监听器和列表数据监听器，当数据变化时通过Platform.runLater异步刷新。最后设置滚动条策略和可见性监听器，返回包含ScrollPane的组件结构。整个过程体现了JavaFX组件的异步更新机制和事件驱动特性。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| shown | ObservableList<T> | 私有可观察列表shown，类型为T。 |
| scrollBar | boolean | 私有布尔型滚动条变量。 |
| FIRST = PseudoClass.getPseudoClass("first") | PseudoClass | 定义常量FIRST表示伪类"first"。 |
| LAST = PseudoClass.getPseudoClass("last") | PseudoClass | 私有静态常量LAST定义为伪类"last"。 |
| visibilityControl = false | boolean | 私有布尔变量visibilityControl默认false |
| compFunction | Function<T, Comp<?>> | 私有函数compFunction，输入T类型，返回Comp<?>类型。 |
| ODD = PseudoClass.getPseudoClass("odd") | PseudoClass | 定义静态常量ODD，表示伪类"odd"。 |
| EVEN = PseudoClass.getPseudoClass("even") | PseudoClass | 定义静态常量EVEN表示伪类"even"。 |
| all | ObservableList<T> | 私有不可变列表all，类型为ObservableList<T>。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| registerVisibilityListeners | void | 注册滚动和布局监听器，动态更新可视状态。 |
| createBase | CompStructure<ScrollPane> | 创建滚动面板组件，包含动态刷新、场景监听和滚动条控制功能。 |
| refresh | void | 刷新UI列表，同步缓存并更新可见性。 |
| updateVisibilities | void | 检查线程后更新VBox子节点可见性，计数可见项，超10不处理。 |
| isVisible | boolean | 检查节点在滚动面板中是否可见，考虑场景、边界和高度条件。 |




