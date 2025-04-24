# 基础信息

|      |      |
|------|------|
| 名称 | AppPrefsSidebarComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/prefs/AppPrefsSidebarComp.java |
| 包名 | io.xpipe.app.prefs |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.SimpleComp', 'io.xpipe.app.comp.base.ButtonComp', 'io.xpipe.app.comp.base.VerticalComp', 'io.xpipe.app.core.AppI18n', 'io.xpipe.app.core.AppRestart', 'io.xpipe.app.util.PlatformThread', 'javafx.css.PseudoClass', 'javafx.geometry.Insets', 'javafx.geometry.Pos', 'javafx.scene.control.Button', 'javafx.scene.layout.Region', 'javafx.scene.text.TextAlignment', 'org.kordamp.ikonli.javafx.FontIcon', 'java.util.ArrayList', 'java.util.stream.Collectors'] |
| 概述说明 | 应用偏好侧边栏组件，包含分类按钮和重启按钮，动态更新选中状态。 |

# 说明

该代码定义了一个名为AppPrefsSidebarComp的Java类，继承自SimpleComp，用于创建应用程序偏好设置侧边栏组件。主要功能包括：筛选并显示可用的偏好设置类别按钮，每个按钮点击后会设置对应的选中类别，并通过伪类状态变化高亮显示当前选中项。侧边栏底部包含一个重启应用按钮，仅在需要重启时显示。所有按钮采用左对齐布局，整体结构为垂直排列的VBox容器，并实时响应类别选择变化自动触发对应按钮事件。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppPrefsSidebarComp | class | 应用偏好设置侧边栏组件，包含分类按钮和重启按钮，动态更新选中状态。 |



## 类 AppPrefsSidebarComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppPrefsSidebarComp |
| 说明 | 应用偏好设置侧边栏组件，包含分类按钮和重启按钮，动态更新选中状态。 |


### UML类图

```mermaid
classDiagram
    class AppPrefsSidebarComp {
        -PseudoClass SELECTED
        +Region createSimple()
    }
    class SimpleComp {
        <<Abstract>>
        +Region createSimple()*
    }
    class AppPrefs {
        +ObservableList~AppPrefsCategory~ getCategories()
        +ObjectProperty~AppPrefsCategory~ getSelectedCategory()
        +BooleanProperty getRequiresRestart()
    }
    class AppPrefsCategory {
        <<Interface>>
        +String getId()
        +boolean show()
    }
    class ButtonComp {
        +ButtonComp(ObservableStringValue text, Runnable action)
        +ButtonComp(ObservableStringValue text, FontIcon icon, Runnable action)
        +ButtonComp apply(Consumer~Node~ consumer)
        +ButtonComp grow(boolean h, boolean v)
        +ButtonComp padding(Insets insets)
        +ButtonComp visible(boolean visible)
    }
    class VerticalComp {
        +VerticalComp(List~Comp~ children)
        +VerticalComp apply(Consumer~Node~ consumer)
    }
    class AppRestart {
        +void restart()
    }
    class AppI18n {
        +ObservableStringValue observable(String key)
    }

    AppPrefsSidebarComp --> SimpleComp : 继承
    AppPrefsSidebarComp --> AppPrefs : 依赖
    AppPrefsSidebarComp --> AppPrefsCategory : 依赖
    AppPrefsSidebarComp --> ButtonComp : 创建实例
    AppPrefsSidebarComp --> VerticalComp : 创建实例
    AppPrefsSidebarComp --> AppRestart : 调用方法
    AppPrefsSidebarComp --> AppI18n : 调用方法
    AppPrefs --> AppPrefsCategory : 包含
    ButtonComp --> VerticalComp : 组合
```

这段代码描述了一个应用偏好设置侧边栏组件(AppPrefsSidebarComp)，它继承自SimpleComp抽象类。该组件主要功能是创建包含分类按钮和重启按钮的垂直布局，其中分类按钮通过AppPrefs获取可显示的类别(AppPrefsCategory)，并实现选中状态管理。当用户点击分类按钮时会更新AppPrefs中的选中状态，点击重启按钮则调用AppRestart.restart()方法。组件使用ButtonComp构建按钮，VerticalComp组织布局，并通过AppI18n实现国际化文本显示。整个设计采用响应式编程模式，通过订阅机制实现状态同步。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AppPrefsSidebarComp"]
    B["常量: SELECTED = PseudoClass.getPseudoClass('selected')"]
    C["重写方法: createSimple()"]
    D["获取有效分类: effectiveCategories = AppPrefs.get().getCategories().filter(show)"]
    E["创建按钮列表: buttons = effectiveCategories.map(创建分类按钮)"]
    F["创建重启按钮: restartButton = new ButtonComp('restartApp')"]
    G["设置重启按钮属性: visible/padding/grow"]
    H["组合组件: vbox = new VerticalComp(buttons + spacer + restartButton)"]
    I["订阅分类选择变化: AppPrefs.get().getSelectedCategory().subscribe(更新按钮状态)"]
    J["返回布局: vbox.createRegion()"]

    A --> B
    A --> C
    C --> D
    C --> E
    C --> F
    C --> G
    C --> H
    C --> I
    C --> J
    E -->|"每个分类按钮"| E1["ButtonComp: 文本/点击事件/样式绑定"]
    E1 --> E2["应用样式: setTextAlignment/setAlignment"]
    E1 --> E3["订阅选择状态: pseudoClassStateChanged(SELECTED)"]
    H --> I1["PlatformThread.runLaterIfNeeded: 自动触发对应分类按钮"]
```

该流程图描述了AppPrefsSidebarComp类的核心逻辑，主要展示偏好设置侧边栏的构建过程。首先过滤出需要显示的分类，为每个分类创建带状态绑定的按钮，然后添加重启应用按钮和间隔组件。所有按钮被垂直布局，并订阅分类选择变化事件以实现自动高亮和按钮触发。最终返回组装好的界面区域，形成一个动态响应偏好设置变化的侧边栏组件。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| SELECTED = PseudoClass.getPseudoClass("selected") | PseudoClass | 定义静态常量SELECTED，表示伪类"selected"。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| createSimple | Region | 创建侧边栏，包含分类按钮和重启应用按钮，动态响应选中状态。 |




