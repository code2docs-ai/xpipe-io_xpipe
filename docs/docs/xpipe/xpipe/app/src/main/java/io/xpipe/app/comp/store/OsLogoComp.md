# 基础信息

|      |      |
|------|------|
| 名称 | OsLogoComp |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/comp/store/OsLogoComp.java |
| 包名 | io.xpipe.app.comp.store |
| 依赖项 | ['io.xpipe.app.comp.SimpleComp', 'io.xpipe.app.comp.base.PrettyImageHelper', 'io.xpipe.app.comp.base.StackComp', 'io.xpipe.app.resources.AppResources', 'io.xpipe.core.process.SystemState', 'io.xpipe.core.store.FileNames', 'javafx.beans.binding.Bindings', 'javafx.beans.property.SimpleObjectProperty', 'javafx.beans.value.ObservableValue', 'javafx.scene.layout.Region', 'java.nio.file.Files', 'java.util.HashMap', 'java.util.List', 'java.util.Map'] |
| 概述说明 | OsLogoComp类根据系统状态显示对应操作系统图标，默认显示Linux图标。 |

# 说明

OsLogoComp是一个用于显示操作系统图标的组件，继承自SimpleComp。它通过StoreEntryWrapper获取系统状态，并根据操作系统名称匹配对应的图标。组件包含一个静态图标映射表ICONS，首次使用时从资源目录加载符合条件的PNG文件并转换为SVG路径。主要逻辑包括：根据系统状态决定是否显示图标，若状态为SUCCESS则从wrapper获取操作系统名称并匹配对应图标，未匹配时默认返回Linux图标。组件内部使用StackComp组合SystemStateComp和PrettyImageHelper，实现状态与图标的切换显示。图标匹配支持名称模糊匹配，忽略大小写和空格差异。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| OsLogoComp | class | OsLogoComp类根据系统状态显示对应操作系统图标，默认使用Linux图标。 |



## 类 OsLogoComp

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | OsLogoComp |
| 说明 | OsLogoComp类根据系统状态显示对应操作系统图标，默认使用Linux图标。 |


### UML类图

```mermaid
classDiagram
    class SimpleComp {
        <<abstract>>
        +createSimple() Region
    }

    class OsLogoComp {
        -static final Map~String,String~ ICONS
        -static final String LINUX_DEFAULT_24
        -StoreEntryWrapper wrapper
        -ObservableValue~SystemStateComp.State~ state
        +OsLogoComp(StoreEntryWrapper wrapper)
        +OsLogoComp(StoreEntryWrapper wrapper, ObservableValue~SystemStateComp.State~ state)
        -String getImage(String name)
    }

    class StoreEntryWrapper {
        +getPersistentState() ObservableValue~PersistentState~
    }

    class SystemStateComp {
        +enum State
        +SystemStateComp(ObservableValue~State~ state)
        +hide(BooleanBinding hide) SystemStateComp
    }

    class PrettyImageHelper {
        <<static>>
        +ofFixedSize(ObservableValue~String~ img, int width, int height) PrettyImageHelper
        +visible(BooleanBinding visible) PrettyImageHelper
    }

    class StackComp {
        +StackComp(List~Region~ children)
        +createRegion() Region
    }

    SimpleComp <|-- OsLogoComp
    OsLogoComp --> StoreEntryWrapper : 依赖
    OsLogoComp --> SystemStateComp : 组合
    OsLogoComp --> PrettyImageHelper : 调用
    OsLogoComp --> StackComp : 组合
    SystemStateComp --> ObservableValue~State~ : 依赖
    PrettyImageHelper --> ObservableValue~String~ : 依赖
    StackComp --> List~Region~ : 聚合

    note for OsLogoComp "根据操作系统状态动态显示LOGO的组件\n1. 通过StoreEntryWrapper获取系统状态\n2. 使用SystemStateComp显示状态图标\n3. 通过PrettyImageHelper加载对应OS的LOGO\n4. 使用StackComp分层显示状态和LOGO"
```

这段代码实现了一个操作系统LOGO显示组件OsLogoComp，它继承自SimpleComp抽象类。该组件主要功能是根据系统状态动态显示操作系统LOGO：当状态为SUCCESS时显示对应操作系统的LOGO图标，否则显示系统状态图标。组件通过StoreEntryWrapper获取持久化状态，使用SystemStateComp处理状态显示，通过PrettyImageHelper加载LOGO图片，最后用StackComp实现分层布局。getImage()方法实现了从资源文件动态加载操作系统图标的逻辑，支持名称模糊匹配和默认图标回退机制。


### 内部方法调用关系图

```mermaid
graph TD
    A["类OsLogoComp"]
    B["继承自: SimpleComp"]
    C["静态常量: Map<String, String> ICONS"]
    D["静态常量: String LINUX_DEFAULT_24"]
    E["属性: StoreEntryWrapper wrapper"]
    F["属性: ObservableValue<SystemStateComp.State> state"]
    G["构造方法: OsLogoComp(StoreEntryWrapper wrapper)"]
    H["构造方法: OsLogoComp(StoreEntryWrapper wrapper, ObservableValue<SystemStateComp.State> state)"]
    I["重写方法: Region createSimple()"]
    J["私有方法: String getImage(String name)"]
    K["创建ObjectBinding: img"]
    L["创建BooleanBinding: hide"]
    M["创建StackComp组合组件"]
    N["调用SystemStateComp"]
    O["调用PrettyImageHelper"]
    P["加载图标资源逻辑"]
    Q["图标匹配逻辑"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    I --> K
    I --> L
    I --> M
    M --> N
    M --> O
    I --> J
    J --> P
    J --> Q
    P -->|"Files.list()"| C
    Q -->|"stream().filter()"| C
```

流程图描述：该流程图展示了OsLogoComp类的完整结构，从继承关系到关键方法调用链。核心流程包含两个构造方法、重写的createSimple()方法实现，以及图标加载逻辑getImage()。createSimple()方法通过绑定机制动态生成界面元素，结合SystemStateComp状态组件和PrettyImageHelper图像组件。getImage()方法实现了图标资源的延迟加载和智能匹配机制，包含文件系统扫描和名称模糊匹配逻辑。整体设计体现了响应式编程思想，通过数据绑定实现UI自动更新。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| LINUX_DEFAULT_24 = "linux-24.png" | String | Linux默认24位图文件名常量。 |
| state | ObservableValue<SystemStateComp.State> | 私有不可变状态观察值，类型为SystemStateComp.State。 |
| wrapper | StoreEntryWrapper | 私有存储条目包装器实例。 |
| ICONS = new HashMap<>() | Map<String, String> | 私有静态常量映射表ICONS，键值均为字符串。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| createSimple | Region | 创建区域：根据状态和持久状态生成图像，隐藏逻辑控制显示。 |
| getImage | String | 根据名称获取对应图标路径，优先匹配关键词，默认返回Linux图标。 |




