# 基础信息

|      |      |
|------|------|
| 名称 | AppConfigurationDialog |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/AppConfigurationDialog.java |
| 包名 | io.xpipe.app.core |
| 依赖项 | ['io.xpipe.app.comp.base.ModalButton', 'io.xpipe.app.comp.base.ModalOverlay', 'io.xpipe.app.comp.base.ScrollComp', 'io.xpipe.app.core.window.AppDialog', 'io.xpipe.app.prefs.AppearanceCategory', 'io.xpipe.app.prefs.EditorCategory', 'io.xpipe.app.prefs.TerminalCategory', 'io.xpipe.app.util.OptionsBuilder', 'javafx.scene.layout.Region'] |
| 概述说明 | 首次启动时显示配置对话框，包含语言、主题、终端和编辑器选项，宽度650，带确定按钮。 |

# 说明

这是一个名为AppConfigurationDialog的类，包含一个静态方法showIfNeeded。该方法在应用首次启动时显示配置对话框。首先检查是否初始启动，若非则直接返回。然后构建包含语言选择、主题选择、终端选择和编辑器选择的选项面板，并设置样式类。将选项面板放入滚动容器，设置最小和首选宽度为650。最后创建模态对话框，添加确认按钮并显示。整个过程用于首次启动时的用户偏好设置。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppConfigurationDialog | class | 首次启动时显示配置对话框，包含语言、主题、终端和编辑器选项，宽度650，带确定按钮。 |



## 类 AppConfigurationDialog

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppConfigurationDialog |
| 说明 | 首次启动时显示配置对话框，包含语言、主题、终端和编辑器选项，宽度650，带确定按钮。 |


### UML类图

```mermaid
classDiagram
    class AppConfigurationDialog {
        +showIfNeeded()
    }

    class AppProperties {
        +isInitialLaunch() boolean
    }

    class OptionsBuilder {
        +sub(Object category) OptionsBuilder
        +buildComp() Object
    }

    class ScrollComp {
        +ScrollComp(Object content)
        +apply(Consumer~Structure~) void
        +minWidth(double) void
        +prefWidth(double) void
    }

    class ModalOverlay {
        +of(String id, Object content) ModalOverlay
        +addButton(ModalButton) void
    }

    class ModalButton {
        +ok() ModalButton
    }

    class AppDialog {
        +show(ModalOverlay) void
    }

    class AppearanceCategory {
        <<Interface>>
        +languageChoice() Object
        +themeChoice() Object
    }

    class TerminalCategory {
        <<Interface>>
        +terminalChoice() Object
    }

    class EditorCategory {
        <<Interface>>
        +editorChoice() Object
    }

    AppConfigurationDialog --> AppProperties : 检查首次启动
    AppConfigurationDialog --> OptionsBuilder : 构建配置选项
    AppConfigurationDialog --> ScrollComp : 创建滚动容器
    AppConfigurationDialog --> ModalOverlay : 创建模态窗口
    OptionsBuilder --> AppearanceCategory : 添加语言/主题选项
    OptionsBuilder --> TerminalCategory : 添加终端选项
    OptionsBuilder --> EditorCategory : 添加编辑器选项
    ModalOverlay --> ModalButton : 添加确认按钮
    ModalOverlay --> AppDialog : 显示对话框
```

该代码实现了一个应用配置对话框的显示逻辑，当检测到应用首次启动时，会构建包含语言、主题、终端和编辑器选项的配置界面，并封装在可滚动的模态窗口中显示。类图展示了核心组件间的协作关系：AppConfigurationDialog作为入口，通过AppProperties判断启动状态，使用建造者模式组合各类配置选项，最终通过ModalOverlay和AppDialog实现交互式弹窗。各配置选项通过接口隔离实现模块化扩展。


### 内部方法调用关系图

```mermaid
graph TD
    A["方法: showIfNeeded()"]
    B["条件判断: !AppProperties.get().isInitialLaunch()"]
    C["返回: return"]
    D["创建OptionsBuilder对象"]
    E["添加子项: languageChoice()"]
    F["添加子项: themeChoice()"]
    G["添加子项: terminalChoice()"]
    H["添加子项: editorChoice()"]
    I["构建组件: buildComp()"]
    J["设置样式类: styleClass('initial-setup')"]
    K["设置样式类: styleClass('prefs-container')"]
    L["创建ScrollComp对象"]
    M["应用高度绑定: apply()"]
    N["设置最小宽度: minWidth(650)"]
    O["设置首选宽度: prefWidth(650)"]
    P["创建ModalOverlay对象"]
    Q["添加按钮: addButton(ModalButton.ok())"]
    R["显示对话框: AppDialog.show(modal)"]

    A --> B
    B --"条件成立"--> C
    B --"条件不成立"--> D
    D --> E
    D --> F
    D --> G
    D --> H
    E --> I
    F --> I
    G --> I
    H --> I
    I --> J
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
    O --> P
    P --> Q
    Q --> R
```

这段代码流程图展示了AppConfigurationDialog类的showIfNeeded()方法的完整执行流程。该方法首先检查应用是否为首次启动，如果不是则直接返回；如果是则构建一个包含语言选择、主题选择、终端选择和编辑器选择的配置界面，设置样式和尺寸后创建模态对话框并显示。流程从条件判断开始，分支出两个路径，然后通过一系列UI组件的创建和配置，最终完成对话框的展示。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| showIfNeeded | void | 首次启动时显示语言、主题、终端和编辑器选项的配置对话框。 |




