# 基础信息

|      |      |
|------|------|
| 名称 | AppCache |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/core/AppCache.java |
| 包名 | io.xpipe.app.core |
| 依赖项 | ['io.xpipe.app.issue.ErrorEvent', 'io.xpipe.core.util.JacksonMapper', 'com.fasterxml.jackson.databind.ObjectMapper', 'lombok.Getter', 'lombok.Setter', 'org.apache.commons.io.FileUtils', 'java.io.IOException', 'java.nio.file.Files', 'java.nio.file.Path', 'java.time.Instant', 'java.util.Optional', 'java.util.function.Supplier'] |
| 概述说明 | AppCache类提供静态方法管理缓存文件，支持清除、读写和查询修改时间。 |

# 说明

这是一个名为AppCache的Java工具类，用于管理基于文件的缓存系统。它提供了静态方法来实现缓存操作，包括设置基础路径、清理缓存、读写缓存数据以及获取文件修改时间。类中使用Path处理文件路径，通过Jackson库实现对象序列化。主要功能包括：清除全部或指定键的缓存；获取非空缓存对象或布尔值，若不存在则返回默认值；更新指定键的缓存值；获取缓存文件的最后修改时间。所有操作都包含异常处理，通过ErrorEvent记录错误并静默失败。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AppCache | class | AppCache类提供静态方法管理缓存文件，支持读写、清除和获取修改时间。 |



## 类 AppCache

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AppCache |
| 说明 | AppCache类提供静态方法管理缓存文件，支持读写、清除和获取修改时间。 |


### UML类图

```mermaid
classDiagram
    class AppCache {
        -Path basePath
        +static Path getBasePath()
        +static void setBasePath(Path basePath)
        -static Path getPath(String key)
        +static void clear()
        +static void clear(String key)
        +static ~T~ getNonNull(String key, Class<?> type, Supplier~T~ notPresent) T
        +static boolean getBoolean(String key, boolean notPresent)
        +static ~T~ update(String key, T val) void
        +static Optional~Instant~ getModifiedTime(String key)
    }

    class ErrorEvent {
        +static ErrorEvent fromThrowable(Throwable t)
        +static ErrorEvent fromThrowable(String msg, Throwable t)
        +ErrorEvent omitted(boolean omitted)
        +ErrorEvent build()
        +void handle()
    }

    class JacksonMapper {
        +static ObjectMapper getDefault()
    }

    AppCache --> ErrorEvent : "异常处理"
    AppCache --> JacksonMapper : "JSON序列化/反序列化"
    AppCache --> FileUtils : "文件操作"
    AppCache --> Files : "文件系统操作"
```

类图描述：
AppCache是一个提供缓存功能的工具类，主要包含静态方法用于管理基于文件的缓存数据。它通过JacksonMapper处理JSON序列化，使用FileUtils和Files进行文件操作，并依赖ErrorEvent处理异常。核心功能包括缓存清理（clear）、数据存取（getNonNull/getBoolean/update）以及获取修改时间（getModifiedTime）。类设计采用静态方法模式，通过路径解析和类型检查确保数据安全，异常处理机制完善，适合需要持久化缓存的场景。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AppCache"]
    B["静态属性: Path basePath"]
    C["私有方法: getPath(String key)"]
    D["公共方法: clear()"]
    E["公共方法: clear(String key)"]
    F["泛型方法: getNonNull(String key, Class<?> type, Supplier<T> notPresent)"]
    G["公共方法: getBoolean(String key, boolean notPresent)"]
    H["泛型方法: update(String key, T val)"]
    I["公共方法: getModifiedTime(String key)"]
    J["异常处理: ErrorEvent.fromThrowable()"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A -.-> J

    D --> C1["检查路径存在"] -->|否| C2["直接返回"]
    C1 -->|是| C3["调用FileUtils.cleanDirectory"]
    C3 --> C4["异常处理"] --> J

    E --> E1["调用getPath"] --> E2["检查路径存在"] -->|是| E3["调用FileUtils.deleteQuietly"]
    E2 -->|否| E4["结束"]

    F --> F1["调用getPath"] --> F2["检查路径存在"] -->|是| F3["读取JSON树"]
    F2 -->|否| F9["返回notPresent"]
    F3 --> F4["检查树有效性"] -->|无效| F5["删除文件并返回notPresent"]
    F4 -->|有效| F6["类型转换"] --> F7["验证类型"] -->|失败| F5
    F7 -->|成功| F8["返回结果"]
    F3 --> F10["异常处理"] --> J --> F5

    G --> G1["调用getPath"] --> G2["检查路径存在"] -->|是| G3["读取JSON树"]
    G2 -->|否| G7["返回默认值"]
    G3 --> G4["检查布尔类型"] -->|无效| G5["删除文件并返回默认值"]
    G4 -->|有效| G6["返回布尔值"]
    G3 --> G8["异常处理"] --> J --> G5

    H --> H1["调用getPath"] --> H2["创建父目录"] --> H3["写入JSON数据"]
    H3 --> H4["异常处理"] --> J

    I --> I1["调用getPath"] --> I2["检查路径存在"] -->|是| I3["获取修改时间"]
    I2 -->|否| I5["返回空Optional"]
    I3 --> I4["转换为Instant"]
    I3 --> I6["异常处理"] --> J --> I5
```

这段代码实现了一个基于文件系统的应用缓存系统，主要功能包括缓存清理、数据读写、类型安全检查和修改时间获取。流程图展示了8个核心方法的调用关系和异常处理逻辑，其中getNonNull()和getBoolean()方法包含完整的JSON解析和类型验证流程，所有方法都通过统一的ErrorEvent机制处理异常。缓存文件存储在basePath指定的目录下，每个键对应一个.cache后缀的文件。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| basePath | Path | 静态路径变量basePath，带Getter和Setter注解。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| clear | void | 静态方法clear删除指定键对应的文件。 |
| getPath | Path | 私有方法，通过键名生成缓存文件路径。 |
| clear | void | 静态方法clear检查路径存在后清空目录，异常时处理错误。 |
| getNonNull | T | 从指定路径读取JSON文件并转换为指定类型对象，若无效则删除文件并返回默认值。 |
| getBoolean | boolean | 静态方法获取布尔值，若文件不存在或解析失败返回默认值。 |
| update | void | 静态方法更新键值数据，异常时记录错误。 |
| getModifiedTime | Optional<Instant> | 获取文件修改时间，存在则返回时间，异常或不存在返回空。 |




