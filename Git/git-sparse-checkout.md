### git只克隆指定内容
在 Git 中，如果你想要克隆一个仓库但只同步指定目录的内容，你可以使用 `sparse-checkout` 功能。这是一项实验性功能，它允许用户仅检出一个仓库的特定子集。以下是使用 `sparse-checkout` 功能的一般步骤：
1. 首先，你需要克隆远程仓库，但不立即检出文件。
   ```shell
   git clone --no-checkout https://github.com/user/repo.git
   ```
2. 进入刚克隆的仓库目录：
   ```shell
   cd repo
   ```
3. 初始化 `sparse-checkout` 文件，这会允许你配置你希望的路径。
   ```shell
   git sparse-checkout init --cone
   ```
4. 设置你希望仅检出的特定目录。例如，如果你只想同步 `docs/` 目录，可以这样设置：
   ```shell
   git sparse-checkout set docs/
   ```
5. 最后执行检出：
   ```shell
   git checkout <branch-name>
   ```
这将只检出 `docs/` 目录中的内容，而不是整个仓库。
请注意，`sparse-checkout` 是 Git 2.25+ 版本引入的改进特性，因此，如果你使用的 Git 版本较旧，可能需要手动配置 `sparse-checkout`：
```shell
git config core.sparseCheckout true
```
然后，手动编辑 `.git/info/sparse-checkout` 并添加你希望检出的路径规则。
不同的 Git 版本操作可能有所不同，请确保参考你目前使用的版本的 Git 文档。
总结一下，通过这种方式，你可以让 Git 仅克隆并同步你指定的目录，而不是整个仓库的所有文件。

### git操作已有仓库，只保留下想要的内容
如果你已经克隆了整个仓库并切换到了指定分支，但现在只想留下指定目录的文件，你可以使用 `sparse-checkout` 功能来实现这一需求。以下是调整现有仓库以仅包含指定目录的步骤：
1. 在仓库根目录下启用 `sparse-checkout` 功能：
   ```shell
   git config core.sparseCheckout true
   ```
2. 在 `.git/info/` 目录下创建或编辑 `sparse-checkout` 文件，并声明你想要包含在检出中的目录模式：
   ```shell
   echo 'path/to/your/directory/' >> .git/info/sparse-checkout
   ```
   请替换 `path/to/your/directory/` 为你实际希望保留的目录。注意结尾的斜杠 `/` 表示目录，这对 Git 来说很重要。
3. 读取 `sparse-checkout` 配置并更新你的工作目录，以仅包含指定的文件和目录：
   ```shell
   git read-tree -m -u HEAD
   ```
这个命令会删除你的工作目录中未包含在 `sparse-checkout` 文件中声明的所有文件和目录，只保留声明的路径。
确保在执行以上步骤之前，保存你对仓库中的所有重要工作的任何修改，因为这些命令可能会删除未包含在 `sparse-checkout` 文件中的路径的文件。
如果想添加其他文件或目录到你的 `sparse-checkout` 配置，只需编辑 `.git/info/sparse-checkout` 文件，然后再次运行 `git read-tree -m -u HEAD`。
从 Git 2.25.0 版本开始，Git 提供了一个新的 `sparse-checkout` 命令用来更方便地管理这些配置。如果你使用的 Git 版本是 2.25 或更高，你可能想使用这种方法：
```shell
# 首先初始化 sparse-checkout
git sparse-checkout init --cone
# 使用 set 命令来指定仅需要的目录
git sparse-checkout set path/to/your/directory/
# 查看现在的 sparse-checkout 列表
git sparse-checkout list
```
记得将 `path/to/your/directory/` 替换成你实际想要的路径。如果你已经在一个默认的 checkout 过程中，`git sparse-checkout set` 命令将把你的仓库文件设置到你指定的路径。
