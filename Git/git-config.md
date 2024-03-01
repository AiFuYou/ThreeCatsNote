在 Git 中，您可以针对特定仓库配置用户信息（用户名和电子邮件地址），这样对于该仓库的提交就会使用这些特定的配置信息，而不是使用全局配置。以下是如何进行配置的步骤：

1. 打开命令行工具（例如 Terminal 或 CMD）。

2. 切换到您想要配置的 Git 仓库的目录下。例如:

   ```shell
   cd /path/to/your/repo
   ```

3. 使用以下命令配置本仓库的用户名和电子邮件地址：

   ```shell
   git config user.name "Your Name"
   git config user.email "your_email@example.com"
   ```

以上命令中的 `"Your Name"` 应替换为您想要设定的用户名，`"your_email@example.com"` 应替换为您的电子邮件地址。

这些命令会分别在当前仓库的配置文件 `.git/config` 中添加或修改对应的条目。您可以通过查看那个文件来确认配置是否完成：

```shell
cat .git/config
```

或者使用下面的命令来分别检查配置的用户名和电子邮件：

```shell
git config user.name
git config user.email
```

如果您需要配置的是所有Git仓库的用户信息，可以通过添加 `--global` 选项来设定全局配置：

```shell
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

全局配置会被保存在您用户目录下的全局配置文件中（一般是 `~/.gitconfig` 或者 `~/.config/git/config`），而不是保存在某个特定的仓库中。当您在没有配置仓库特定用户信息的仓库中进行提交时，Git 会使用这些全局设置。
