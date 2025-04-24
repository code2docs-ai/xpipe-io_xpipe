# 基础信息

|      |      |
|------|------|
| 名称 | StoreCreationMenu |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/store/StoreCreationMenu.java |
| 包名 | io.xpipe.app.comp.store |
| 依赖项 | ['io.xpipe.app.comp.base.PrettyImageHelper', 'io.xpipe.app.core.AppI18n', 'io.xpipe.app.ext.DataStoreCreationCategory', 'io.xpipe.app.ext.DataStoreProviders', 'io.xpipe.app.util.ScanDialog', 'javafx.application.Platform', 'javafx.scene.control.Menu', 'javafx.scene.control.MenuButton', 'javafx.scene.control.MenuItem', 'javafx.scene.control.SeparatorMenuItem', 'org.kordamp.ikonli.javafx.FontIcon', 'java.util.Comparator'] |
| 概述说明 | 为菜单添加创建各类数据存储的按钮选项。 |

# 说明

该代码描述了一个用于创建数据存储的菜单类StoreCreationMenu。主要功能包括根据参数allowSearch决定是否添加搜索按钮，以及添加多个预设类别的数据存储创建选项，如主机、桌面、脚本、命令、服务、隧道、串口和身份等。每个类别通过category方法生成菜单项，该方法会根据提供程序数量决定显示单个菜单项或带子菜单的选项。菜单项包含图标、本地化文本和点击事件处理，点击后会打开对应的创建对话框。对于多提供程序的类别，会按优先级排序并分组显示。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| StoreCreationMenu | class | 创建菜单按钮，支持搜索及多种数据存储类别添加。 |



## 类 StoreCreationMenu

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | StoreCreationMenu |
| 说明 | 创建菜单按钮，支持搜索及多种数据存储类别添加。 |


### UML类图

```mermaid
classDiagram
    class StoreCreationMenu {
        +addButtons(MenuButton menu, boolean allowSearch) void
        -category(String name, String graphic, DataStoreCreationCategory category, String defaultProvider) MenuItem
    }

    class MenuButton {
        +getItems() ObservableList~MenuItem~
    }

    class MenuItem {
        +setGraphic(Node value) void
        +textProperty() StringProperty
        +setOnAction(EventHandler~ActionEvent~ value) void
    }

    class FontIcon {
        +FontIcon(String iconCode)
    }

    class AppI18n {
        +observable(String key) StringBinding
    }

    class ScanDialog {
        +showSingleAsync(Object arg) void
    }

    class SeparatorMenuItem {
    }

    class DataStoreCreationCategory {
        <<Enumeration>>
        HOST
        DESKTOP
        SCRIPT
        COMMAND
        SERVICE
        TUNNEL
        SERIAL
        IDENTITY
    }

    class DataStoreProviders {
        +getAll() List~DataStoreProvider~
        +byId(String id) Optional~DataStoreProvider~
    }

    class DataStoreProvider {
        <<Interface>>
        +getCreationCategory() DataStoreCreationCategory
        +getOrderPriority() int
        +displayName() StringBinding
        +getDisplayIconFileName(Object arg) String
    }

    class StoreCreationDialog {
        +showCreation(DataStoreProvider provider, DataStoreCreationCategory category) void
    }

    class PrettyImageHelper {
        +ofFixedSizeSquare(String fileName, int size) ImageHelper
    }

    StoreCreationMenu --> MenuButton : 使用
    StoreCreationMenu --> DataStoreProviders : 查询
    StoreCreationMenu --> DataStoreCreationCategory : 使用枚举
    StoreCreationMenu --> StoreCreationDialog : 调用
    MenuItem <|-- SeparatorMenuItem : 继承
    DataStoreProviders --> DataStoreProvider : 管理
    PrettyImageHelper --> ImageHelper : 创建
```

这段代码描述了一个商店创建菜单系统，主要包含StoreCreationMenu类及其相关依赖。StoreCreationMenu通过addButtons方法动态构建菜单项，根据allowSearch参数决定是否添加搜索功能，并使用category方法创建不同类型的菜单项。系统涉及菜单项管理、国际化支持、图标显示、对话框交互等功能，通过DataStoreProviders获取不同类别的数据存储提供者，最终通过StoreCreationDialog展示创建界面。代码结构清晰，采用了JavaFX的UI组件和事件处理机制。


### 内部方法调用关系图

```mermaid
graph TD
    A["类StoreCreationMenu"]
    B["静态方法: addButtons(MenuButton menu, boolean allowSearch)"]
    C["私有静态方法: category(String name, String graphic, DataStoreCreationCategory category, String defaultProvider)"]
    D["条件判断: if (allowSearch)"]
    E["创建MenuItem: automatically"]
    F["绑定图标: setGraphic"]
    G["绑定文本: textProperty.bind"]
    H["设置点击事件: setOnAction"]
    I["添加菜单项: menu.getItems().add"]
    J["添加分隔符: new SeparatorMenuItem()"]
    K["调用category方法添加各类菜单项"]
    L["过滤数据存储提供者: DataStoreProviders.getAll().stream().filter"]
    M["判断提供者数量: if (sub.size() < 2)"]
    N["创建简单菜单项: new MenuItem()"]
    O["创建子菜单: new Menu()"]
    P["排序提供者: providers.stream().sorted"]
    Q["添加分隔符和子菜单项"]

    A --> B
    A --> C
    B --> D
    D -->|true| E
    E --> F
    E --> G
    E --> H
    E --> I
    I --> J
    B --> K
    K --> C
    C --> L
    C --> M
    M -->|true| N
    N --> F
    N --> G
    N --> H
    N --> I
    M -->|false| O
    O --> F
    O --> G
    O --> H
    O --> P
    P --> Q
```

这段代码流程图展示了StoreCreationMenu类的主要结构和工作流程。该类包含两个核心方法：addButtons用于构建菜单按钮，根据allowSearch参数决定是否添加搜索功能；category方法负责创建不同类型的菜单项，根据数据存储提供者数量决定生成简单菜单项还是带子菜单的复杂项。流程从主方法开始，通过条件分支和循环结构动态构建菜单层次，最终形成一个完整的交互式菜单系统。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| category | MenuItem | 创建菜单项，根据类别筛选数据存储提供者，支持单选项或多级菜单。 |
| addButtons | void | 为菜单添加按钮，包括搜索、主机、桌面、脚本、命令、服务、隧道、串口和身份选项。 |




