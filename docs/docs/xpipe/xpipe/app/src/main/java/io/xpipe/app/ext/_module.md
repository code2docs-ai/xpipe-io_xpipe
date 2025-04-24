# 基础信息

|      |      |
|------|------|
| 名称 | ext |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/ext |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.ext |
| 概述说明 | DataStoreProviders类管理数据存储提供者初始化和操作。PrefsProvider抽象类管理偏好设置。ShellSession管理ShellControl生命周期。ProcessControlProvider提供进程控制功能。LocalStore实现本地存储接口。ConnectionFileSystem通过ShellControl执行文件操作。 |

# 说明

```markdown
## 概述

该代码模块是XPipe应用的核心扩展系统，主要提供数据存储管理、Shell控制、偏好设置、进程控制等基础服务能力。模块采用模块化设计，通过`ModuleLayerLoader`接口实现动态加载机制，支持服务提供者的注册、初始化和生命周期管理。关键组件包括：

1. **数据存储系统**：包含`DataStoreProviders`管理提供者注册，`DataStoreProvider`定义存储接口，支持按ID/类型查找，配合`DataStorageExtensionProvider`实现扩展机制
2. **Shell控制体系**：`ShellControl`相关类实现Shell会话管理、命令执行和文件系统操作，`ShellSession`管理生命周期，`ConnectionFileSystem`提供基于Shell的文件操作
3. **配置管理**：`PrefsProvider`抽象类实现偏好设置管理，`PrefsHandler`处理带验证的GUI对话框
4. **进程控制**：`ProcessControlProvider`抽象类提供进程创建、权限提升、Shell方言管理等能力
5. **异常处理**：`ExtensionException`提供扩展异常处理机制，包含安装损坏检测等特殊场景处理

## 主要业务场景

1. **数据存储管理**：
   - 通过`DataStoreProviders`初始化/重置存储提供者
   - 使用`byId`/`byStore`进行提供者查找
   - `ContainerStoreState`管理容器存储状态合并
   - `LocalStore`实现本地存储的特殊处理

2. **Shell操作**：
   - `ShellSession`创建并管理Shell控制会话
   - `ConnectionFileSystem`实现基于Shell的文件系统操作
   - `ShellControlFunction`执行具体Shell命令

3. **系统配置**：
   - `PrefsProvider`加载和管理所有偏好设置
   - `GuiDialog`构建带验证的配置对话框
   - `UserBasedValue`处理用户级配置值

4. **扩展异常处理**：
   - 通过`ExtensionException.corrupt()`检测安装损坏
   - 统一处理模块加载过程中的各类异常

5. **模块化加载**：
   - 各组件通过`Loader`内部类实现`ModuleLayerLoader`接口
   - 使用ServiceLoader机制动态加载实现类
   - 初始化时进行排序和验证（如`ScanProvider`的扫描功能初始化）

模块采用建造者模式（如`ContainerStoreState`）、单例模式（如`ProcessControlProvider`）等设计模式，结合Lombok简化代码，通过Jackson实现序列化支持。
```


### 包内部结构视图

```mermaid
graph TD
    ext --> DataStoreProviders.java
    ext --> ActionProvider.java
    ext --> NameableStore.java
    ext --> DataStoreProvider.java
    ext --> ShellControlFunction.java
    ext --> SingletonSessionStoreProvider.java
    ext --> PrefsHandler.java
    ext --> GuiDialog.java
    ext --> PrefsProvider.java
    ext --> DataStoreUsageCategory.java
    ext --> ExtensionException.java
    ext --> ShellSession.java
    ext --> EnabledParentStoreProvider.java
    ext --> ScanProvider.java
    ext --> UserBasedValue.java
    ext --> ContainerImageStore.java
    ext --> UserScopeStore.java
    ext --> ProcessControlProvider.java
    ext --> ContainerStoreState.java
    ext --> ShellControlParentStoreFunction.java
    ext --> LocalStore.java
    ext --> DataStorageExtensionProvider.java
    ext --> PrefsChoiceValue.java
    ext --> DataStoreCreationCategory.java
    ext --> ShellStore.java
    ext --> ConnectionFileSystem.java
```

该流程图展示了xpipe项目中ext目录下的所有文件结构。根节点为ext，直接包含24个不同类型的Java文件，涵盖数据存储、Shell控制、用户偏好设置、容器管理等多个功能模块。这些文件共同构成了xpipe应用的核心扩展功能体系，每个文件代表一个特定的功能接口或实现类。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [DataStoreUsageCategory.java](DataStoreUsageCategory.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [PrefsProvider.java](PrefsProvider.md) | file | 抽象类PrefsProvider管理偏好设置，提供获取所有实例和按类查找功能，支持初始化和模块加载。 |
| [GuiDialog.java](GuiDialog.md) | file | GUI对话框类，含组件和验证器，支持全参和单参构造。 |
| [PrefsHandler.java](PrefsHandler.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [SingletonSessionStoreProvider.java](SingletonSessionStoreProvider.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [ShellControlFunction.java](ShellControlFunction.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息。 |
| [DataStoreProvider.java](DataStoreProvider.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [PrefsChoiceValue.java](PrefsChoiceValue.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [DataStorageExtensionProvider.java](DataStorageExtensionProvider.md) | file | 抽象类提供数据存储扩展，静态方法获取所有实例，Loader初始化模块层并加载服务。 |
| [LocalStore.java](LocalStore.md) | file | 本地存储类实现网络隧道和Shell存储接口，支持Shell控制功能。 |
| [ShellControlParentStoreFunction.java](ShellControlParentStoreFunction.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [ProcessControlProvider.java](ProcessControlProvider.md) | file | 抽象类提供进程控制功能，包括初始化、重置、命令执行、本地进程创建及存储处理等。 |
| [UserScopeStore.java](UserScopeStore.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [ContainerImageStore.java](ContainerImageStore.md) | file | 输入内容为空，无法生成概要。请提供具体信息以便总结。 |
| [UserBasedValue.java](UserBasedValue.md) | file | 信息为空，无法生成概要。 |
| [ScanProvider.java](ScanProvider.md) | file | 抽象类ScanProvider提供扫描功能，包含创建扫描机会和抽象扫描方法，内部类ScanOpportunity存储扫描信息，Loader初始化所有扫描提供者。 |
| [EnabledParentStoreProvider.java](EnabledParentStoreProvider.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息。 |
| [ShellSession.java](ShellSession.md) | file | ShellSession类管理ShellControl生命周期，处理启动、停止及状态变更通知。 |
| [ConnectionFileSystem.java](ConnectionFileSystem.md) | file | 基于ShellControl实现的文件系统操作类，提供文件读写、增删改查等功能。 |
| [ShellStore.java](ShellStore.md) | file | 输入内容为空，无法生成概要。请提供具体信息以便总结。 |
| [DataStoreCreationCategory.java](DataStoreCreationCategory.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [ContainerStoreState.java](ContainerStoreState.md) | file | Java类ContainerStoreState继承ShellStoreState，包含imageName、containerState、shellMissing字段，支持合并更新。 |
| [ExtensionException.java](ExtensionException.md) | file | 自定义异常类，处理XPipe安装数据损坏问题。 |
| [NameableStore.java](NameableStore.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [ActionProvider.java](ActionProvider.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [DataStoreProviders.java](DataStoreProviders.md) | file | 数据存储提供者管理类，包含初始化、重置、查询功能，支持模块加载与验证。 |


