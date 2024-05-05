## neo4j导出导入数据库

### 脚本

```python
# -*- encoding: utf-8 -*-
"""
    @File    :   neo4j_import.py
    @Time    :   2023/09/04 22:31:38
    @Author  :   mkid 
    @Version :   1.0
    @Note    :   neo4j数据导入导出脚本
"""


from py2neo import Graph, Node, Relationship
import json
import argparse

def parser_arguments():
    parser = argparse.ArgumentParser(description='neo4j数据导入导出脚本')
    parser.add_argument('-mode', type=str, default='dump', help='dump导出，import导入')
    parser.add_argument('-file', type=str, default='graph.json', help='neo4j数据导出/导入的保存路径')
    args = parser.parse_args()
    return args


config_dict = {
    "neo4j_url": "http://localhost:7474",
    "neo4j_username": "neo4j",
    "neo4j_password": "123456",
}

# graph.db数据导出
def graph_dump(save_path):
    """
    把neo4j默认数据库中的数据保存为一个json文件
    Args:
        save_path: 保存neo4j中所有数据的json文件
    Returns:
        None
    """
    print("开始导出......")
    graph = Graph(config_dict['neo4j_url'], auth=(config_dict['neo4j_username'], config_dict['neo4j_password']))
    cypher = "MATCH (n) RETURN n"
    result = graph.run(cypher).data()
    
    nodes = []
    for record in result:
        node = record['n']
        nodes.append({
            'labels': list(node.labels),
            'properties': dict(node)
        })
    
    cypher = "MATCH (n)-[r]->(m) RETURN n, r, m"
    result = graph.run(cypher).data()

    relationships = []
    for record in result:
        node1 = record['n']
        relation = record['r']
        node2 = record['m']
        relationships.append({
            'type': type(relation).__name__,
            'start_node': node1.identity,
            'end_node': node2.identity,
            'properties': dict(relation)
        })
    
    with open(save_path, 'w', encoding='utf-8') as json_file:
        json.dump({
            "nodes": nodes,
            "relationships": relationships
        }, json_file, ensure_ascii=False, indent=4)
    print(f"导出成功，导出路径是: {save_path}")


def graph_import(filename):
    """
    从json文件中读取数据，并把数据插入neo4j数据库中
    Args:
        filename: 保存neo4j数据的json文件
    Returns:
        None
    """
    print("开始导入...")
    graph = Graph(config_dict['neo4j_url'], auth=(config_dict['neo4j_username'], config_dict['neo4j_password']))
    with open(filename, 'r', encoding='utf-8') as json_file:
        data = json.load(json_file)
    
    for node_data in data['nodes']:
        labels = node_data['labels']
        properties = node_data['properties']
        
        node = Node(*labels, **properties)
        graph.create(node)
    
    for rel_data in data['relationships']:
        rel_type = rel_data['type']
        start_node = rel_data['start_node']
        end_node = rel_data['end_node']
        properties = rel_data['properties']
        relationship = Relationship(start_node, rel_data, end_node, **properties)
        graph.create(relationship)

    print("导入成功。")
        


if __name__ == "__main__":
    args = parser_arguments()
    if args.mode == 'dump':
        graph_dump(args.file)
    if args.mode == 'import':
        graph_dump(args.file)
```



### 导出（没用）

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

#### 导出例子（没用）

```
./neo4j-admin dump --database=graph.db --to=F:\\code\\eryuan\\小系统代码\\graph.db.dump
```

环境变量：E:\Neo4j\neo4j-community-3.5.9\bin