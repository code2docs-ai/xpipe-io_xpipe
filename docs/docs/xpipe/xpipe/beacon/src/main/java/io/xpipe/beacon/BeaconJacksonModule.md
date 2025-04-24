# 基础信息

|      |      |
|------|------|
| 名称 | BeaconJacksonModule |
| 编码语言 | .java |
| 代码路径 | xpipe/beacon/src/main/java/io/xpipe/beacon/BeaconJacksonModule.java |
| 包名 | io.xpipe.beacon |
| 依赖项 | ['com.fasterxml.jackson.databind.jsontype.NamedType', 'com.fasterxml.jackson.databind.module.SimpleModule'] |
| 概述说明 | BeaconJacksonModule注册BeaconClientInformation和BeaconAuthMethod的子类型。 |

# 说明

这段内容描述了一个名为BeaconJacksonModule的类，继承自SimpleModule。该类重写了setupModule方法，用于注册多个子类型。具体注册了两组子类型：第一组包含BeaconClientInformation的三个内部类（Api、Cli、Daemon），第二组包含BeaconAuthMethod的两个内部类（Local、ApiKey）。这些注册操作通过SetupContext的registerSubtypes方法完成。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| BeaconJacksonModule | class | BeaconJacksonModule注册BeaconClientInformation和BeaconAuthMethod的子类型。 |



## 类 BeaconJacksonModule

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | BeaconJacksonModule |
| 说明 | BeaconJacksonModule注册BeaconClientInformation和BeaconAuthMethod的子类型。 |


### UML类图

```mermaid
classDiagram
    class BeaconJacksonModule {
        +setupModule(SetupContext context) void
    }
    class SimpleModule {
        <<Interface>>
    }
    class SetupContext {
        <<Interface>>
        +registerSubtypes(NamedType... types) void
    }
    class NamedType {
        +NamedType(Class~?~ type)
    }
    class BeaconClientInformation {
        <<Interface>>
    }
    class BeaconAuthMethod {
        <<Interface>>
    }

    BeaconJacksonModule --|> SimpleModule : 继承
    BeaconJacksonModule --> SetupContext : 使用
    BeaconJacksonModule --> NamedType : 创建
    NamedType --> BeaconClientInformation : 关联
    NamedType --> BeaconAuthMethod : 关联
```

这段代码展示了一个BeaconJacksonModule类，它继承自SimpleModule接口，主要用于配置Jackson的序列化/反序列化模块。该类重写了setupModule方法，通过SetupContext注册了BeaconClientInformation和BeaconAuthMethod的子类型（Api、Cli、Daemon、Local、ApiKey）。类图清晰地展示了继承关系、接口实现以及类之间的依赖关系，核心功能是通过NamedType动态注册子类型以便Jackson能够正确处理多态类型。


### 内部方法调用关系图

```mermaid
graph TD
    A["类BeaconJacksonModule"]
    B["继承: SimpleModule"]
    C["重写方法: setupModule(SetupContext context)"]
    D["调用: context.registerSubtypes(NamedType...)"]
    E["注册子类: BeaconClientInformation.Api"]
    F["注册子类: BeaconClientInformation.Cli"]
    G["注册子类: BeaconClientInformation.Daemon"]
    H["注册子类: BeaconAuthMethod.Local"]
    I["注册子类: BeaconAuthMethod.ApiKey"]

    A --> B
    A --> C
    C --> D
    D --> E
    D --> F
    D --> G
    C --> D
    D --> H
    D --> I
```

这段代码是BeaconJacksonModule类的实现，继承自SimpleModule，主要用于配置Jackson模块的子类型注册。通过重写setupModule方法，分两次调用registerSubtypes注册了BeaconClientInformation和BeaconAuthMethod的多个子类，包括Api、Cli、Daemon以及Local和ApiKey。这些注册操作使得Jackson能够正确识别和处理这些子类的序列化与反序列化。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| setupModule | void | 注册BeaconClientInformation和BeaconAuthMethod的子类型。 |




