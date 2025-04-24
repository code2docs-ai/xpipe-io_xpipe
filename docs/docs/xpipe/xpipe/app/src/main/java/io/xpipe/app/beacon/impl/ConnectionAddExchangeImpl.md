# 基础信息

|      |      |
|------|------|
| 名称 | ConnectionAddExchangeImpl |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/beacon/impl/ConnectionAddExchangeImpl.java |
| 包名 | io.xpipe.app.beacon.impl |
| 依赖项 | ['io.xpipe.app.issue.ErrorEvent', 'io.xpipe.app.storage.DataStorage', 'io.xpipe.app.storage.DataStoreEntry', 'io.xpipe.beacon.BeaconClientException', 'io.xpipe.beacon.api.ConnectionAddExchange', 'io.xpipe.core.util.ValidationException', 'com.sun.net.httpserver.HttpExchange'] |
| 概述说明 | 处理HTTP请求，管理数据存储条目，验证并返回连接响应。 |

# 说明

ConnectionAddExchangeImpl类继承自ConnectionAddExchange，重写了handle方法处理HTTP交换请求。该方法首先检查数据存储中是否存在指定数据或名称的条目，若存在则更新数据并返回连接响应。若不存在且指定分类ID无效，抛出异常。接着创建新数据条目，设置分类ID（如有），并尝试添加到存储中，期间进行验证处理，捕获验证异常或堆栈溢出错误。最后确保条目添加完成并分配分类，返回包含新条目UUID的响应。此外，重写getSynchronizationObject方法返回数据存储实例。整个过程包含数据查找、验证、异常处理和分类管理。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ConnectionAddExchangeImpl | class | 处理HTTP请求，检查数据存储，验证并添加新条目，返回连接UUID。 |



## 类 ConnectionAddExchangeImpl

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ConnectionAddExchangeImpl |
| 说明 | 处理HTTP请求，检查数据存储，验证并添加新条目，返回连接UUID。 |


### UML类图

```mermaid
classDiagram
    class ConnectionAddExchangeImpl {
        +handle(HttpExchange exchange, Request msg) Object
        +getSynchronizationObject() Object
    }
    
    class ConnectionAddExchange {
        <<Interface>>
        +handle(HttpExchange exchange, Request msg) Object
        +getSynchronizationObject() Object
    }
    
    class DataStorage {
        <<Singleton>>
        +get() DataStorage
        +getStoreEntryIfPresent(Object data, boolean b) Optional~DataStoreEntry~
        +getStoreCategoryIfPresent(Object category) Optional~StoreCategory~
        +addStoreEntryInProgress(DataStoreEntry entry)
        +removeStoreEntryInProgress(DataStoreEntry entry)
        +addStoreEntryIfNotPresent(DataStoreEntry entry)
        +moveEntryToCategory(DataStoreEntry entry, StoreCategory category)
    }
    
    class DataStoreEntry {
        +createNew(String name, Object data) DataStoreEntry
        +setStoreInternal(Object data, boolean b)
        +getUuid() Object
        +setCategoryUuid(Object category)
        +validateOrThrow()
    }
    
    class Request {
        +getData() Object
        +getName() String
        +getCategory() Object
        +getValidate() boolean
    }
    
    class Response {
        +builder() Builder
    }
    
    class Builder {
        +connection(Object uuid) Builder
        +build() Response
    }
    
    class ErrorEvent {
        <<Utility>>
        +expected(Throwable ex)
    }
    
    ConnectionAddExchangeImpl --|> ConnectionAddExchange : 实现
    ConnectionAddExchangeImpl --> DataStorage : 使用
    ConnectionAddExchangeImpl --> DataStoreEntry : 创建
    ConnectionAddExchangeImpl --> Request : 处理
    ConnectionAddExchangeImpl --> Response : 返回
    DataStoreEntry --> ValidationException : 可能抛出
    DataStoreEntry --> StoreCategory : 关联
    DataStorage --> StoreCategory : 管理
```

```mermaid
flowchart TD
    A["开始handle()"] --> B["查找数据(found = DataStorage.getStoreEntryIfPresent)"]
    B --> C{found为空?}
    C -->|是| D["按名称查找(found = DataStorage.getStoreEntryIfPresent)"]
    C -->|否| E["更新数据(found.setStoreInternal)"]
    D --> F{found存在?}
    F -->|是| E
    E --> G["返回响应(Response.builder)"]
    F -->|否| H{"分类存在且无效?"}
    H -->|是| I["抛出BeaconClientException"]
    H -->|否| J["创建新条目(DataStoreEntry.createNew)"]
    J --> K{"分类存在?"}
    K -->|是| L["设置分类(entry.setCategoryUuid)"]
    K -->|否| M["添加条目到临时存储(DataStorage.addStoreEntryInProgress)"]
    L --> M
    M --> N{"需要验证?"}
    N -->|是| O["执行验证(entry.validateOrThrow)"]
    O --> P{验证异常?}
    P -->|ValidationException| Q["记录预期错误(ErrorEvent.expected)"]
    P -->|StackOverflowError| Q
    Q --> R["重新抛出异常"]
    N -->|否| S["从临时存储移除(DataStorage.removeStoreEntryInProgress)"]
    O --> S
    S --> T["持久化存储(DataStorage.addStoreEntryIfNotPresent)"]
    T --> U{"分类存在?"}
    U -->|是| V["移动条目到分类(DataStorage.moveEntryToCategory)"]
    U -->|否| W["返回响应(Response.builder)"]
    V --> W
```

这段代码实现了一个连接添加交换处理器，主要处理HTTP交换请求，通过数据存储管理数据条目。类图展示了核心类关系，包括单例数据存储、数据条目、请求响应模型等。流程图详细描述了处理逻辑：先尝试查找现有数据，不存在则创建新条目，处理验证和分类关联，最后返回包含UUID的响应。特别注意了异常处理和临时存储管理机制。


### 内部方法调用关系图

```mermaid
graph TD
    A["ConnectionAddExchangeImpl.handle"]
    B["DataStorage.get().getStoreEntryIfPresent(msg.getData(), false)"]
    C["found.isEmpty()?"]
    D["DataStorage.get().getStoreEntryIfPresent(msg.getName())"]
    E["found.isPresent()?"]
    F["found.get().setStoreInternal(data, true)"]
    G["返回Response.builder().connection(found.get().getUuid()).build()"]
    H["msg.getCategory() != null且getStoreCategoryIfPresent为空?"]
    I["抛出BeaconClientException"]
    J["DataStoreEntry.createNew(msg.getName(), msg.getData())"]
    K["msg.getCategory() != null?"]
    L["entry.setCategoryUuid(msg.getCategory())"]
    M["DataStorage.get().addStoreEntryInProgress(entry)"]
    N["msg.getValidate()?"]
    O["entry.validateOrThrow()"]
    P["捕获ValidationException/StackOverflowError"]
    Q["ErrorEvent.expected(ex)"]
    R["抛出异常"]
    S["DataStorage.get().removeStoreEntryInProgress(entry)"]
    T["DataStorage.get().addStoreEntryIfNotPresent(entry)"]
    U["msg.getCategory() != null?"]
    V["DataStorage.moveEntryToCategory(entry, getStoreCategoryIfPresent)"]
    W["返回Response.builder().connection(entry.getUuid()).build()"]

    A --> B
    B --> C
    C -- 是 --> D
    C -- 否 --> E
    D --> E
    E -- 是 --> F
    F --> G
    E -- 否 --> H
    H -- 是 --> I
    H -- 否 --> J
    J --> K
    K -- 是 --> L
    K -- 否 --> M
    L --> M
    M --> N
    N -- 是 --> O
    O --> S
    N -- 否 --> S
    O -. 异常 .-> P
    P --> Q
    Q --> R
    S --> T
    T --> U
    U -- 是 --> V
    V --> W
    U -- 否 --> W
```

这段流程图描述了ConnectionAddExchangeImpl类中handle方法的完整执行逻辑。该方法首先尝试通过数据或名称查找现有存储条目，若存在则更新数据并返回响应；否则会检查分类有效性，创建新条目并进行验证处理，最后将条目添加到存储系统并可能关联到指定分类。整个过程包含异常处理和资源清理，最终返回新建条目的UUID响应。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getSynchronizationObject | Object | 重写方法，返回DataStorage单例对象。 |
| handle | Object | 处理HTTP请求，查询或创建数据存储条目，验证并返回响应。 |




