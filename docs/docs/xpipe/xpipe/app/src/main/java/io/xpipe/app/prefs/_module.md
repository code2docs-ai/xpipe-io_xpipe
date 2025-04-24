# 基础信息

|      |      |
|------|------|
| 名称 | prefs |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/prefs |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.prefs |
| 概述说明 | 应用偏好设置类实现，管理外观、终端、安全等配置选项，支持多平台和自定义设置。 |

# 说明

```markdown
## 概述

该代码模块实现了一个综合性的应用程序偏好设置管理系统，采用分层架构设计，主要包含以下核心组件：

1. **核心框架类**：
   - `AppPrefs`：单例模式管理所有偏好设置，支持本地/远程存储分离，包含300+配置项
   - `AppPrefsCategory`：抽象基类定义偏好设置分类的标准接口
   - `AppPrefsStorageHandler`：JSON格式的持久化存储处理器

2. **UI组件体系**：
   - `AppPrefsComp`：主界面采用水平分割布局（导航栏+内容区）
   - `AppPrefsSidebarComp`：动态生成分类导航按钮
   - `OptionsBuilder`：统一界面构建工具

3. **分类实现**：
   - 包含20+具体分类（如外观、安全、终端等）
   - 每个分类继承`AppPrefsCategory`并实现特定配置功能
   - 支持跨平台差异化显示（Windows/macOS/Linux）

4. **辅助功能**：
   - 外部应用集成（编辑器/RDP客户端等）
   - 更新检查机制
   - 故障诊断工具集
   - 第三方依赖管理

## 主要业务场景

1. **系统配置管理**：
   - 启动/关闭行为设置（`StartupBehaviour`/`CloseBehaviour`）
   - 开发者模式开关（`DeveloperCategory`）
   - 日志管理（`LoggingCategory`）

2. **UI个性化**：
   - 主题/语言选择（`AppearanceCategory`）
   - 图标源管理（`IconsCategory`）
   - 终端样式配置（`TerminalCategory`）

3. **安全控制**：
   - 密码管理器集成（`PasswordManagerCategory`）
   - 保险库加密（`VaultCategory`）
   - API认证设置（`HttpApiCategory`）

4. **网络与连接**：
   - SSH客户端配置（`SshCategory`）
   - RDP客户端设置（`RdpCategory`）
   - 代理服务器选项

5. **工作区管理**：
   - 多工作区创建（`WorkspacesCategory`）
   - 文件浏览器设置（`FileBrowserCategory`）
   - 云同步配置（`SyncCategory`）

6. **维护功能**：
   - 更新检查（`UpdatesCategory`）
   - 故障诊断（`TroubleshootCategory`）
   - 第三方依赖查看（`ThirdPartyDependencyListComp`）

7. **外部工具集成**：
   - 编辑器配置（`EditorCategory`）
   - 外部应用检测（`ExternalApplicationType`）
   - 命令行参数处理（`ExternalApplicationHelper`）

典型交互流程：
1. 用户通过侧边栏选择配置分类
2. 系统动态加载对应分类的UI组件
3. 修改配置后自动保存至JSON文件
4. 部分关键配置变更触发重启提示
5. 开发者模式启用后显示高级选项
```


### 包内部结构视图

```mermaid
graph TD
    prefs --> AppearanceCategory.java
    prefs --> AppPrefsComp.java
    prefs --> HttpApiCategory.java
    prefs --> RdpCategory.java
    prefs --> EditorCategory.java
    prefs --> AppPrefsStorageHandler.java
    prefs --> ThirdPartyDependency.java
    prefs --> UpdateCheckComp.java
    prefs --> VaultCategory.java
    prefs --> SystemCategory.java
    prefs --> SshCategory.java
    prefs --> SecurityCategory.java
    prefs --> WorkspaceCreationDialog.java
    prefs --> LoggingCategory.java
    prefs --> ExternalApplicationHelper.java
    prefs --> AboutCategory.java
    prefs --> CloseBehaviour.java
    prefs --> TroubleshootCategory.java
    prefs --> StartupBehaviour.java
    prefs --> ExternalRdpClientType.java
    prefs --> ConnectionHubCategory.java
    prefs --> ThirdPartyDependencyListComp.java
    prefs --> CloseBehaviourDialog.java
    prefs --> FileBrowserCategory.java
    prefs --> WorkspacesCategory.java
    prefs --> AppPrefsSidebarComp.java
    prefs --> ExternalApplicationType.java
    prefs --> DeveloperCategory.java
    prefs --> IconsCategory.java
    prefs --> LinksCategory.java
    prefs --> SyncCategory.java
    prefs --> TerminalCategory.java
    prefs --> AppPrefs.java
    prefs --> UpdatesCategory.java
    prefs --> ExternalEditorType.java
    prefs --> AppPrefsCategory.java
    prefs --> SupportedLocale.java
    prefs --> PasswordManagerCategory.java
```

该流程图展示了xpipe项目中prefs目录下的所有文件和类结构。prefs作为根节点，直接包含34个不同类型的配置类文件，涵盖外观、安全、终端、编辑器、第三方依赖等多个功能模块的配置管理。这些配置类主要用于应用程序的偏好设置和系统参数管理，体现了模块化的设计思想。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [PasswordManagerCategory.java](PasswordManagerCategory.md) | file | 密码管理器类，含测试功能与UI组件。 |
| [ExternalApplicationType.java](ExternalApplicationType.md) | file | 抽象类ExternalApplicationType定义外部应用类型，含Mac、Path、Windows子类，检查可用性并处理启动逻辑。 |
| [ThirdPartyDependencyListComp.java](ThirdPartyDependencyListComp.md) | file | 创建第三方依赖列表组件，包含可折叠面板、超链接、许可证信息及文本展示。 |
| [ExternalApplicationHelper.java](ExternalApplicationHelper.md) | file | 替换变量并启动异步命令的工具类。 |
| [AppPrefsStorageHandler.java](AppPrefsStorageHandler.md) | file | 应用偏好存储处理器，管理JSON文件读写与对象序列化。 |
| [EditorCategory.java](EditorCategory.md) | file | 编辑器配置类，含外部编辑器选择和测试功能。 |
| [RdpCategory.java](RdpCategory.md) | file | RdpCategory类定义RDP配置选项，包括客户端类型和自定义命令设置。 |
| [HttpApiCategory.java](HttpApiCategory.md) | file | HTTP API配置类，包含启用开关、API密钥输入和禁用认证选项。 |
| [AppPrefsComp.java](AppPrefsComp.md) | file | 应用偏好设置组件，包含分类列表和滚动联动逻辑。 |
| [AppearanceCategory.java](AppearanceCategory.md) | file | 外观设置类，包含主题、语言、性能模式等UI选项配置。 |
| [LoggingCategory.java](LoggingCategory.md) | file | 日志设置类，包含终端日志开关和打开日志目录按钮功能。 |
| [WorkspaceCreationDialog.java](WorkspaceCreationDialog.md) | file | 异步显示工作空间创建对话框，验证许可后收集名称和路径，创建快捷方式并关闭操作模式。 |
| [SecurityCategory.java](SecurityCategory.md) | file | 安全设置类，包含权限确认、密码缓存等选项。 |
| [SshCategory.java](SshCategory.md) | file | SSH配置类，含详细输出选项，Windows下支持X11 WSL实例设置。 |
| [SystemCategory.java](SystemCategory.md) | file | SystemCategory类扩展AppPrefsCategory，创建系统偏好设置界面，包含启动、关闭行为和开发者模式选项。 |
| [VaultCategory.java](VaultCategory.md) | file | VaultCategory类扩展AppPrefsCategory，管理保险库设置，包括加密、用户类型和团队功能，支持同步和许可控制。 |
| [UpdateCheckComp.java](UpdateCheckComp.md) | file | 更新检查组件，包含状态监测、刷新和弹窗功能，支持多语言和不同分发类型。 |
| [ThirdPartyDependency.java](ThirdPartyDependency.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息以便总结。 |
| [AppPrefsSidebarComp.java](AppPrefsSidebarComp.md) | file | 应用偏好侧边栏组件，包含分类按钮和重启按钮，动态更新选中状态。 |
| [WorkspacesCategory.java](WorkspacesCategory.md) | file | WorkspacesCategory类扩展AppPrefsCategory，管理创建工作区选项，需许可证支持。 |
| [FileBrowserCategory.java](FileBrowserCategory.md) | file | 文件浏览器设置类，包含终端停靠、双击编辑、下载目录和启动固定选项。 |
| [CloseBehaviourDialog.java](CloseBehaviourDialog.md) | file | 检查关闭行为设置，未设置时显示对话框供用户选择，确认后保存设置。 |
| [ConnectionHubCategory.java](ConnectionHubCategory.md) | file | ConnectionHubCategory类扩展AppPrefsCategory，定义连接中心配置选项。 |
| [ExternalRdpClientType.java](ExternalRdpClientType.md) | file | 输入内容为空，无法生成概要描述。请提供具体信息。 |
| [StartupBehaviour.java](StartupBehaviour.md) | file | 输入内容为空，无法生成概要描述。 |
| [TroubleshootCategory.java](TroubleshootCategory.md) | file | TroubleshootCategory类提供故障排查选项，包括报告问题、调试模式、日志操作、数据清理和堆转储功能。 |
| [CloseBehaviour.java](CloseBehaviour.md) | file | 输入内容为空，无法生成概要描述。 |
| [AboutCategory.java](AboutCategory.md) | file | 关于页面的Java类，包含版本信息和更新检查组件。 |
| [SupportedLocale.java](SupportedLocale.md) | file | 当前输入内容为空，请提供需要总结的具体信息。 |
| [AppPrefsCategory.java](AppPrefsCategory.md) | file | 抽象类AppPrefsCategory定义组件宽度600，默认显示，需实现获取ID和创建组件方法。 |
| [ExternalEditorType.java](ExternalEditorType.md) | file | 输入内容为空，无法生成概要。请提供具体信息。 |
| [UpdatesCategory.java](UpdatesCategory.md) | file | UpdatesCategory类扩展AppPrefsCategory，创建包含自动检查和安全性更新选项的界面。 |
| [AppPrefs.java](AppPrefs.md) | file | 应用配置类，管理本地和共享远程设置，包含主题、终端、密码管理等属性，支持保存和加载。 |
| [TerminalCategory.java](TerminalCategory.md) | file | 终端配置类，包含类型选择、代理设置、提示符和多路复用器选项，支持测试和许可验证。 |
| [SyncCategory.java](SyncCategory.md) | file | SyncCategory类实现同步设置界面，包含测试连接、远程仓库配置和浏览保险库功能。 |
| [LinksCategory.java](LinksCategory.md) | file | LinksCategory类创建包含多个链接按钮的界面，如Discord、文档、隐私等，点击后跳转对应页面或打开模态框。 |
| [IconsCategory.java](IconsCategory.md) | file | IconsCategory类管理图标源，提供添加、刷新和删除功能，支持Git和本地目录源。 |
| [DeveloperCategory.java](DeveloperCategory.md) | file | 开发者选项类，包含命令执行和调试开关功能。 |


