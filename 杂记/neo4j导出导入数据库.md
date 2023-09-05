## neo4j导出导入数据库

### 查看有哪些数据库



### 导出

要导出Neo4j数据库，您可以使用Neo4j提供的工具和方法之一。以下是一种常见的方法：

使用Neo4j的命令行工具：

1. 打开命令行终端。
2. 导航到Neo4j数据库的安装目录。通常，Neo4j数据库安装在一个目录中，您可以在其中找到bin子目录。
3. 在终端中运行以下命令来导出数据库：
   
   ```
   neo4j-admin dump --database=your_database_name --to=export_directory
   ```

   - `your_database_name`是您要导出的数据库的名称。
   - `export_directory`是导出的数据存储目录。

4. Neo4j将开始导出数据库。导出时间取决于数据库的大小。

5. 完成导出后，您将在`export_directory`目录中找到导出的数据文件。

请注意，导出的数据文件通常包含在Neo4j的二进制格式中，因此如果您要将数据迁移到另一个Neo4j实例或将其导入到其他数据库系统中，您需要使用Neo4j提供的相应工具或方法来完成导入操作。

另外，请确保在执行导出操作之前，Neo4j数据库已停止，以避免数据不一致。在导出之后，您可以使用`neo4j-admin load`命令将数据加载到新的Neo4j实例中。

#### 导出例子

```
./neo4j-admin dump --database=graph.db --to=F:\\code\\eryuan\\小系统代码\\graph.db.dump
```

环境变量：E:\Neo4j\neo4j-community-3.5.9\bin