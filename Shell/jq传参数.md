如果您想要传递第二个参数给 `jq` 命令，可以使用 `--arg` 选项来添加额外的参数。下面是如何添加第二个参数 `appName2` 的例子：

```bash
jq -r --arg appName $APP_NAME --arg appName2 $APP_NAME2 '.Dir_Bundle.[$appName].Git.Online, .Dir_Bundle.[$appName2].Git.Online' $JENKINSFILE_CONFIG_FILE
```

在这个例子中，我们添加了第二个 `--arg` 选项，`appName2` 是新的变量名称，`$APP_NAME2` 是包含第二个应用名称的 shell 变量。`jq` 表达式中相应地添加了对 `$appName2` 的引用。

这条命令会分别打印出与 `$APP_NAME` 和 `$APP_NAME2` 相关的 `.Git.Online` 路径。如果您希望这两个输出在同一行上，可以保持上面的表达式。如果想要分行输出，可以使用 `jq` 的多个表达式：

```bash
jq -r --arg appName $APP_NAME --arg appName2 $APP_NAME2 '.Dir_Bundle.[$appName].Git.Online, .Dir_Bundle.[$appName2].Git.Online' $JENKINSFILE_CONFIG_FILE
```

请确保 `$APP_NAME` 和 `$APP_NAME2` 变量被正确地传递并且在环境中有定义。如果您的 JSON 文件结构与查询表达式不匹配，还可能需要根据实际情况调整 `jq` 表达式。
