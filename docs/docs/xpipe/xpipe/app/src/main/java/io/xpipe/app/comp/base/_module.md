# 基础信息

|      |      |
|------|------|
| 名称 | base |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/base |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.comp.base |
| 概述说明 | 多个JavaFX组件类，包括弹出菜单按钮、字体图标、文本区域、文件拖放、模态对话框、列表选择器等UI控件，实现各种交互功能。 |

# 说明

```markdown
## 概述

该代码模块是一个基于JavaFX的UI组件库，提供了一系列可复用的基础组件和复合组件，用于构建现代化的桌面应用程序界面。模块采用响应式设计理念，通过属性绑定和观察者模式实现数据与UI的自动同步。主要特点包括：

1. **组件化架构**：所有组件均继承自基础Comp或SimpleComp类，遵循统一的创建和生命周期管理规范
2. **响应式数据绑定**：广泛使用ObservableValue和Property实现数据驱动UI更新
3. **丰富的UI控件**：包含按钮、输入框、选择器、列表、弹窗等50+基础组件
4. **复合布局组件**：提供多种布局容器（垂直、水平、堆叠、锚点等）和复杂组合组件
5. **主题与国际化支持**：内置暗色/亮色主题切换和国际化文本处理能力
6. **交互增强**：支持快捷键、工具提示、文件拖放、模态对话框等交互模式

## 主要业务场景

1. **表单与数据输入**
   - 文本输入：TextFieldComp、TextAreaComp、SecretFieldComp、LazyTextFieldComp
   - 数值输入：IntFieldComp、IntComboFieldComp
   - 选择控件：ChoiceComp、ToggleGroupComp、ToggleSwitchComp、ListSelectorComp
   - 复合输入：ContextualFileReferenceChoiceComp、ComboTextFieldComp

2. **导航与布局**
   - 主框架：AppLayoutComp、AppMainWindowContentComp
   - 侧边栏：SideMenuBarComp
   - 分栏布局：LeftSplitPaneComp
   - 滚动容器：ScrollComp
   - 动态布局：MultiContentComp、StackComp、AnchorComp

3. **对话框与提示**
   - 模态系统：ModalOverlay、ModalOverlayComp、ModalOverlayStackComp
   - 按钮组件：ModalButton、ButtonComp、IconButtonComp、TileButtonComp
   - 工具提示：TooltipHelper

4. **内容展示**
   - 图文混排：LabelComp、FontIconComp、PrettyImageComp
   - Markdown渲染：MarkdownComp、MarkdownEditorComp
   - 列表展示：ListBoxViewComp、VerticalComp、HorizontalComp
   - 状态指示：LoadingOverlayComp、CountComp

5. **特殊交互**
   - 弹出菜单：PopupMenuButtonComp、DropdownComp
   - 文件处理：FileDropOverlayComp、IntegratedTextAreaComp
   - 选项配置：OptionsComp、SimpleTitledPaneComp
   - 引导界面：IntroComp、IntroListComp

该组件库适用于需要构建复杂、交互丰富的企业级桌面应用程序，特别是数据管理、配置工具和开发工具类软件。通过组合这些基础组件，可以快速搭建出功能完整、体验一致的应用程序界面。
```


### 包内部结构视图

```mermaid
graph TD
    base --> PopupMenuButtonComp.java
    base --> FontIconComp.java
    base --> IntegratedTextAreaComp.java
    base --> FileDropOverlayComp.java
    base --> AppMainWindowContentComp.java
    base --> ModalOverlay.java
    base --> LazyTextFieldComp.java
    base --> MarkdownEditorComp.java
    base --> IntroComp.java
    base --> PrettyImageComp.java
    base --> TextFieldComp.java
    base --> SideMenuBarComp.java
    base --> AppLayoutComp.java
    base --> ListBoxViewComp.java
    base --> VerticalComp.java
    base --> ToggleGroupComp.java
    base --> ChoiceComp.java
    base --> LeftSplitPaneComp.java
    base --> DialogComp.java
    base --> PrettyImageHelper.java
    base --> FilterComp.java
    base --> ModalOverlayComp.java
    base --> CountComp.java
    base --> TooltipHelper.java
    base --> TextAreaComp.java
    base --> IntFieldComp.java
    base --> ModalOverlayStackComp.java
    base --> DelayedInitComp.java
    base --> ModalOverlayContentComp.java
    base --> LabelComp.java
    base --> ToggleSwitchComp.java
    base --> ListSelectorComp.java
    base --> ContextualFileReferenceSync.java
    base --> LoadingOverlayComp.java
    base --> StackComp.java
    base --> ChoicePaneComp.java
    base --> ModalButton.java
    base --> HorizontalComp.java
    base --> InputGroupComp.java
    base --> ScrollComp.java
    base --> SecretFieldComp.java
    base --> IntComboFieldComp.java
    base --> ButtonComp.java
    base --> IconButtonComp.java
    base --> OptionsComp.java
    base --> MarkdownComp.java
    base --> ComboTextFieldComp.java
    base --> ContextualFileReferenceChoiceComp.java
    base --> AnchorComp.java
    base --> SimpleTitledPaneComp.java
    base --> ToolbarComp.java
    base --> TileButtonComp.java
    base --> IntroListComp.java
    base --> MultiContentComp.java
    base --> DropdownComp.java
```

该流程图展示了一个名为"base"的目录下包含的46个Java组件文件。这些组件涵盖了UI交互的各种功能模块，包括按钮、对话框、文本编辑、图像显示、布局管理等。每个文件都直接隶属于base目录，没有更深层次的嵌套结构，所有组件都处于同一层级，共同构成了一个完整的UI组件库。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [IntFieldComp.java](IntFieldComp.md) | file | 整型输入框组件，支持属性绑定、范围限制和输入验证。 |
| [TextAreaComp.java](TextAreaComp.md) | file | 文本区域组件类，含值属性和懒加载功能，支持双向绑定和布局控制。 |
| [LazyTextFieldComp.java](LazyTextFieldComp.md) | file | 懒加载文本框组件，支持回车确认、ESC取消、失焦保存，绑定属性值同步更新。 |
| [ModalOverlay.java](ModalOverlay.md) | file | ModalOverlay类用于创建模态对话框，支持标题、内容、按钮等配置，提供显示、隐藏和关闭功能。 |
| [AppMainWindowContentComp.java](AppMainWindowContentComp.md) | file | 应用主窗口内容组件，含加载动画、版本显示和模态叠加层处理。 |
| [FileDropOverlayComp.java](FileDropOverlayComp.md) | file | 文件拖放覆盖组件，支持文件拖拽处理与回调。 |
| [IntegratedTextAreaComp.java](IntegratedTextAreaComp.md) | file | 集成文本区域组件，支持脚本编辑、文件拖放和外部编辑器打开。 |
| [FontIconComp.java](FontIconComp.md) | file | FontIconComp类：使用FontIcon和StackPane创建UI组件，支持动态更新图标。 |
| [PopupMenuButtonComp.java](PopupMenuButtonComp.md) | file | 弹出菜单按钮组件，绑定名称和内容，支持懒加载。 |
| [ToggleGroupComp.java](ToggleGroupComp.md) | file | 这是一个JavaFX的ToggleGroupComp类，用于创建水平排列的切换按钮组，支持动态更新选项和样式管理。 |
| [VerticalComp.java](VerticalComp.md) | file | 垂直布局组件类，支持动态条目更新和间距设置。 |
| [ListBoxViewComp.java](ListBoxViewComp.md) | file | 列表视图组件，支持动态刷新、滚动条控制和可见性管理。 |
| [AppLayoutComp.java](AppLayoutComp.md) | file | AppLayoutComp类实现布局组件，包含侧边栏和多内容切换功能，处理选中项监听和快捷键事件。 |
| [SideMenuBarComp.java](SideMenuBarComp.md) | file | 侧边栏组件类，含菜单项、更新按钮和队列管理功能。 |
| [TextFieldComp.java](TextFieldComp.md) | file | 文本框组件类，支持懒更新和值同步，继承Comp基类。 |
| [PrettyImageComp.java](PrettyImageComp.md) | file | PrettyImageComp类：基于ObservableValue创建自适应图片组件，支持暗黑模式切换。 |
| [IntroComp.java](IntroComp.md) | file | IntroComp类：带标题、描述、图标和按钮的UI组件。 |
| [MarkdownEditorComp.java](MarkdownEditorComp.md) | file | Markdown编辑器组件类，包含编辑按钮和显示区域。 |
| [TooltipHelper.java](TooltipHelper.md) | file | TooltipHelper类提供创建带快捷键提示的自定义Tooltip方法，支持文本绑定和样式设置。 |
| [CountComp.java](CountComp.md) | file | CountComp类继承Comp，使用ObservableIntegerValue和Function创建带绑定的Label组件。 |
| [ModalOverlayComp.java](ModalOverlayComp.md) | file | 模态覆盖组件类，管理背景与弹窗内容，支持动画、焦点控制及按钮交互。 |
| [FilterComp.java](FilterComp.md) | file | FilterComp组件，绑定文本属性，实现搜索框功能，含清除和图标切换逻辑。 |
| [PrettyImageHelper.java](PrettyImageHelper.md) | file | PrettyImageHelper类提供图像处理功能，支持SVG/PNG格式检查、缩放和固定尺寸显示。 |
| [DialogComp.java](DialogComp.md) | file | 抽象类DialogComp扩展Comp，实现对话框布局，含导航按钮和内容区域。 |
| [LeftSplitPaneComp.java](LeftSplitPaneComp.md) | file | 左分栏面板组件，含左右区域和宽度调整功能。 |
| [ChoiceComp.java](ChoiceComp.md) | file | ChoiceComp类：泛型下拉框组件，支持属性绑定、动态范围更新和国际化。 |
| [LoadingOverlayComp.java](LoadingOverlayComp.md) | file | 加载覆盖组件，绑定进度条和显示状态，支持无进度模式。 |
| [ContextualFileReferenceSync.java](ContextualFileReferenceSync.md) | file | 类ContextualFileReferenceSync用于同步文件引用，包含路径、用户过滤和目标位置处理，提供获取现有文件列表方法。 |
| [ListSelectorComp.java](ListSelectorComp.md) | file | 列表选择组件，支持多选、禁用项和全选功能，基于JavaFX实现。 |
| [ToggleSwitchComp.java](ToggleSwitchComp.md) | file | 切换开关组件类，含选中状态、名称和图形属性，支持键盘操作和状态同步。 |
| [LabelComp.java](LabelComp.md) | file | LabelComp类继承Comp，封装Label组件，支持动态文本和图形更新。 |
| [ModalOverlayContentComp.java](ModalOverlayContentComp.md) | file | 抽象类ModalOverlayContentComp扩展SimpleComp，含模态覆盖层设置、关闭方法和忙碌状态返回值。 |
| [DelayedInitComp.java](DelayedInitComp.md) | file | 延迟初始化组件，条件满足时加载子组件到堆栈面板。 |
| [ModalOverlayStackComp.java](ModalOverlayStackComp.md) | file | ModalOverlayStackComp类管理模态覆盖层堆栈，处理背景和覆盖层列表。 |
| [IconButtonComp.java](IconButtonComp.md) | file | 图标按钮组件类，支持动态图标和点击事件。 |
| [ButtonComp.java](ButtonComp.md) | file | 按钮组件类，含名称、图标和监听器，动态更新UI。 |
| [IntComboFieldComp.java](IntComboFieldComp.md) | file | 整数组合框组件，支持预定义值和负数输入。 |
| [ScrollComp.java](ScrollComp.md) | file | 滚动组件类，包含内容区域和垂直滚动条控制逻辑。 |
| [InputGroupComp.java](InputGroupComp.md) | file | 输入组件组类，包含条目列表，支持间距设置和居中布局。 |
| [HorizontalComp.java](HorizontalComp.md) | file | 水平布局组件类，支持动态条目更新和间距设置。 |
| [ModalButton.java](ModalButton.md) | file | ModalButton类定义模态框按钮，含key、action等属性，提供多种静态方法创建预设按钮。 |
| [ChoicePaneComp.java](ChoicePaneComp.md) | file | JavaFX组件类，管理下拉选择框及动态内容显示。 |
| [MultiContentComp.java](MultiContentComp.md) | file | 多内容组件类，管理动态显示区域，支持日志跟踪和状态订阅。 |
| [IntroListComp.java](IntroListComp.md) | file | IntroListComp类继承SimpleComp，接收IntroComp列表并创建垂直布局组件，设置间距、尺寸和边距后返回。 |
| [TileButtonComp.java](TileButtonComp.md) | file | TileButtonComp类：带图标、名称、描述的按钮组件，支持自定义右侧内容和点击事件。 |
| [ToolbarComp.java](ToolbarComp.md) | file | 工具栏组件类，继承Comp，管理条目列表，动态更新UI。 |
| [SimpleTitledPaneComp.java](SimpleTitledPaneComp.md) | file | 可折叠标题面板组件，绑定名称和内容，支持样式控制。 |
| [AnchorComp.java](AnchorComp.md) | file | Java类AnchorComp继承Comp，用AnchorPane布局管理子组件列表。 |
| [ComboTextFieldComp.java](ComboTextFieldComp.md) | file | 组合文本框组件，支持预定义值和自定义单元格，绑定属性值并处理键盘事件。 |
| [MarkdownComp.java](MarkdownComp.md) | file | MarkdownComp类：将Markdown转换为HTML并在WebView中显示，支持主题切换和链接处理。 |
| [DropdownComp.java](DropdownComp.md) | file | 下拉菜单组件类，包含按钮和菜单项列表，绑定可见性并设置图标样式。 |
| [ContextualFileReferenceChoiceComp.java](ContextualFileReferenceChoiceComp.md) | file | 文件引用选择组件，支持浏览、同步和Git共享功能。 |
| [OptionsComp.java](OptionsComp.md) | file | OptionsComp类用于创建垂直布局面板，管理条目列表，支持名称、描述和组件显示，包含样式和交互逻辑。 |
| [SecretFieldComp.java](SecretFieldComp.md) | file | SecretFieldComp组件：处理密码输入，支持复制和自定义按钮。 |
| [StackComp.java](StackComp.md) | file | 堆叠组件类，包含子组件列表，创建居中堆叠布局。 |


