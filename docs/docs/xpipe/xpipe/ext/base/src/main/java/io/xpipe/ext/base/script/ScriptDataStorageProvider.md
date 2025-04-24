# 基础信息

|      |      |
|------|------|
| 名称 | ScriptDataStorageProvider |
| 编码语言 | .java |
| 代码路径 | xpipe/ext/base/src/main/java/io/xpipe/ext/base/script/ScriptDataStorageProvider.java |
| 包名 | io.xpipe.ext.base.script |
| 依赖项 | ['io.xpipe.app.core.AppProperties', 'io.xpipe.app.ext.DataStorageExtensionProvider', 'io.xpipe.app.storage.DataStorage', 'io.xpipe.app.storage.DataStoreEntry', 'java.nio.charset.StandardCharsets', 'java.util.UUID'] |
| 概述说明 | ScriptDataStorageProvider初始化脚本存储，处理自定义和预定义脚本组及脚本条目。 |

# 说明

ScriptDataStorageProvider继承DataStorageExtensionProvider，在storageInit方法中处理脚本存储初始化。若非首次启动则跳过。创建自定义脚本存储条目，并为每个预定义脚本组和脚本创建或更新存储条目，设置UUID、名称、描述等属性，维护引用关系。确保条目存在且状态正确。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ScriptDataStorageProvider | class | ScriptDataStorageProvider初始化存储，处理自定义和预定义脚本组及脚本条目。 |



## 类 ScriptDataStorageProvider

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ScriptDataStorageProvider |
| 说明 | ScriptDataStorageProvider初始化存储，处理自定义和预定义脚本组及脚本条目。 |


### UML类图

```mermaid
classDiagram
    class DataStorageExtensionProvider {
        <<Interface>>
        +storageInit() void
    }

    class ScriptDataStorageProvider {
        +storageInit() void
    }

    class AppProperties {
        +isInitialLaunch() boolean
    }

    class DataStorage {
        +CUSTOM_SCRIPTS_CATEGORY_UUID UUID
        +PREDEFINED_SCRIPTS_CATEGORY_UUID UUID
        +get() DataStorage
        +addStoreEntryIfNotPresent(DataStoreEntry) DataStoreEntry
        +getStoreEntryIfPresent(UUID) Optional~DataStoreEntry~
    }

    class DataStoreEntry {
        +createNew(UUID, UUID, String, Object) DataStoreEntry
        +setStoreInternal(Object, boolean) void
        +setExpanded(boolean) void
        +ref() Reference~DataStoreEntry~
    }

    class ScriptGroupStore {
        +builder() Builder
    }

    class PredefinedScriptGroup {
        <<Enum>>
        +values() PredefinedScriptGroup[]
        +getName() String
        +getDescription() String
        +isExpanded() boolean
        +setEntry(Reference~DataStoreEntry~) void
    }

    class PredefinedScriptStore {
        <<Enum>>
        +values() PredefinedScriptStore[]
        +getUuid() UUID
        +getName() String
        +getScriptStore() Supplier~ScriptStore~
        +setEntry(Reference~DataStoreEntry~) void
    }

    ScriptDataStorageProvider --> DataStorageExtensionProvider : 实现
    ScriptDataStorageProvider --> AppProperties : 检查初始启动
    ScriptDataStorageProvider --> DataStorage : 数据存储操作
    ScriptDataStorageProvider --> DataStoreEntry : 创建/更新存储条目
    ScriptDataStorageProvider --> ScriptGroupStore : 构建脚本组存储
    ScriptDataStorageProvider --> PredefinedScriptGroup : 处理预定义脚本组
    ScriptDataStorageProvider --> PredefinedScriptStore : 处理预定义脚本存储
    DataStoreEntry --> Reference : 返回引用
```

该代码实现了一个脚本数据存储提供者，主要功能是在应用初始启动时初始化脚本存储结构。类图展示了核心组件关系：ScriptDataStorageProvider继承自DataStorageExtensionProvider接口，通过DataStorage管理存储条目(DataStoreEntry)，处理两类脚本数据（自定义脚本和预定义脚本）。预定义脚本通过PredefinedScriptGroup和PredefinedScriptStore枚举配置，使用ScriptGroupStore构建存储结构，整个过程严格检查初始启动状态以避免重复初始化。


### 内部方法调用关系图

```mermaid
graph TD
    A["ScriptDataStorageProvider.storageInit()"]
    B["检查初始启动: !AppProperties.get().isInitialLaunch()"]
    C["创建自定义脚本存储: DataStoreEntry.createNew"]
    D["添加存储条目: DataStorage.get().addStoreEntryIfNotPresent"]
    E["遍历PredefinedScriptGroup"]
    F["构建脚本组存储: ScriptGroupStore.builder"]
    G["创建预定义脚本条目: DataStoreEntry.createNew"]
    H["设置存储属性: e.setStoreInternal/store.setExpanded/value.setEntry"]
    I["遍历PredefinedScriptStore"]
    J["检查条目存在: DataStorage.get().getStoreEntryIfPresent"]
    K["更新现有条目: previous.get().setStoreInternal/value.setEntry"]
    L["创建新条目: DataStoreEntry.createNew/addStoreEntryIfNotPresent/value.setEntry"]

    A --> B
    B -->|false| C
    C --> D
    A --> E
    E --> F
    F --> G
    G --> H
    A --> I
    I --> J
    J -->|存在| K
    J -->|不存在| L
```

这段代码流程图展示了ScriptDataStorageProvider类的初始化过程。首先检查是否为首次启动，然后分别处理自定义脚本和预定义脚本的存储初始化。对于预定义脚本，会遍历枚举值创建或更新存储条目，设置相关属性如UUID、名称、描述等，并通过引用关联存储对象。整个过程确保数据存储的完整性和一致性，同时避免重复创建已有条目。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| storageInit | void | 初始化存储，检查首次启动后添加自定义和预定义脚本组及脚本条目。 |




