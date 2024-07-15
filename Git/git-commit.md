`git commit`
命令可以带有多种参数，允许你为你的提交定义标题（即提交信息的第一行）和正文。以下是你可以使用的一些常见 `git commit` 选项：

1. `-m` 或 `--message`：
   使用这个参数可以在命令行中直接提供提交信息。对于标题和正文，你可以通过提供多个 `-m` 选项来实现，第一个 `-m`
   会被视为提交信息的标题，之后的每个 `-m` 则用于添加一个新的段落作为正文。

   例如：
   ```shell
   git commit -m "Commit title" -m "Commit body"
   ```

2. `-a` 或 `--all`：
   这个参数让 Git 自动把所有已经追踪的、发生更改的文件添加到提交中，无需先执行 `git add`。

3. `--amend`：
   使用这个参数，你可以修改上一次的提交而不是创建一个新提交。

4. `--no-edit`：
   与 `--amend` 一起使用时，它将使用与上一次提交相同的提交信息，而不会打开编辑器。

5. `--author`：
   允许你更改提交的作者信息。

6. `--signoff` 或 `-s`：
   添加签名到提交信息的末尾，以证明你是该修改的作者，通常用于符合开发者证明原则的项目。

7. `--no-verify` 或 `-n`：
   跳过 `pre-commit` 或者 `commit-msg` 钩子（hook）。

8. `-v` 或 `--verbose`：
   提供更多提交信息，包括差异内容。

9. 可以使用 `--` 参数后跟文件列表来只提交特定文件：
   ```shell
   git commit -- file1.txt file2.txt
   ```

如果要在一次命令中添加提交的标题和正文，通常使用多个 `-m` 选项。如果提交信息很长或者需要更好的格式化，推荐的做法是不带 `-m`
参数执行 `git commit`，这样 Git 将会打开默认的文本编辑器（例如 Vim、Emacs、Nano
等），让你在其中编写提交信息。在编辑器中，第一行会作为提交的标题，留一个空行，然后开始写正文。

如果你更喜欢使用其他编辑器输入提交信息，可以设置环境变量 `GIT_EDITOR` 或配置参数 `core.editor`，如：

```shell
git config --global core.editor "code --wait"
```

上面的命令将 Visual Studio Code 设置为 Git 的默认编辑器。当你运行 `git commit` 时，就会打开 VS Code 并等待你完成提交信息编辑。

# 检查当前有多少个commit未推送

可以编写一个简单的 Bash 脚本来检测当前 Git 仓库中是否有未推送的提交，并获取这些提交的数量。这里有一个示例脚本：

```bash
#!/bin/bash

# 检查是否在一个 git 仓库内
if ! git rev-parse --is-inside-work-tree > /dev/null 2>&1; then
  echo "当前目录不是一个Git仓库."
  exit 1
fi

# 获取未推送的提交数量
uncommitted_count=$(git rev-list --count @{u}..)

if [ $uncommitted_count -eq 0 ]; then
  echo "没有未推送的提交."
else
  echo "有 $uncommitted_count 个未推送的提交."
fi
```

解释：

1. `git rev-parse --is-inside-work-tree` 检查当前目录是否是一个 Git 仓库。若不是，则脚本退出并显示相应信息。
2. `git rev-list --count @{u}..` 获取未推送的提交数量，其中 `@{u}` 代表当前分支的上游分支。这条命令会计算从上游分支到当前分支的提交数量。
3. 根据获取到的数量，脚本会打印出相应的提示信息。

你可以将这个脚本保存为 `check_unpushed_commits.sh`，然后通过以下命令授予可执行权限并运行它：

```sh
chmod +x check_unpushed_commits.sh
./check_unpushed_commits.sh
```

希望这段脚本能满足你的要求！

