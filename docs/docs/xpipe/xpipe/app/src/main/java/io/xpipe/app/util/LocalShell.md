# 基础信息

|      |      |
|------|------|
| 名称 | LocalShell |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/util/LocalShell.java |
| 包名 | io.xpipe.app.util |
| 依赖项 | ['io.xpipe.app.ext.ProcessControlProvider', 'io.xpipe.app.issue.ErrorEvent', 'io.xpipe.core.process.ProcessOutputException', 'io.xpipe.core.process.ShellControl', 'io.xpipe.core.process.ShellDialect', 'io.xpipe.core.process.ShellDialects', 'lombok.Getter', 'lombok.SneakyThrows'] |
| 概述说明 | 本地Shell管理类，含初始化、重置、获取Shell及PowerShell功能，支持缓存和异常处理。 |

# 说明

LocalShell类管理本地Shell进程和缓存，提供初始化、重置、获取Shell控制对象等功能。包含静态方法init初始化本地Shell，reset强制或优雅终止进程，getLocalPowershell获取PowerShell实例，isLocalShellInitialized检查初始化状态，getShell获取当前Shell控制对象，getDialect获取当前Shell方言。通过LocalShellCache缓存数据，处理异常时记录错误事件。支持强制终止或等待进程正常退出，确保资源释放。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| LocalShell | class | 本地Shell管理类，含初始化和重置功能，支持PowerShell子进程控制。 |



## 类 LocalShell

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | LocalShell |
| 说明 | 本地Shell管理类，含初始化和重置功能，支持PowerShell子进程控制。 |


### UML类图

```mermaid
classDiagram
    class LocalShell {
        -static ShellControl local
        -static ShellControl localPowershell
        +static LocalShellCache localCache
        +static void init() throws Exception
        +static void reset(boolean force)
        +static ShellControl getLocalPowershell() throws Exception
        +static boolean isLocalShellInitialized()
        +static ShellControl getShell() throws SneakyThrows
        +static ShellDialect getDialect()
    }

    class LocalShellCache {
        // 由@Getter注解生成的getter方法
    }

    class ShellControl {
        <<Interface>>
        +start() ShellControl
        +exitAndWait() void
        +kill() void
        +subShell(ShellDialect dialect) ShellControl
    }

    class ProcessControlProvider {
        <<Interface>>
        +get() ProcessControlProvider
        +createLocalProcessControl(boolean) ShellControl
        +getEffectiveLocalDialect() ShellDialect
    }

    class ShellDialects {
        <<Interface>>
        +isPowershell(ShellControl) boolean
        +POWERSHELL ShellDialect
    }

    class ProcessOutputException {
        +withPrefix(String, ProcessOutputException) ProcessOutputException
    }

    class ErrorEvent {
        +fromThrowable(Throwable) ErrorEvent
        +omit() ErrorEvent
        +handle() void
    }

    LocalShell --> ProcessControlProvider : 依赖
    LocalShell --> ShellControl : 依赖
    LocalShell --> LocalShellCache : 包含
    LocalShell --> ShellDialects : 依赖
    LocalShell --> ProcessOutputException : 依赖
    LocalShell --> ErrorEvent : 依赖
    ShellControl <|.. ProcessControlProvider : 实现
    ShellDialects <|.. ProcessControlProvider : 实现
```

这段代码描述了一个本地Shell管理类LocalShell，它负责初始化、重置和获取本地Shell进程控制实例。类图展示了LocalShell与多个接口和类的交互关系，包括ShellControl接口（定义Shell操作）、ProcessControlProvider接口（创建Shell实例）、ShellDialects接口（判断Shell类型）等。LocalShell通过静态方法管理Shell生命周期，支持普通Shell和PowerShell两种模式，并包含异常处理和缓存机制。整个设计体现了对Shell进程的细粒度控制和类型安全处理。


### 内部方法调用关系图

```mermaid
graph TD
    A["类LocalShell"]
    B["属性: static LocalShellCache localCache"]
    C["属性: static ShellControl local"]
    D["属性: static ShellControl localPowershell"]
    E["方法: static init()"]
    F["方法: static reset(boolean force)"]
    G["方法: static getLocalPowershell()"]
    H["方法: static isLocalShellInitialized()"]
    I["方法: static getShell()"]
    J["方法: static getDialect()"]
    K["操作: local = ProcessControlProvider.createLocalProcessControl(false).start()"]
    L["操作: localCache = new LocalShellCache(local)"]
    M["条件: if (local != null)"]
    N["操作: local.exitAndWait()"]
    O["异常处理: ErrorEvent.fromThrowable(e).omit().handle()"]
    P["操作: local.kill()"]
    Q["操作: local = null"]
    R["操作: localCache = null"]
    S["条件: if (localPowershell != null)"]
    T["操作: localPowershell.exitAndWait()"]
    U["操作: localPowershell.kill()"]
    V["操作: localPowershell = null"]
    W["条件: if (ShellDialects.isPowershell(s))"]
    X["操作: localPowershell = ProcessControlProvider.createLocalProcessControl(false).subShell(ShellDialects.POWERSHELL).start()"]
    Y["异常处理: throw ProcessOutputException.withPrefix('Failed to start local powershell process', ex)"]
    Z["操作: return localPowershell.start()"]
    AA["条件: if (local == null)"]
    AB["异常处理: throw new IllegalStateException('Local shell not initialized yet')"]
    AC["操作: return local.start()"]
    AD["操作: return ProcessControlProvider.get().getEffectiveLocalDialect()"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    E --> K
    E --> L
    F --> M
    M -- true --> N
    N --> O
    O --> P
    M -- false --> P
    P --> Q
    Q --> R
    F --> S
    S -- true --> T
    T --> O
    S -- false --> U
    U --> V
    G --> W
    W -- true --> AC
    W -- false --> X
    X --> Y
    X --> Z
    I --> AA
    AA -- true --> AB
    AA -- false --> AC
    J --> AD
```

这段代码流程图展示了LocalShell类的完整控制流程，包含初始化、重置、获取Shell实例等核心操作。类通过静态方法管理本地Shell进程和PowerShell进程的生命周期，采用异常处理机制保证进程终止的可靠性。流程图清晰呈现了条件分支、异常捕获和资源清理的复杂逻辑，特别是reset()方法中根据force参数选择不同终止策略的决策过程，以及getLocalPowershell()方法中Shell类型检查的流程控制。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| localPowershell | ShellControl | 私有静态ShellControl实例localPowershell |
| localCache | LocalShellCache | 私有静态本地缓存变量声明。 |
| local | ShellControl | 私有静态ShellControl变量local |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| init | void | 初始化本地进程控制和缓存 |
| getDialect | ShellDialect | 获取当前有效的本地Shell方言。 |
| getShell | ShellControl | 获取Shell实例，未初始化时抛出异常。 |
| isLocalShellInitialized | boolean | 检查本地Shell是否初始化 |
| getLocalPowershell | ShellControl | 获取本地PowerShell实例，不存在则创建并启动。 |
| reset | void | 静态方法reset根据force参数决定强制或安全终止local和localPowershell进程并清空缓存。 |




