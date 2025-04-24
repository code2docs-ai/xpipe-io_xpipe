# 基础信息

|      |      |
|------|------|
| 名称 | identity |
| 编码语言 | .java |
| 代码路径 | xpipe/ext/base/src/main/java/io/xpipe/ext/base/identity |
| 包名 | xpipe.ext.base.src.main.java.io.xpipe.ext.base.identity |
| 概述说明 | IdentityStore抽象类实现接口，含用户名及密码、SSH策略方法。LocalIdentityConvertAction转换本地身份为同步身份。SyncedIdentityStoreProvider管理同步身份存储。IdentityChoice提供SSH和容器验证选项。SshIdentityStrategyHelper处理SSH代理验证。IdentityMigrationDeserializer处理身份数据迁移。LocalIdentityStore存储本地身份信息。SshIdentityStateManager管理SSH代理状态。IdentitySelectComp为身份选择UI组件。SyncedIdentityStore实现同步身份存储。IdentityStoreProvider管理身份存储核心功能。 |

# 说明

```markdown
## 概述

该代码模块是一个身份管理系统的核心实现，主要提供本地和同步身份存储的管理功能。模块基于Java构建，使用Lombok简化代码，包含身份验证策略管理、存储转换、数据迁移和UI组件等完整解决方案。核心功能包括：

1. **身份存储体系**：通过`IdentityStore`抽象类及其子类`LocalIdentityStore`和`SyncedIdentityStore`实现不同作用域（本地/同步）的身份信息存储
2. **策略管理**：支持多种SSH身份验证策略（密钥文件、代理转发等）和密码管理策略
3. **数据转换**：提供本地身份与同步身份之间的相互转换能力
4. **向后兼容**：包含JSON反序列化迁移逻辑，确保旧版数据兼容性
5. **可视化交互**：完整的GUI对话框和组合框组件，支持身份信息的可视化管理和选择

## 主要业务场景

### 1. 身份信息存储与管理
- **本地存储**：通过`LocalIdentityStore`管理设备本地存储的用户名、密码和SSH密钥
- **同步存储**：通过`SyncedIdentityStore`实现跨设备同步的身份信息，支持按用户或全局配置
- **策略验证**：通过`checkComplete`方法验证密码和SSH身份策略的完整性

### 2. 身份验证策略处理
- **SSH认证**：支持密钥文件、多种代理（SshAgent/GpgAgent等）和PKCS11库路径配置
- **密码管理**：通过`SecretRetrievalStrategy`实现加密密码的存储和检索
- **策略构建**：使用工厂模式动态生成不同验证策略的选项界面

### 3. 数据转换与迁移
- **存储转换**：`LocalIdentityConvertAction`将本地身份加密转换为同步身份
- **格式迁移**：`IdentityMigrationDeserializer`处理旧版身份数据的JSON结构迁移

### 4. 用户交互
- **身份选择**：`IdentitySelectComp`提供组合框和按钮实现可视化身份选择
- **配置对话框**：通过`*StoreProvider`类构建包含用户名/密码/SSH密钥选项的GUI配置界面
- **选项构建**：`IdentityChoice`类动态生成SSH或容器模式的身份验证选项

### 5. 系统集成
- **代理管理**：`SshIdentityStateManager`处理不同操作系统下的SSH代理状态管理
- **数据同步**：验证SSH密钥文件是否同步到数据目录，确保跨设备可用性

该模块典型应用于需要统一管理认证凭据的系统，如：
- 跨服务器SSH连接工具
- 需要多设备同步的密码管理器
- 支持多种认证方式的自动化运维平台
```


### 包内部结构视图

```mermaid
graph TD
    identity --> IdentityStore.java
    identity --> LocalIdentityConvertAction.java
    identity --> SshIdentityStrategy.java
    identity --> IdentityValue.java
    identity --> SyncedIdentityStoreProvider.java
    identity --> IdentityChoice.java
    identity --> SshIdentityStrategyHelper.java
    identity --> IdentityMigrationDeserializer.java
    identity --> LocalIdentityStoreProvider.java
    identity --> LocalIdentityStore.java
    identity --> SshIdentityStateManager.java
    identity --> IdentitySelectComp.java
    identity --> SyncedIdentityStore.java
    identity --> IdentityStoreProvider.java
```

该流程图展示了xpipe项目中identity模块下的文件结构，所有Java文件均直接位于identity目录下，没有更深层级的子目录。这些文件主要涉及身份管理功能，包括身份存储、转换操作、SSH策略、状态管理等多种实现类，共同构成了一个完整的身份管理模块。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [IdentitySelectComp.java](IdentitySelectComp.md) | file | 身份选择组件，支持本地和同步身份管理，包含添加、编辑和清除功能。 |
| [LocalIdentityStoreProvider.java](LocalIdentityStoreProvider.md) | file | 本地身份存储提供类，实现获取分类、创建对话框、生成摘要等功能。 |
| [SshIdentityStrategy.java](SshIdentityStrategy.md) | file | 输入内容为空，无法生成概要描述。 |
| [LocalIdentityConvertAction.java](LocalIdentityConvertAction.md) | file | LocalIdentityConvertAction实现同步本地身份到远程存储功能。 |
| [IdentityStore.java](IdentityStore.md) | file | 抽象类IdentityStore实现密码和SSH身份验证策略检查。 |
| [IdentityMigrationDeserializer.java](IdentityMigrationDeserializer.md) | file | IdentityMigrationDeserializer继承DelegatingDeserializer，用于JSON数据迁移和重构。 |
| [SshIdentityStrategyHelper.java](SshIdentityStrategyHelper.md) | file | SSH身份策略助手类，提供多种身份验证方法选项构建器，包括文件、代理、PKCS11库等。 |
| [IdentityChoice.java](IdentityChoice.md) | file | IdentityChoice类提供SSH和容器身份验证选项构建器，支持自定义用户输入、密码和密钥配置。 |
| [SyncedIdentityStoreProvider.java](SyncedIdentityStoreProvider.md) | file | SyncedIdentityStoreProvider类处理同步身份存储，支持用户名、密码和SSH密钥认证，提供GUI配置和用户/全局身份管理。 |
| [IdentityValue.java](IdentityValue.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [IdentityStoreProvider.java](IdentityStoreProvider.md) | file | 抽象类实现身份存储功能，含状态显示、搜索项、信息字符串等方法。 |
| [SyncedIdentityStore.java](SyncedIdentityStore.md) | file | SyncedIdentityStore类继承IdentityStore，存储加密密码和SSH身份，支持用户范围存储，验证完整性。 |
| [SshIdentityStateManager.java](SshIdentityStateManager.md) | file | 管理SSH代理状态，支持Windows和Linux，处理外部、GPG和OpenSSH代理。 |
| [LocalIdentityStore.java](LocalIdentityStore.md) | file | LocalIdentityStore类继承IdentityStore，包含加密密码和SSH身份字段及对应方法。 |


