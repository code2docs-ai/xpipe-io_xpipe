# 基础信息

|      |      |
|------|------|
| 名称 | ConnectionInfoExchangeImpl |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/beacon/impl/ConnectionInfoExchangeImpl.java |
| 包名 | io.xpipe.app.beacon.impl |
| 依赖项 | ['io.xpipe.app.storage.DataStorage', 'io.xpipe.beacon.BeaconClientException', 'io.xpipe.beacon.api.ConnectionInfoExchange', 'io.xpipe.core.store.StorePath', 'com.sun.net.httpserver.HttpExchange', 'org.apache.commons.lang3.ClassUtils', 'java.util.ArrayList', 'java.util.UUID', 'java.util.stream.Collectors'] |
| 概述说明 | 处理HTTP请求，获取连接信息并构建响应列表。 |

# 说明

ConnectionInfoExchangeImpl类继承ConnectionInfoExchange，重写handle方法处理HTTP请求。该方法遍历请求中的UUID列表，从DataStorage获取对应连接信息，构造包含最后修改时间、使用时间、连接UUID、分类路径、原始数据等信息的InfoResponse对象列表，最终返回包含这些信息的Response对象。此外，重写getSynchronizationObject方法返回DataStorage实例作为同步对象。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ConnectionInfoExchangeImpl | class | 处理HTTP请求，获取连接信息并构建响应列表。 |



## 类 ConnectionInfoExchangeImpl

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ConnectionInfoExchangeImpl |
| 说明 | 处理HTTP请求，获取连接信息并构建响应列表。 |


### UML类图

```mermaid
classDiagram
    class ConnectionInfoExchangeImpl {
        +Object handle(HttpExchange exchange, Request msg) throws BeaconClientException
        +Object getSynchronizationObject()
    }
    class ConnectionInfoExchange {
        <<Interface>>
    }
    class DataStorage {
        +get() DataStorage
        +getStoreEntryIfPresent(UUID uuid) Optional~StoreEntry~
        +getStoreCategoryIfPresent(UUID uuid) Optional~StoreCategory~
        +getStorePath(StoreEntry e) StorePath
        +getStorePath(StoreCategory category) StorePath
    }
    class StoreEntry {
        -UUID uuid
        -UUID categoryUuid
        -long lastModified
        -long lastUsed
        -Provider provider
        -Map~String, Object~ store
        -Map~String, Object~ storeCache
        -Object storePersistentState
        +getUuid() UUID
        +getCategoryUuid() UUID
        +getLastModified() long
        +getLastUsed() long
        +getProvider() Provider
        +getStore() Map~String, Object~
        +getStoreCache() Map~String, Object~
        +getStorePersistentState() Object
    }
    class StoreCategory {
        <<Interface>>
    }
    class StorePath {
        -List~String~ names
        +StorePath(List~String~ names)
        +getNames() List~String~
    }
    class InfoResponse {
        <<Builder>>
        +builder() Builder
        +Builder lastModified(long lastModified)
        +Builder lastUsed(long lastUsed)
        +Builder connection(UUID uuid)
        +Builder category(StorePath cat)
        +Builder name(StorePath name)
        +Builder rawData(Map~String, Object~ rawData)
        +Builder usageCategory(String usageCategory)
        +Builder type(String type)
        +Builder state(Object state)
        +Builder cache(Map~String, Object~ cache)
        +build() InfoResponse
    }
    class Response {
        <<Builder>>
        +builder() Builder
        +Builder infos(List~InfoResponse~ infos)
        +build() Object
    }
    class Provider {
        <<Interface>>
        +getUsageCategory() String
        +getId() String
    }
    class ClassUtils {
        <<Utility>>
        +isPrimitiveOrWrapper(Class~?~ clazz) boolean
    }

    ConnectionInfoExchangeImpl --|> ConnectionInfoExchange : 实现
    ConnectionInfoExchangeImpl --> DataStorage : 依赖
    ConnectionInfoExchangeImpl --> StoreEntry : 依赖
    ConnectionInfoExchangeImpl --> StorePath : 依赖
    ConnectionInfoExchangeImpl --> InfoResponse : 依赖
    ConnectionInfoExchangeImpl --> Response : 依赖
    DataStorage --> StoreEntry : 关联
    DataStorage --> StoreCategory : 关联
    DataStorage --> StorePath : 关联
    StoreEntry --> Provider : 关联
    StoreEntry --> StoreCategory : 关联
    InfoResponse --> StorePath : 组合
    Response --> InfoResponse : 组合
```

这段代码实现了一个连接信息交换服务，主要处理HTTP请求并返回连接信息响应。ConnectionInfoExchangeImpl类通过DataStorage获取存储的各类信息（包括连接条目、分类、路径等），构建InfoResponse对象列表，最终封装成Response返回。该实现涉及多个数据实体类（StoreEntry、StorePath等）和工具类（ClassUtils），通过Builder模式构建复杂响应对象，同时处理了空值检查和基本类型验证等边缘情况。


### 内部方法调用关系图

```mermaid
graph TD
    A["ConnectionInfoExchangeImpl.handle"]
    B["创建ArrayList<InfoResponse>"]
    C["遍历msg.getConnections()"]
    D["DataStorage.getStoreEntryIfPresent(uuid)"]
    E["抛出BeaconClientException"]
    F["DataStorage.getStoreCategoryIfPresent"]
    G["DataStorage.getStorePath"]
    H["创建StorePath对象"]
    I["过滤e.getStoreCache()"]
    J["构建InfoResponse"]
    K["list.add(apply)"]
    L["构建Response对象"]

    A --> B
    A --> C
    C --> D
    D -->|不存在| E
    D -->|存在| F
    F --> G
    G --> H
    C --> I
    I --> J
    J --> K
    K --> C
    C -->|循环结束| L

    M["ConnectionInfoExchangeImpl.getSynchronizationObject"]
    N["返回DataStorage.get()"]
    M --> N
```

```mermaid
sequenceDiagram
    participant Client
    participant ConnectionInfoExchangeImpl
    participant DataStorage
    participant InfoResponseBuilder

    Client->>ConnectionInfoExchangeImpl: handle(exchange, msg)
    ConnectionInfoExchangeImpl->>DataStorage: getStoreEntryIfPresent(uuid)
    alt 存在记录
        DataStorage-->>ConnectionInfoExchangeImpl: StoreEntry
        ConnectionInfoExchangeImpl->>DataStorage: getStoreCategoryIfPresent
        DataStorage-->>ConnectionInfoExchangeImpl: StoreCategory
        ConnectionInfoExchangeImpl->>DataStorage: getStorePath
        DataStorage-->>ConnectionInfoExchangeImpl: StorePath
        ConnectionInfoExchangeImpl->>InfoResponseBuilder: builder()
        InfoResponseBuilder-->>ConnectionInfoExchangeImpl: InfoResponse
    else 不存在记录
        DataStorage-->>ConnectionInfoExchangeImpl: 抛出异常
    end
    ConnectionInfoExchangeImpl-->>Client: Response对象
```

这段代码实现了一个连接信息交换服务，主要处理HTTP请求并返回连接相关信息。流程图展示了两个主要方法：handle()方法通过多层数据查询和过滤构建响应列表，getSynchronizationObject()方法返回数据存储实例。时序图详细描述了handle()方法中客户端与服务端、数据存储层之间的交互过程，包括异常处理和数据转换逻辑。代码通过DataStorage获取连接元数据，过滤有效缓存条目，最终构建标准化的InfoResponse对象列表返回给客户端。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getSynchronizationObject | Object | 重写方法，返回DataStorage的单例对象。 |
| handle | Object | 处理HTTP请求，获取连接信息并构建响应列表。 |




