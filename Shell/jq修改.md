`jq` 是一款流行的命令行 JSON 处理工具，非常适合用来解析、过滤、映射和操作 JSON 数据。要使用 `jq` 命令修改 JSON 文件中的值，您可以采取以下步骤：

1. 确定要修改的 JSON 文件路径和要修改的键（key）及其新值。
2. 使用 `jq` 的赋值 (`=`) 操作或更新操作 (`|=`) 修改值。
3. 确保将 `jq` 的输出重定向至一个新文件，或者输出到管道 (`|`) 并覆盖原文件。

下面是一个实例，假设您有一个名为 `data.json` 的 JSON 文件，您希望将 key 为 `username` 的值改为 `new_username`：

```shell
jq '.username = "new_username"' data.json > temp.json && mv temp.json data.json
```

这个命令串做了以下事情：

- `.username = "new_username"`: 使 `jq` 查找键 `username` 并将其值设置为 `"new_username"`。
- `data.json`: 是要处理的原始 JSON 文件。
- `>`: 将 `jq` 命令的结果输出到 `temp.json` 文件中。
- `&&`: 是一个逻辑操作符，表示若前面的命令执行成功后才执行后面的命令。
- `mv temp.json data.json`: 将临时文件 `temp.json` 重命名回 `data.json`，这样就实现了对原文件的「就地修改」。

**注意事项**：

- 一定要先将 `jq` 输出重定向至一个临时文件。如果你直接用 `jq` 输出覆盖原文件，可能会导致数据的不完整。
- 确保你有正确的文件权限去读写这些文件。

如果你想要就地编辑（in-place edit），即直接修改原文件不产生临时文件，可以使用 `sponge` 命令，它在 `moreutils` 包中：

```shell
jq '.username = "new_username"' data.json | sponge data.json
```

`jq` 也可以处理更复杂的结构，例如修改嵌套对象或数组。关键在于使用正确的 `jq` 过滤器来定位到要修改的具体元素。还可以使用 `--arg` 参数传递新值，避免在命令行中硬编码值，特别是处理动态值时。例如：

```shell
newval="new_username"
jq --arg nv "$newval" '.username = $nv' data.json > temp.json && mv temp.json data.json
```

在实际操作中，请根据您的具体需求选择合适的 `jq` 语法和方法。

`--tab` 可用于美化输出