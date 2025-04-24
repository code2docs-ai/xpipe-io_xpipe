# 基础信息

|      |      |
|------|------|
| 名称 | FilterComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/base/FilterComp.java |
| 包名 | io.xpipe.app.comp.base |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.CompStructure', 'io.xpipe.app.comp.SimpleCompStructure', 'io.xpipe.app.core.AppActionLinkDetector', 'io.xpipe.app.core.AppI18n', 'io.xpipe.app.util.PlatformThread', 'javafx.beans.binding.Bindings', 'javafx.beans.property.Property', 'javafx.scene.Cursor', 'javafx.scene.input.KeyCode', 'javafx.scene.input.KeyCodeCombination', 'javafx.scene.input.KeyEvent', 'javafx.scene.input.MouseButton', 'atlantafx.base.controls.CustomTextField', 'org.kordamp.ikonli.javafx.FontIcon', 'java.util.Objects'] |
| 概述说明 | FilterComp组件，绑定文本属性，实现搜索框功能，含清除和图标切换逻辑。 |

# 说明

FilterComp是一个继承自Comp的组件类，用于创建带过滤功能的文本框。它接收一个Property<String>类型的filterText属性作为构造参数。组件包含一个搜索图标和一个清除图标，点击清除图标会清空filterText值。文本框支持ESC键清空内容并转移焦点，同时会实时同步filterText与文本框内容。当输入以xpipe://开头的链接时会触发特殊处理。组件还包含国际化提示文本、样式类绑定以及线程安全的内容更新机制。最终返回一个包含自定义文本框的SimpleCompStructure实例。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| FilterComp | class | FilterComp组件，绑定文本属性，含搜索框、清除按钮，支持快捷键和URL处理。 |



## 类 FilterComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | FilterComp |
| 说明 | FilterComp组件，绑定文本属性，含搜索框、清除按钮，支持快捷键和URL处理。 |


### UML类图

```mermaid
classDiagram
    class Comp~T~ {
        <<Abstract>>
        +T createBase()*
    }
    class CompStructure~T~ {
        <<Interface>>
    }
    class SimpleCompStructure~T~ {
        +SimpleCompStructure(T element)
    }
    class FilterComp {
        -Property~String~ filterText
        +FilterComp(Property~String~ filterText)
        +CompStructure~CustomTextField~ createBase()
    }
    class CustomTextField {
        +setMinHeight(double value)
        +setMaxHeight(double value)
        +getStyleClass() ObservableList~String~
        +promptTextProperty() StringProperty
        +rightProperty() ObjectProperty~Node~
        +setAccessibleText(String value)
        +addEventFilter(EventType~E~ eventType, EventHandler~E~ filter)
        +textProperty() StringProperty
        +getText() String
        +setText(String value)
        +clear()
        +getScene() Scene
        +focusedProperty() BooleanProperty
        +isFocused() boolean
    }
    class Property~T~ {
        <<Interface>>
        +T getValue()
        +void setValue(T value)
        +void subscribe(Consumer~T~ subscriber)
    }
    class FontIcon {
        +FontIcon(String iconCode)
        +setCursor(Cursor value)
        +setOnMousePressed(EventHandler~MouseEvent~ value)
        +setVisible(boolean value)
    }
    class PlatformThread {
        <<Utility>>
        +static void runLaterIfNeeded(Runnable runnable)
    }
    class AppI18n {
        <<Utility>>
        +static ObservableStringValue observable(String key)
    }
    class AppActionLinkDetector {
        <<Utility>>
        +static void handle(String url, boolean confirm)
    }

    FilterComp --> Comp : 继承
    FilterComp --> Property : 依赖
    FilterComp --> CustomTextField : 创建
    FilterComp --> FontIcon : 创建
    FilterComp --> PlatformThread : 调用
    FilterComp --> AppI18n : 调用
    FilterComp --> AppActionLinkDetector : 调用
    Comp <|-- FilterComp
    CompStructure <|.. SimpleCompStructure
    SimpleCompStructure --> CustomTextField : 包含
```

这段代码实现了一个可过滤文本的UI组件`FilterComp`，继承自泛型抽象类`Comp`，主要功能包括：1) 创建带有搜索图标和清除按钮的输入框；2) 处理文本输入、粘贴和ESC键清除操作；3) 与外部属性`filterText`双向绑定；4) 特殊处理xpipe协议链接。该组件通过`CustomTextField`实现核心输入功能，使用`FontIcon`显示图标，并通过属性订阅机制实现数据同步。类图展示了组件与JavaFX控件、工具类之间的复杂交互关系。


### 内部方法调用关系图

```mermaid
graph TD
    A["类FilterComp"]
    B["属性: Property<String> filterText"]
    C["构造方法: FilterComp(Property<String> filterText)"]
    D["重写方法: createBase()"]
    E["创建FontIcon: 'mdi2m-magnify'"]
    F["创建FontIcon: 'mdi2c-close'"]
    G["设置clear图标点击事件"]
    H["创建CustomTextField"]
    I["配置filter样式属性"]
    J["绑定promptText到国际化文本"]
    K["动态绑定右侧图标"]
    L["添加ESC键事件过滤"]
    M["订阅filterText变更"]
    N["监听filter文本变化"]
    O["返回SimpleCompStructure"]

    A --> B
    A --> C
    A --> D
    D --> E
    D --> F
    D --> G
    D --> H
    D --> I
    D --> J
    D --> K
    D --> L
    D --> M
    D --> N
    D --> O
    G -->|"MouseButton.PRIMARY"| G1["清空filterText"]
    K -->|"条件判断"| K1["显示clear/fi图标"]
    L -->|"KeyCode.ESCAPE"| L1["清空filter并转移焦点"]
    M -->|"值变更"| M1["更新UI线程显示"]
    N -->|"文本变化"| N1["处理特殊链接或更新filterText"]
```

该流程图展示了FilterComp类的完整工作流程。该类主要实现了一个带过滤功能的文本框组件，包含图标显示、文本绑定、事件处理等核心功能。当用户输入时，会实时更新过滤文本；点击清除图标或按ESC键会重置状态；特殊格式的链接会被拦截处理。整个过程通过属性绑定和事件监听实现响应式更新，最终返回一个封装好的UI组件结构。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| filterText | Property<String> | 私有字符串属性filterText |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| createBase | CompStructure<CustomTextField> | 创建搜索文本框组件，包含清除按钮、图标绑定、快捷键处理和文本监听功能。 |




