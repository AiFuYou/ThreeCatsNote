在Shell脚本中获取当前Git仓库分支名称的命令是：

```bash
git rev-parse --abbrev-ref HEAD
```

下面详细解释这个命令的各个部分：

1. **git**: 这是调用Git命令行工具的基本命令。

2. **rev-parse**: 这是一个Git内部命令，用于操作与Git修订历史相关的各种属性。它能够解析Git中的对象名称、提交ID等，转换为需要的格式。

3. **--abbrev-ref**: 这是`git rev-parse`命令的一个选项，作用是将引用（如标签名、分支名）转化为简短的引用名称。

4. **HEAD**: 在Git中，`HEAD`指向当前的工作头指针，通常用于表示当前检出的快照。在大多数情况下，它指向当前的分支引用。

整体来看，`git rev-parse --abbrev-ref HEAD`命令的作用是获取当前检出的分支的简短名称。

可以使用如下的Shell脚本来实现检查当前Git仓库的分支名称是否为`develop_online`，如果不是，则退出脚本，并返回错误代码1：

```bash
#!/bin/bash

# 获取当前分支名称
current_branch=$(git rev-parse --abbrev-ref HEAD)

# 检查分支是否为develop_online
if [ "$current_branch" != "develop_online" ]; then
    echo "当前分支不是develop_online，脚本将退出。"
    exit 1
else
    echo "当前分支是develop_online。"
fi
```

这段脚本首先通过`git rev-parse --abbrev-ref HEAD`命令获取当前的分支名，然后通过一条`if`
语句检查这个分支名是否为`develop_online`。如果不是，脚本会打印一条消息，并通过`exit 1`
命令退出且返回状态码1（通常用于表示异常情况或错误）。如果分支名是`develop_online`，则会打印确认消息。

# 注意

- 如果有和分支名相同的tag，则checkout分支时，需要使用 `git checkout -b local_branch origin/remote_branch` 才能正确切换到目标分支
- 如果有和分支名相同的tag，则获取到的名为 `heads/develop_online`
