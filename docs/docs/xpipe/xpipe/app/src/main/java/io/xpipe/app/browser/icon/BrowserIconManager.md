# 基础信息

|      |      |
|------|------|
| 名称 | BrowserIconManager |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/browser/icon/BrowserIconManager.java |
| 包名 | io.xpipe.app.browser.icon |
| 依赖项 | ['io.xpipe.core.store.FileEntry', 'io.xpipe.core.store.FileKind'] |
| 概述说明 | BrowserIconManager类管理文件图标加载与获取，支持文件和目录类型匹配。 |

# 说明

BrowserIconManager是一个管理浏览器图标加载与获取的类。它包含一个静态布尔变量loaded标记是否已加载图标定义。loadIfNecessary方法通过同步方式确保只加载一次BrowserIconFileType和BrowserIconDirectoryType的定义。getFileIcon方法根据传入的FileEntry对象类型（文件或目录）匹配对应的图标，若未匹配则返回默认图标路径。整个过程采用线程安全设计。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| BrowserIconManager | class | BrowserIconManager类管理文件图标，按需加载并返回匹配的图标路径。 |



## 类 BrowserIconManager

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | BrowserIconManager |
| 说明 | BrowserIconManager类管理文件图标，按需加载并返回匹配的图标路径。 |


### UML类图

```mermaid
classDiagram
    class BrowserIconManager {
        -boolean loaded
        +synchronized loadIfNecessary()
        +synchronized getFileIcon(FileEntry entry) String
    }

    class BrowserIconFileType {
        +static loadDefinitions()
        +static getAll() Collection~BrowserIconFileType~
        +matches(FileEntry) boolean
        +getIcon() String
    }

    class BrowserIconDirectoryType {
        +static loadDefinitions()
        +static getAll() Collection~BrowserIconDirectoryType~
        +matches(FileEntry) boolean
        +getIcon(FileEntry) String
    }

    class FileEntry {
        +resolved() FileEntry
    }

    BrowserIconManager --> BrowserIconFileType : 调用静态方法
    BrowserIconManager --> BrowserIconDirectoryType : 调用静态方法
    BrowserIconManager --> FileEntry : 参数依赖
```

该代码展示了一个浏览器图标管理系统，BrowserIconManager通过双重检查锁模式延迟加载图标定义文件。当获取文件图标时，会根据文件类型（普通文件/目录）分别匹配BrowserIconFileType或BrowserIconDirectoryType中注册的图标规则，未匹配时返回默认图标。系统通过FileEntry对象获取文件元信息，各组件间通过静态方法调用协作，体现了线程安全的单例初始化模式。


### 内部方法调用关系图

```mermaid
graph TD
    A["类BrowserIconManager"]
    B["静态属性: boolean loaded"]
    C["静态方法: loadIfNecessary()"]
    D["静态方法: getFileIcon(FileEntry entry)"]
    E["条件判断: if (!loaded)"]
    F["调用: BrowserIconFileType.loadDefinitions()"]
    G["调用: BrowserIconDirectoryType.loadDefinitions()"]
    H["设置: loaded = true"]
    I["条件判断: if (entry == null)"]
    J["调用: entry.resolved()"]
    K["条件分支: 文件类型判断"]
    L["遍历: BrowserIconFileType.getAll()"]
    M["条件匹配: f.matches(r)"]
    N["返回: f.getIcon()"]
    O["遍历: BrowserIconDirectoryType.getAll()"]
    P["条件匹配: f.matches(r)"]
    Q["返回: f.getIcon(r)"]
    R["返回默认图标路径"]

    A --> B
    A --> C
    A --> D
    C --> E
    E -->|true| F
    E -->|true| G
    E -->|true| H
    D --> I
    I -->|false| J
    J --> K
    K -->|文件| L
    L --> M
    M -->|true| N
    K -->|目录| O
    O --> P
    P -->|true| Q
    K --> R
```

流程图描述了BrowserIconManager类的核心逻辑：通过loadIfNecessary()方法实现懒加载图标定义，getFileIcon()方法根据文件类型（普通文件/目录）匹配对应的图标。流程包含双重检查锁定的加载控制、空值保护、类型分发处理、动态匹配逻辑以及默认图标回退机制，展现了完整的图标管理决策过程。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| loaded | boolean | 私有静态布尔变量loaded |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| loadIfNecessary | void | 静态同步方法，检查未加载则加载浏览器图标定义并标记已加载。 |
| getFileIcon | String | 静态同步方法，根据文件类型返回对应图标，无则返回默认图标。 |




