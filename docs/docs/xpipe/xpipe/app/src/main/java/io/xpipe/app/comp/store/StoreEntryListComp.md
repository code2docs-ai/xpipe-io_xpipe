# 基础信息

|      |      |
|------|------|
| 名称 | StoreEntryListComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/store/StoreEntryListComp.java |
| 包名 | io.xpipe.app.comp.store |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.SimpleComp', 'io.xpipe.app.comp.base.ListBoxViewComp', 'io.xpipe.app.comp.base.MultiContentComp', 'io.xpipe.app.comp.base.VerticalComp', 'io.xpipe.app.core.AppCache', 'io.xpipe.app.core.AppLayoutModel', 'javafx.beans.binding.Bindings', 'javafx.beans.property.SimpleBooleanProperty', 'javafx.beans.value.ObservableValue', 'javafx.geometry.Insets', 'javafx.scene.layout.Region', 'javafx.scene.layout.VBox', 'java.util.LinkedHashMap', 'java.util.List'] |
| 概述说明 | 创建商店条目列表组件，包含滚动重置、状态栏和不同条件下的内容显示逻辑。 |

# 说明

StoreEntryListComp是一个继承自SimpleComp的组件，主要用于创建和管理商店条目列表界面。它包含一个createList方法，用于构建列表视图，该视图显示当前顶级部分的子项，并支持滚动重置功能。组件还包含状态栏和多个条件绑定的显示逻辑，如根据不同的分类和条目数量显示不同的介绍内容。整体布局采用垂直结构，结合了多种条件判断来控制不同组件的显示与隐藏。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| StoreEntryListComp | class | 创建商店条目列表组件，包含动态显示逻辑和滚动控制。 |



## 类 StoreEntryListComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | StoreEntryListComp |
| 说明 | 创建商店条目列表组件，包含动态显示逻辑和滚动控制。 |


### UML类图

```mermaid
classDiagram
    class StoreEntryListComp {
        -Comp~?~ createList()
        +Region createSimple()
    }

    class SimpleComp {
        <<Abstract>>
        +Region createSimple()*
    }

    class StoreViewState {
        <<Singleton>>
        +StoreViewState get()
        +StoreSection getCurrentTopLevelSection()
        +ObservableList~StoreEntry~ getAllEntries()
        +StoreCategory getActiveCategory()
        +String getFilterString()
        +BooleanProperty getBatchMode()
        +StoreCategory getAllConnectionsCategory()
        +StoreCategory getAllIdentitiesCategory()
        +StoreCategory getAllScriptsCategory()
    }

    class StoreSection {
        +ObservableList~StoreSection~ getShownChildren()
        +ObservableList~StoreSection~ getAllChildren()
        +StoreSection customSection(StoreSection e)
    }

    class ListBoxViewComp~T~ {
        +ListBoxViewComp~T~(ObservableList~T~ shown, ObservableList~T~ all, Function~T, Node~ cellFactory, boolean showHeader)
        +void setVisibilityControl(boolean visible)
        +void apply(Consumer~Structure~ consumer)
        +void styleClass(String style)
        +void vgrow()
    }

    class StoreEntryListStatusBarComp {
        +void apply(Consumer~Structure~ consumer)
        +void hide(BooleanProperty condition)
    }

    class VerticalComp {
        +VerticalComp(List~Comp~ children)
    }

    class MultiContentComp {
        +MultiContentComp(Map~Comp~?~, ObservableValue~Boolean~~ components, boolean showFirst)
        +Region createRegion()
    }

    class StoreNotFoundComp
    class StoreIntroComp
    class StoreScriptsIntroComp
    class StoreIdentitiesIntroComp

    StoreEntryListComp --|> SimpleComp
    StoreEntryListComp --> StoreViewState : 获取状态
    StoreEntryListComp --> ListBoxViewComp~StoreSection~ : 创建列表视图
    StoreEntryListComp --> StoreEntryListStatusBarComp : 创建状态栏
    StoreEntryListComp --> VerticalComp : 组合组件
    StoreEntryListComp --> MultiContentComp : 多内容管理
    StoreViewState --> StoreSection : 包含
    ListBoxViewComp~T~ --> StoreSection : 显示元素
    MultiContentComp --> StoreNotFoundComp : 包含
    MultiContentComp --> StoreIntroComp : 包含
    MultiContentComp --> StoreScriptsIntroComp : 包含
    MultiContentComp --> StoreIdentitiesIntroComp : 包含
```

类图描述：
该图展示了StoreEntryListComp继承自SimpleComp的类结构，主要功能是管理商店条目列表的显示逻辑。核心类StoreViewState作为单例维护应用状态，StoreSection处理分类数据，ListBoxViewComp实现动态列表渲染。通过MultiContentComp协调多个子组件（如StoreIntroComp等）的显示条件，根据不同的状态（如空列表、首次访问等）展示相应内容。整体结构体现了观察者模式和组合模式的应用，通过属性绑定实现动态UI更新。


### 内部方法调用关系图

```mermaid
graph TD
    A["类StoreEntryListComp"]
    B["方法: createList"]
    C["方法: createSimple"]
    D["子方法: 获取shown/all列表"]
    E["子方法: 创建ListBoxViewComp"]
    F["子方法: 设置滚动监听"]
    G["子方法: 创建statusBar"]
    H["子方法: 返回VerticalComp"]
    I["子方法: 创建条件绑定"]
    J["子方法: 构建内容映射表"]
    K["子方法: 返回MultiContentComp"]

    A --> B
    A --> C
    B --> D
    B --> E
    B --> F
    B --> G
    B --> H
    C --> I
    C --> J
    C --> K
```

这段代码是StoreEntryListComp类的实现，继承自SimpleComp。主要功能是创建商店条目列表界面，包含两个核心方法：createList()负责构建列表视图和状态栏，createSimple()处理不同场景下的内容显示逻辑。流程图展示了类结构和方法调用关系，createList()内部获取数据、创建组件并设置监听器，createSimple()通过多个条件绑定决定显示哪种内容（介绍页或列表页），最终返回组合后的界面区域。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| createSimple | Region | 创建界面组件，根据条件显示不同内容：连接、脚本、身份介绍或列表。 |
| createList | Comp<?> | 创建列表组件，包含显示项、滚动重置和状态栏。 |




