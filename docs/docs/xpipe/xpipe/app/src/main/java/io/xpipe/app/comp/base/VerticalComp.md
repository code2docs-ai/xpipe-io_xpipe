# 基础信息

|      |      |
|------|------|
| 名称 | VerticalComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/base/VerticalComp.java |
| 包名 | io.xpipe.app.comp.base |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.CompStructure', 'io.xpipe.app.comp.SimpleCompStructure', 'io.xpipe.app.util.PlatformThread', 'javafx.collections.FXCollections', 'javafx.collections.ListChangeListener', 'javafx.collections.ObservableList', 'javafx.scene.layout.VBox', 'java.util.List'] |
| 概述说明 | 垂直布局组件类，支持动态条目更新和间距设置。 |

# 说明

VerticalComp是一个基于JavaFX的组件类，继承自Comp类，使用VBox作为布局容器。它包含一个可观察的条目列表entries，可通过构造函数传入普通列表或可观察列表。提供spacing方法设置子组件间距。在createBase方法中创建VBox容器，添加样式类，并设置条目变化监听器以动态更新子组件。初始化时会遍历条目列表并添加对应区域到容器中。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| VerticalComp | class | 垂直布局组件类，支持动态更新子组件和间距设置。 |



## 类 VerticalComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | VerticalComp |
| 说明 | 垂直布局组件类，支持动态更新子组件和间距设置。 |


### UML类图

```mermaid
classDiagram
    class VerticalComp {
        -ObservableList~Comp~?~~ entries
        +VerticalComp(List~Comp~?~~ comps)
        +VerticalComp(ObservableList~Comp~?~~ entries)
        +spacing(double spacing) Comp~CompStructure~VBox~~
        +createBase() CompStructure~VBox~
    }

    class Comp~T~ {
        <<Interface>>
        +createBase() T
        +apply(Function~T,T~ func) Comp~T~
    }

    class CompStructure~T~ {
        <<Interface>>
    }

    class SimpleCompStructure~T~ {
        +SimpleCompStructure(T base)
    }

    class VBox {
        +setSpacing(double spacing)
        +getChildren() ObservableList~Node~
        +getStyleClass() ObservableList~String~
    }

    class PlatformThread {
        +sync(ObservableList~T~ list) ObservableList~T~
    }

    VerticalComp --> Comp : 实现
    SimpleCompStructure --> CompStructure : 实现
    VerticalComp --> VBox : 使用
    VerticalComp --> PlatformThread : 依赖
```

这段类图展示了VerticalComp类的结构及其相关依赖。VerticalComp是一个泛型类，实现了Comp接口，用于垂直布局组件。它包含一个可观察的组件列表entries，提供两种构造方式，并支持设置间距。通过createBase()方法创建基于VBox的布局结构，当entries变化时自动更新子节点。类图中还展示了与Comp接口、SimpleCompStructure实现类、JavaFX的VBox类以及PlatformThread工具类的关系。


### 内部方法调用关系图

```mermaid
graph TD
    A["类VerticalComp"]
    B["泛型: Comp<CompStructure<VBox>>"]
    C["属性: ObservableList<Comp<?>> entries"]
    D["构造方法1: VerticalComp(List<Comp<?>> comps)"]
    E["构造方法2: VerticalComp(ObservableList<Comp<?>> entries)"]
    F["方法: spacing(double spacing)"]
    G["重写方法: createBase()"]
    H["内部操作: FXCollections.observableArrayList"]
    I["内部操作: PlatformThread.sync"]
    J["内部操作: struc.get().setSpacing"]
    K["内部操作: VBox构造"]
    L["内部操作: addListener"]
    M["内部操作: getChildren().setAll"]
    N["内部操作: stream().map"]
    O["内部操作: getChildren().add"]
    P["返回: SimpleCompStructure<VBox>"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    D --> H
    E --> I
    F --> J
    G --> K
    G --> L
    G --> M
    M --> N
    G --> O
    G --> P
```

这段代码描述了一个名为VerticalComp的类，继承自泛型类Comp<CompStructure<VBox>>，主要用于垂直布局组件的管理。类中包含两个构造方法，分别接收List和ObservableList类型的组件列表，并通过createBase方法创建基于VBox的布局结构。关键操作包括监听列表变化动态更新子组件、设置间距参数以及初始化时添加所有子组件到VBox容器中。流程图清晰展示了从构造到布局生成的全过程，包括数据转换、事件监听和UI构建等关键步骤。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| entries | ObservableList<Comp<?>> | 私有可观察列表，存储Comp泛型对象。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| spacing | Comp<CompStructure<VBox>> | 设置VBox组件间距的方法，返回Comp对象。 |
| createBase | CompStructure<VBox> | 重写createBase方法，创建VBox并动态更新子组件。 |




