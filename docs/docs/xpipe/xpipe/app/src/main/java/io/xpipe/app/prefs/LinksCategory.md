# 基础信息

|      |      |
|------|------|
| 名称 | LinksCategory |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/prefs/LinksCategory.java |
| 包名 | io.xpipe.app.prefs |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.base.ModalOverlay', 'io.xpipe.app.comp.base.TileButtonComp', 'io.xpipe.app.util.DocumentationLink', 'io.xpipe.app.util.Hyperlinks', 'io.xpipe.app.util.OptionsBuilder'] |
| 概述说明 | LinksCategory类创建包含多个链接按钮的界面，如Discord、文档、隐私等，点击后跳转对应页面或打开模态框。 |

# 说明

LinksCategory类继承自AppPrefsCategory，用于创建包含多个链接按钮的界面组件。组件包含Discord、文档、测试版、隐私政策、第三方依赖和用户协议等按钮，点击后分别打开对应链接或弹窗。每个按钮具有描述文本、图标和点击事件处理逻辑。组件宽度预设为600像素，并添加了特定样式类。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| LinksCategory | class | 创建链接分类界面，包含Discord、文档、测试版、隐私、第三方依赖和EULA等按钮。 |



## 类 LinksCategory

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | LinksCategory |
| 说明 | 创建链接分类界面，包含Discord、文档、测试版、隐私、第三方依赖和EULA等按钮。 |


### UML类图

```mermaid
classDiagram
    class AppPrefsCategory {
        <<Interface>>
        +String getId()
        +Comp~?~ create()
    }

    class LinksCategory {
        -Comp~?~ createLinks()
        +String getId()
        +Comp~?~ create()
    }

    class OptionsBuilder {
        +addTitle(String title) OptionsBuilder
        +addComp(Comp~?~ comp) OptionsBuilder
        +addComp(Comp~?~ comp, Object constraints) OptionsBuilder
        +buildComp() Comp~?~
    }

    class TileButtonComp {
        +TileButtonComp(String text, String desc, String icon, EventHandler~ActionEvent~ handler)
        +grow(boolean horizontal, boolean vertical) TileButtonComp
    }

    class Hyperlinks {
        <<final class>>
        +static String DISCORD
        +static String DOCS
        +static String GITHUB_PTB
        +static void open(String url)
    }

    class DocumentationLink {
        <<enum>>
        +PRIVACY
        +EULA
        +void open()
    }

    class ThirdPartyDependencyListComp {
        +prefWidth(double width) ThirdPartyDependencyListComp
        +styleClass(String styleClass) ThirdPartyDependencyListComp
    }

    class ModalOverlay {
        +static ModalOverlay of(String id, Comp~?~ content)
        +void show()
    }

    LinksCategory --> AppPrefsCategory : 实现
    LinksCategory --> OptionsBuilder : 使用
    LinksCategory --> TileButtonComp : 创建
    LinksCategory --> Hyperlinks : 调用
    LinksCategory --> DocumentationLink : 调用
    LinksCategory --> ThirdPartyDependencyListComp : 创建
    LinksCategory --> ModalOverlay : 使用
    TileButtonComp --> Hyperlinks : 依赖
    TileButtonComp --> DocumentationLink : 依赖
    TileButtonComp --> ThirdPartyDependencyListComp : 依赖
    TileButtonComp --> ModalOverlay : 依赖
```

这段代码展示了一个`LinksCategory`类，它继承自`AppPrefsCategory`接口，主要用于创建包含多个链接按钮的界面组件。通过`OptionsBuilder`构建布局，使用`TileButtonComp`创建不同功能的按钮（如打开Discord、文档、测试版等），并处理点击事件。按钮事件涉及`Hyperlinks`打开URL、`DocumentationLink`显示文档、以及`ModalOverlay`显示第三方依赖列表。整体设计采用构建器模式，具有清晰的组件结构和事件处理机制。


### 内部方法调用关系图

```mermaid
graph TD
    A["类LinksCategory继承AppPrefsCategory"]
    B["方法: Comp<?> createLinks()"]
    C["方法: String getId()"]
    D["重写方法: Comp<?> create()"]
    E["OptionsBuilder构造"]
    F["添加标题: 'links'"]
    G["添加垂直间距: 19px"]
    H["创建TileButtonComp: discord"]
    I["创建TileButtonComp: documentation"]
    J["创建TileButtonComp: tryPtb"]
    K["创建TileButtonComp: privacy"]
    L["创建TileButtonComp: thirdParty"]
    M["创建TileButtonComp: eula"]
    N["添加垂直间距: 40px"]
    O["构建组件: buildComp()"]
    P["设置样式类: 'information'"]
    Q["设置样式类: 'about-tab'"]
    R["设置预设宽度: 600px"]

    A --> B
    A --> C
    A --> D
    B --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
    D --> B
    D --> P
    P --> Q
    Q --> R
```

这段代码展示了一个LinksCategory类，它继承自AppPrefsCategory，主要用于创建包含多个功能按钮的链接面板。通过createLinks()方法使用OptionsBuilder构建界面，添加了6个不同功能的TileButtonComp（Discord、文档、测试版、隐私条款、第三方依赖和用户协议），每个按钮都绑定了对应的事件处理逻辑。最后通过重写create()方法设置组件样式和宽度，形成一个完整的链接分类界面。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getId | String | 重写getId方法，返回字符串"links"。 |
| createLinks | Comp<?> | 创建包含多个功能按钮的界面组件，按钮包括Discord、文档、测试版、隐私、第三方依赖和EULA。 |
| create | Comp<?> | 重写create方法，生成带样式的组件并设置宽度为600。 |




