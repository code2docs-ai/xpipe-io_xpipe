# 基础信息

|      |      |
|------|------|
| 名称 | AppAvCheck |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/check/AppAvCheck.java |
| 包名 | io.xpipe.app.core.check |
| 依赖项 | ['io.xpipe.app.comp.Comp', 'io.xpipe.app.comp.base.MarkdownComp', 'io.xpipe.app.comp.base.ModalButton', 'io.xpipe.app.comp.base.ModalOverlay', 'io.xpipe.app.core.AppProperties', 'io.xpipe.app.resources.AppResources', 'io.xpipe.app.util.WindowsRegistry', 'io.xpipe.core.process.OsType', 'javafx.scene.layout.Region', 'lombok.Getter', 'java.nio.file.Files', 'java.util.Optional', 'java.util.concurrent.atomic.AtomicReference'] |
| 概述说明 | 检测Windows首次启动时的杀毒软件，显示警告信息。支持Bitdefender、Malwarebytes、McAfee。 |

# 说明

该代码定义了一个名为AppAvCheck的类，用于检测Windows系统上特定杀毒软件的存在，并在首次启动时显示警告信息。类包含detect方法遍历AvType枚举检查活动杀毒软件，check方法仅在Windows首次启动时执行检测。检测到杀毒软件后会显示模态窗口，展示格式化后的警告信息。AvType枚举定义了Bitdefender、Malwarebytes和McAfee三种杀毒软件，每个类型包含名称、描述和检测活动状态的方法，通过检查Windows注册表键值判断软件是否存在。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppAvCheck | class | 检测Windows首次启动时的杀毒软件，显示警告信息。支持Bitdefender、Malwarebytes、McAfee。 |



## 类 AppAvCheck

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppAvCheck |
| 说明 | 检测Windows首次启动时的杀毒软件，显示警告信息。支持Bitdefender、Malwarebytes、McAfee。 |


### UML类图

```mermaid
classDiagram
    class AppAvCheck {
        +static Optional~AvType~ detect()
        +static void check()
    }

    class AvType {
        <<enumeration>>
        -String name
        +String getName()
        +abstract String getDescription()
        +abstract boolean isActive()
        +BITDEFENDER
        +MALWAREBYTES
        +MCAFEE
    }

    class WindowsRegistry {
        <<Interface>>
        +static WindowsRegistry local()
        +boolean valueExists(HKEY hkey, String path, String value)
    }

    class ModalOverlay {
        +static ModalOverlay of(Region content)
        +void addButton(ModalButton button)
        +void showAndWait()
    }

    class ModalButton {
        <<enumeration>>
        +QUIT
        +OK
        +static ModalButton quit()
        +static ModalButton ok()
    }

    class MarkdownComp {
        +MarkdownComp(String text, Function~String,String~ formatter, boolean dark)
        +Region createRegion()
    }

    class AppProperties {
        +static AppProperties get()
        -boolean initialLaunch
        -String version
        +boolean isInitialLaunch()
        +String getVersion()
    }

    class OsType {
        <<enumeration>>
        +WINDOWS
        +static OsType getLocal()
    }

    AppAvCheck --> AvType : 使用
    AppAvCheck --> WindowsRegistry : 间接依赖
    AppAvCheck --> ModalOverlay : 使用
    AppAvCheck --> ModalButton : 使用
    AppAvCheck --> AppProperties : 使用
    AppAvCheck --> OsType : 使用
    AvType --> WindowsRegistry : 依赖
    ModalOverlay --> ModalButton : 组合
    ModalOverlay --> MarkdownComp : 间接依赖
```

这段代码主要实现了一个Windows平台上的杀毒软件检测功能。AppAvCheck类通过检测注册表来判断是否安装了特定杀毒软件(Bitdefender/Malwarebytes/McAfee)，如果是首次启动且在Windows平台，会显示一个包含警告信息的模态对话框。AvType枚举定义了不同杀毒软件的特性检测逻辑，WindowsRegistry接口提供了注册表操作能力，ModalOverlay负责构建和显示警告界面。整个设计采用了工厂模式、策略模式和依赖注入等设计模式，具有良好的扩展性和可维护性。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AppAvCheck"]
    B["静态方法: Optional<AvType> detect()"]
    C["静态方法: void check()"]
    D["枚举AvType"]
    E["属性: String name"]
    F["抽象方法: String getDescription()"]
    G["抽象方法: boolean isActive()"]
    H["具体枚举值: BITDEFENDER/MALWAREBYTES/MCAFEE"]
    I["构造方法: AvType(String name)"]
    J["条件检查: OsType与InitialLaunch"]
    K["调用detect()"]
    L["创建ModalOverlay"]
    M["加载Markdown内容"]
    N["添加按钮: quit/ok"]
    O["显示模态框: showAndWait"]

    A --> B
    A --> C
    A --> D
    D --> E
    D --> F
    D --> G
    D --> H
    D --> I
    C --> J
    C --> K
    C --> L
    L --> M
    L --> N
    L --> O
    H -.->|实现| F
    H -.->|实现| G
```

流程图描述：该流程图展示了AppAvCheck类的核心结构，包含检测杀毒软件的静态方法和枚举定义。主要流程从check()方法开始，先进行操作系统和首次启动条件检查，然后调用detect()遍历AvType枚举检测活动杀软，最后通过ModalOverlay展示警告信息。枚举类型定义了三种杀软的具体实现，每个枚举值需实现获取描述和检测状态的抽象方法。模态框创建过程包含Markdown内容加载和按钮添加等步骤。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| check | void | 检查首次Windows启动时是否检测到杀毒软件，若有则显示警告弹窗并提供退出或继续选项。 |
| detect | Optional<AvType> | 检测活跃AvType并返回首个匹配项，无则返回空。 |




