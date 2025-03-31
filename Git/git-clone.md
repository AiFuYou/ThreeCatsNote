使用 git clone 时指定分支有几种方法：

1. 克隆特定分支：

```
git clone -b <branch_name> <remote_repo_url>
```

例如：
```
git clone -b develop https://github.com/user/repo.git
```

这会克隆仓库，并直接切换到 'develop' 分支。

2. 克隆特定分支，并且只获取该分支的历史：

```
git clone -b <branch_name> --single-branch <remote_repo_url>
```

例如：
```
git clone -b develop --single-branch https://github.com/user/repo.git
```

这样可以减少下载的数据量，因为它只获取指定分支的历史。

3. 克隆后切换分支：

如果你已经克隆了仓库，但想切换到特定分支：

```
git clone <remote_repo_url>
cd <repo_directory>
git checkout <branch_name>
```

4. 克隆所有分支，然后切换：

```
git clone <remote_repo_url>
cd <repo_directory>
git branch -a  # 列出所有分支
git checkout <branch_name>
```

5. 克隆特定标签（tag）：

```
git clone -b <tag_name> <remote_repo_url>
```

记住，当你使用 -b 选项时，你可以指定分支名、标签名或者甚至是特定的提交哈希。

选择哪种方法取决于你的具体需求，比如是否需要其他分支的历史，或者是否只关注特定的分支或版本。
