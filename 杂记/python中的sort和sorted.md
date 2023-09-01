## sorted和sort的区别和使用

在Python中，`sorted`和`list.sort`是两种不同的方法，用于对列表（或可迭代对象）进行排序。它们的主要区别在于用法和行为：

1. **`sorted`函数**：
   - `sorted`是一个全局函数，不仅适用于列表，还适用于任何可迭代对象（如元组、字符串、集合等）。
   - 它接受一个可迭代对象作为输入，并返回一个新的已排序的列表，不会改变原始列表。
   - 可以通过参数来自定义排序规则，例如使用`key`参数来传递一个排序函数。
   - `sorted`的语法：`sorted(iterable, key=key_function, reverse=reverse_flag)`

示例使用`sorted`函数：

```python
original_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
sorted_list = sorted(original_list)
print(sorted_list)  # 输出：[1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]
```

2. **`list.sort`方法**：
   - `sort`是列表对象的方法，只能用于列表。
   - 它在原地对列表进行排序，即会修改原始列表，而不会返回新的列表。
   - 与`sorted`不同，不需要创建新的列表对象，所以在大数据集上可能会更高效。
   - 同样可以使用`key`和`reverse`参数来自定义排序规则。
   - `list.sort`的语法：`list.sort(key=key_function, reverse=reverse_flag)`

示例使用`list.sort`方法：

```python
original_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
original_list.sort()
print(original_list)  # 输出：[1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]
```

总结：如果你想要保留原始列表不变，并获得一个已排序的副本，可以使用`sorted`函数。如果你想要原地修改列表并进行排序，可以使用`list.sort`方法。