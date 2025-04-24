# 基础信息

|      |      |
|------|------|
| 名称 | AttachmentHelper |
| 编码语言 | .java |
| 代码路径 | xpipe/app/src/main/java/io/xpipe/app/issue/AttachmentHelper.java |
| 包名 | io.xpipe.app.issue |
| 依赖项 | ['org.apache.commons.io.IOUtils', 'java.io.File', 'java.io.FileInputStream', 'java.io.FileOutputStream', 'java.io.IOException', 'java.nio.file.Path', 'java.util.zip.ZipEntry', 'java.util.zip.ZipOutputStream'] |
| 概述说明 | Java类实现目录压缩为ZIP文件功能。 |

# 说明

该代码描述了一个用于压缩文件的工具类AttachmentHelper，包含两个静态方法。compressZipfile方法接收源目录和目标文件路径，创建ZipOutputStream并调用compressDirectoryToZipfile进行压缩，最后关闭流并返回输出文件路径。compressDirectoryToZipfile是递归方法，遍历源目录下的所有文件和子目录，将文件内容写入ZIP输出流，使用相对路径创建ZipEntry，并通过IOUtils工具类处理流的复制和关闭操作。整个过程实现了将指定目录递归压缩为ZIP文件的功能。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| AttachmentHelper | class | Java类实现目录压缩为ZIP文件功能。 |



## 类 AttachmentHelper

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | AttachmentHelper |
| 说明 | Java类实现目录压缩为ZIP文件功能。 |


### UML类图

```mermaid
classDiagram
    class AttachmentHelper {
        +Path compressZipfile(Path sourceDir, Path outputFile) throws IOException
        -void compressDirectoryToZipfile(Path rootDir, Path sourceDir, ZipOutputStream out) throws IOException
    }

    class ZipOutputStream {
        +void putNextEntry(ZipEntry e) throws IOException
    }

    class ZipEntry {
        +ZipEntry(String name)
    }

    class FileInputStream {
        +FileInputStream(String name) throws FileNotFoundException
    }

    class IOUtils {
        <<static>>
        +void copy(InputStream input, OutputStream output) throws IOException
        +void closeQuietly(Closeable closeable)
    }

    AttachmentHelper --> ZipOutputStream : 使用
    AttachmentHelper --> ZipEntry : 创建
    AttachmentHelper --> FileInputStream : 使用
    AttachmentHelper --> IOUtils : 调用静态方法
    ZipOutputStream --> ZipEntry : 处理
```

这段代码展示了一个压缩工具类AttachmentHelper，主要功能是将目录压缩为ZIP文件。类图清晰地展示了其与Java I/O类的交互关系：通过ZipOutputStream处理压缩流，使用ZipEntry创建压缩条目，借助FileInputStream读取文件内容，并调用IOUtils工具类进行流操作。压缩过程采用递归方式处理子目录，体现了典型的组合模式应用场景。


### 内部方法调用关系图

```mermaid
graph TD
    A["类AttachmentHelper"]
    B["静态方法: compressZipfile(Path sourceDir, Path outputFile)"]
    C["创建ZipOutputStream"]
    D["调用compressDirectoryToZipfile"]
    E["关闭zipFile流"]
    F["返回outputFile"]
    G["私有方法: compressDirectoryToZipfile(Path rootDir, Path sourceDir, ZipOutputStream out)"]
    H["获取文件列表files"]
    I["检查files是否为null"]
    J["遍历files"]
    K["判断是否为目录"]
    L["递归调用compressDirectoryToZipfile"]
    M["创建ZipEntry"]
    N["写入文件到zip流"]
    O["打开文件输入流"]
    P["IOUtils.copy复制数据"]
    Q["关闭输入流"]

    A --> B
    B --> C
    B --> D
    B --> E
    B --> F
    A -.-> G
    G --> H
    G --> I
    G --> J
    J --> K
    K -- 是 --> L
    K -- 否 --> M
    M --> N
    N --> O
    O --> P
    P --> Q
```

这段代码实现了一个ZIP压缩工具类，主要包含两个方法：compressZipfile作为入口方法创建压缩流并调用核心压缩方法，compressDirectoryToZipfile递归处理目录结构。流程图清晰展示了从初始化压缩流、递归遍历目录结构、处理文件/目录判断、写入压缩条目到最终关闭流的完整流程，特别突出了递归处理目录和文件复制两个关键路径。所有IO操作都包含在try-with-resources或显式关闭逻辑中，体现了良好的资源管理实践。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| compressDirectoryToZipfile | void | 递归压缩目录到ZIP文件，处理子目录和文件。 |
| compressZipfile | Path | 压缩目录为ZIP文件，返回输出路径。 |




