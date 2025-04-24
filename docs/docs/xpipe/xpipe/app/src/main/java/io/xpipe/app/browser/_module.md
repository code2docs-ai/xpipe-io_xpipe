# 基础信息

|      |      |
|------|------|
| 名称 | browser |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/browser |
| 包名 | xpipe.app.src.main.java.io.xpipe.app.browser |
| 概述说明 | 浏览器图标管理系统，支持文件/目录图标动态加载、主题适配和统一尺寸处理。 |

# 说明

```markdown
## 概述

该代码模块实现了一个完整的浏览器文件管理系统，采用分层架构设计，主要包含以下核心功能：
1. **文件浏览器界面**：提供文件列表展示、导航栏、面包屑导航等UI组件
2. **文件操作管理**：支持文件传输、剪贴板操作、上下文菜单等交互功能
3. **会话管理**：实现多标签页、分屏浏览、历史记录等会话功能
4. **图标系统**：动态加载和管理文件/目录图标，支持主题适配
5. **文件选择器**：提供模态对话框形式的文件选择功能

模块采用观察者模式实现数据与UI的动态绑定，支持跨平台操作（Windows/MacOS/Linux），并包含权限管理、路径处理等基础功能。

## 主要业务场景

1. **文件浏览与管理**
   - 通过文件列表组件展示目录内容，支持排序、过滤和多选操作
   - 导航栏和面包屑组件提供路径导航和快捷操作（前进/后退/刷新）
   - 图标系统根据文件类型和主题动态加载对应图标

2. **文件传输与操作**
   - 处理本地/跨系统文件移动/复制操作
   - 管理下载队列和传输进度
   - 提供剪贴板和拖放操作支持
   - 通过上下文菜单实现各类文件操作

3. **会话管理**
   - 多标签页浏览支持，包括标签页固定、分屏等功能
   - 维护导航历史记录（前进/后退）
   - 持久化最近访问目录状态
   - 管理用户/组权限信息

4. **文件选择器**
   - 提供模态对话框形式的文件选择界面
   - 支持单文件/多文件选择模式
   - 包含书签过滤和文件系统导航功能

5. **终端集成**
   - 从文件浏览器直接启动终端操作
   - 管理终端会话

6. **特殊功能**
   - 本地文件系统访问
   - 动态问候语显示
   - 状态栏展示传输状态和操作按钮
```


### 包内部结构视图

```mermaid
graph TD
    browser --> icon
    browser --> file
    browser --> action
    browser --> BrowserFullSessionComp.java
    browser --> BrowserFullSessionModel.java
    browser --> BrowserFileChooserSessionModel.java
    browser --> BrowserStoreSessionTab.java
    browser --> BrowserSessionTabsComp.java
    browser --> BrowserAbstractSessionModel.java
    browser --> BrowserFileChooserSessionComp.java
    browser --> BrowserSessionTab.java
    icon --> BrowserIconFileType.java
    icon --> BrowserIcons.java
    icon --> BrowserIconDirectoryType.java
    icon --> BrowserIconManager.java
    icon --> BrowserIconVariant.java
    file --> BrowserFileSystemCache.java
    file --> BrowserFileSystemHelper.java
    file --> BrowserConnectionListFilterComp.java
    file --> BrowserFileTransferMode.java
    file --> BrowserQuickAccessContextMenu.java
    file --> BrowserNavBarComp.java
    file --> BrowserFileListNameCell.java
    file --> BrowserFileOpener.java
    file --> BrowserFileSystemTabModel.java
    file --> BrowserTransferProgress.java
    file --> BrowserHistorySavedState.java
    file --> BrowserClipboard.java
    file --> BrowserTransferModel.java
    file --> BrowserContextMenu.java
    file --> BrowserQuickAccessButtonComp.java
    file --> BrowserLocalFileSystem.java
    file --> BrowserAlerts.java
    file --> BrowserFileSystemTabComp.java
    file --> BrowserHistorySavedStateImpl.java
    file --> BrowserOverviewComp.java
    file --> BrowserFileSelectionListComp.java
    file --> BrowserTerminalDockTabModel.java
    file --> BrowserFileListFilterComp.java
    file --> BrowserFileListModel.java
    file --> BrowserBreadcrumbBar.java
    file --> BrowserFileTransferOperation.java
    file --> BrowserConnectionListComp.java
    file --> BrowserFileOverviewComp.java
    file --> BrowserStatusBarComp.java
    file --> BrowserFileSystemHistory.java
    file --> BrowserTransferComp.java
    file --> BrowserHistoryTabModel.java
    file --> BrowserHistoryTabComp.java
    file --> BrowserFileSystemSavedState.java
    file --> BrowserFileListCompEntry.java
    file --> BrowserFileListComp.java
    file --> BrowserGreetingComp.java
    file --> BrowserEntry.java
    action --> BrowserAction.java
    action --> BrowserApplicationPathAction.java
    action --> BrowserActionFormatter.java
    action --> BrowserBranchAction.java
    action --> BrowserLeafAction.java
```

该流程图展示了xpipe项目中browser模块的完整文件结构，包含icon、file、action三个主要子目录及其下属文件，以及直接位于browser目录下的多个核心组件类。文件目录层级清晰，共呈现了56个节点，完整覆盖了路径中所有终端文件和目录关系，未超出给定路径总数。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [BrowserSessionTab.java](BrowserSessionTab.md) | file | 抽象类定义浏览器会话标签页，含状态属性、模型引用及标签页拆分功能，提供组件、关闭、初始化等抽象方法。 |
| [BrowserFileChooserSessionComp.java](BrowserFileChooserSessionComp.md) | file | 浏览器文件选择器组件，支持单文件选择和保存操作，包含书签列表和文件系统导航功能。 |
| [BrowserSessionTabsComp.java](BrowserSessionTabsComp.md) | file | 浏览器标签页组件，支持拖拽排序、快捷键操作和自定义样式。 |
| [BrowserStoreSessionTab.java](BrowserStoreSessionTab.md) | file | 抽象类BrowserStoreSessionTab扩展BrowserSessionTab，含数据存储引用、名称及图标颜色方法，需实现组件、关闭等抽象方法。 |
| [BrowserFileChooserSessionModel.java](BrowserFileChooserSessionModel.md) | file | 文件选择会话模型，含选择模式、文件列表监听及完成回调功能。 |
| [BrowserFullSessionModel.java](BrowserFullSessionModel.md) | file | 浏览器会话管理类，含标签页拆分、固定、恢复状态及文件系统操作功能。 |
| [BrowserFullSessionComp.java](BrowserFullSessionComp.md) | file | 浏览器会话组件，包含左右分屏、标签页和加载指示器。 |
| [BrowserAbstractSessionModel.java](BrowserAbstractSessionModel.md) | file | 浏览器会话模型类，管理标签页列表、选中项和忙碌状态，支持异步关闭和同步打开/关闭操作。 |
| [action](action/_module.md) | package | 输入内容为空，无法生成总结。请提供具体内容。 |
| [file](file/_module.md) | package | BrowserFileSystemCache管理用户组信息；BrowserFileSystemHelper处理路径；BrowserConnectionListFilterComp实现过滤；BrowserQuickAccessContextMenu提供快捷菜单；BrowserNavBarComp构建导航栏；BrowserFileListNameCell显示文件名；BrowserFileOpener处理文件操作；BrowserFileSystemTabModel管理标签页；BrowserTransferProgress跟踪传输；BrowserClipboard管理剪贴板；BrowserTransferModel管理下载；BrowserContextMenu创建菜单；BrowserLocalFileSystem处理本地文件；BrowserAlerts提供弹窗；BrowserFileSystemTabComp构建浏览器界面；BrowserHistorySavedStateImpl管理历史记录；BrowserOverviewComp展示概览；BrowserFileSelectionListComp管理选择列表；BrowserTerminalDockTabModel管理终端；BrowserFileListFilterComp实现过滤；BrowserFileListModel管理文件列表；BrowserBreadcrumbBar构建导航；BrowserFileTransferOperation处理文件传输；BrowserConnectionListComp管理连接列表；BrowserFileOverviewComp展示文件概览；BrowserStatusBarComp构建状态栏；BrowserFileSystemHistory管理历史；BrowserTransferComp处理传输；BrowserHistoryTabModel管理历史标签；BrowserHistoryTabComp展示历史；BrowserFileSystemSavedState保存状态；BrowserFileListCompEntry处理交互；BrowserFileListComp展示文件列表；BrowserGreetingComp显示问候；BrowserEntry管理文件条目。 |
| [icon](icon/_module.md) | package | 浏览器图标管理类：抽象类定义文件/目录类型匹配与图标获取，包含加载、查询方法，支持亮暗主题，线程安全设计。 |


