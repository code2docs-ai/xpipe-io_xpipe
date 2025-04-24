# 基础信息

|      |      |
|------|------|
| 名称 | service |
| 编码语言 | .java |
| 代码路径 | xpipe/ext/base/src/main/java/io/xpipe/ext/base/service |
| 包名 | xpipe.ext.base.src.main.java.io.xpipe.ext.base.service |
| 概述说明 | Java类集合，包含服务存储、组存储、控制会话及相关功能实现，使用Lombok注解简化代码，支持JSON序列化与GUI配置。 |

# 说明

```markdown
## 概述
该代码模块是一个基于Java的服务管理框架，主要提供各类服务的存储、配置、控制和状态管理功能。模块采用分层设计，包含抽象基类、具体实现和辅助工具类，使用Lombok简化代码，Jackson处理序列化。核心功能围绕服务存储(ServiceStore)、服务组(ServiceGroup)和服务控制(ServiceControl)三大体系构建，支持自定义服务、固定服务和映射服务等多种服务类型，提供统一的GUI配置界面和操作API。

## 主要业务场景
1. **服务存储管理**
   - 支持三种服务存储类型：`CustomServiceStore`(自定义服务)、`FixedServiceStore`(固定服务)和`MappedServiceStore`(映射服务)
   - 通过`AbstractServiceStoreProvider`及其子类提供存储配置、会话管理和状态监控
   - 包含端口转发功能，支持本地与远程端口映射

2. **服务组管理**
   - 通过`AbstractServiceGroupStore`及其实现类(`CustomServiceGroupStore`/`FixedServiceGroupStore`)管理服务组
   - 支持批量操作子服务，包括启停控制和状态刷新
   - 提供父子服务层级关系管理

3. **服务控制**
   - `ServiceControlStore`配合`ServiceControlSession`实现服务生命周期管理
   - 支持通过脚本(start/stop/status)控制服务状态
   - 包含权限提升(elevation)机制

4. **辅助功能**
   - 地址复制(`ServiceCopyAddressAction`)：格式化服务地址并复制到剪贴板
   - 服务刷新(`ServiceRefreshAction`)：手动刷新服务状态
   - 协议类型处理(`ServiceProtocolTypeHelper`)：管理HTTP/HTTPS等协议配置

5. **GUI集成**
   - 统一的配置对话框构建机制
   - 动态UI组件生成(如协议类型选择器)
   - 状态感知的界面元素控制
```


### 包内部结构视图

```mermaid
graph TD
    service --> CustomServiceStore.java
    service --> FixedServiceCreatorStore.java
    service --> MappedServiceStoreProvider.java
    service --> CustomServiceStoreProvider.java
    service --> AbstractServiceGroupStore.java
    service --> CustomServiceGroupStore.java
    service --> ServiceCopyAddressAction.java
    service --> AbstractServiceStoreProvider.java
    service --> ServiceRefreshAction.java
    service --> AbstractServiceGroupStoreProvider.java
    service --> FixedServiceGroupStore.java
    service --> FixedServiceStoreProvider.java
    service --> MappedServiceStore.java
    service --> AbstractServiceStore.java
    service --> FixedServiceGroupStoreProvider.java
    service --> FixedServiceStore.java
    service --> ServiceControlSession.java
    service --> ServiceProtocolType.java
    service --> ServiceControlStore.java
    service --> ServiceControlStoreProvider.java
    service --> CustomServiceGroupStoreProvider.java
    service --> ServiceProtocolTypeHelper.java
```

该流程图展示了xpipe项目中service目录下的所有文件结构。根节点为service文件夹，直接包含23个Java类文件，这些文件主要涉及服务存储、服务组管理、服务控制等功能的实现类。所有文件均位于同一层级，没有子目录嵌套关系，属于扁平化结构设计。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [FixedServiceStore.java](FixedServiceStore.md) | file | FixedServiceStore类继承AbstractServiceStore，包含host和displayParent字段，实现FixedChildStore接口，无需许可证，检查非空并返回固定ID。 |
| [AbstractServiceStore.java](AbstractServiceStore.md) | file | 抽象类实现网络隧道会话存储，含端口配置、许可证检查及会话创建逻辑。 |
| [ServiceCopyAddressAction.java](ServiceCopyAddressAction.md) | file | 服务地址复制动作类，实现ActionProvider接口，提供复制服务地址功能。 |
| [FixedServiceCreatorStore.java](FixedServiceCreatorStore.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [CustomServiceStore.java](CustomServiceStore.md) | file | Java类CustomServiceStore继承AbstractServiceStore，包含host字段，使用多个注解配置。 |
| [CustomServiceGroupStore.java](CustomServiceGroupStore.md) | file | 自定义服务组存储类，继承抽象服务组存储，检查父类类型为DataStore。 |
| [AbstractServiceGroupStore.java](AbstractServiceGroupStore.md) | file | 抽象类实现数据存储和组存储接口，包含父引用检查和完整性验证。 |
| [CustomServiceStoreProvider.java](CustomServiceStoreProvider.md) | file | 自定义服务存储提供类，实现服务配置、端口绑定及协议选择功能。 |
| [MappedServiceStoreProvider.java](MappedServiceStoreProvider.md) | file | MappedServiceStoreProvider类扩展FixedServiceStoreProvider，提供映射服务存储的显示名称、ID、格式化服务和GUI对话框功能。 |
| [FixedServiceGroupStoreProvider.java](FixedServiceGroupStoreProvider.md) | file | 固定服务组存储提供类，实现默认存储、获取父项、ID及存储类列表功能。 |
| [MappedServiceStore.java](MappedServiceStore.md) | file | MappedServiceStore类继承FixedServiceStore，包含containerPort字段且需许可证。 |
| [FixedServiceStoreProvider.java](FixedServiceStoreProvider.md) | file | FixedServiceStoreProvider类继承AbstractServiceStoreProvider，提供固定服务存储功能，包括获取父存储、ID标识、存储类列表和GUI对话框配置。 |
| [FixedServiceGroupStore.java](FixedServiceGroupStore.md) | file | FixedServiceGroupStore类继承AbstractServiceGroupStore，实现DataStore和FixedHierarchyStore接口，包含完整性检查和子项列表方法。 |
| [AbstractServiceGroupStoreProvider.java](AbstractServiceGroupStoreProvider.md) | file | 抽象服务组存储提供类，实现数据存储接口，管理子服务开关状态及信息显示。 |
| [ServiceRefreshAction.java](ServiceRefreshAction.md) | file | 实现服务刷新的ActionProvider类，包含单例和批量操作逻辑。 |
| [AbstractServiceStoreProvider.java](AbstractServiceStoreProvider.md) | file | 抽象服务存储提供者类，实现会话和数据存储接口，支持隧道功能、状态显示和自定义条目组件。 |
| [ServiceProtocolTypeHelper.java](ServiceProtocolTypeHelper.md) | file | ServiceProtocolTypeHelper类提供HTTP、HTTPS和自定义协议选项构建功能。 |
| [CustomServiceGroupStoreProvider.java](CustomServiceGroupStoreProvider.md) | file | 自定义服务组存储提供类，继承抽象类，实现默认存储、显示父项、ID及存储类列表方法。 |
| [ServiceControlStoreProvider.java](ServiceControlStoreProvider.md) | file | ServiceControlStoreProvider实现数据存储接口，管理服务控制存储的显示、分类和对话框配置。 |
| [ServiceControlStore.java](ServiceControlStore.md) | file | ServiceControlStore类实现SingletonSessionStore接口，包含主机、启停状态脚本及权限检查。 |
| [ServiceProtocolType.java](ServiceProtocolType.md) | file | 输入内容为空，无法生成概要。请提供需要总结的具体信息。 |
| [ServiceControlSession.java](ServiceControlSession.md) | file | ServiceControlSession管理服务启停，检查状态并通知状态变更。 |


