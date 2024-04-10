在 shell 中异步运行多个 Python 脚本，你可以分别在后台运行它们，并使用 `wait` 命令来等待所有后台进程完成。在 Bash 脚本中，这可以通过使用 `&` 将命令放入后台来实现，然后收集每个后台任务的进程 ID，并使用 `wait` 。

以下是一个简单的示例，展示了如何在 shell 中为每个文件异步运行 Python 脚本，并等待它们全部完成：

```bash
#!/bin/bash

# 假设 files.txt 包含文件列表，每行一个
file_list="files.txt"

# 读取文件列表，为每个文件异步运行 Python 脚本
while IFS= read -r file
do
    # 在后台异步执行 Python 脚本，并传递文件名作为参数
    python your_script.py "$file" &
    
    # 将后台任务的 PID 加入数组中
    pids+=($!)
done < "$file_list"

# 等待所有后台 Python 脚本完成
for pid in ${pids[*]}; do
    wait $pid
done

# 此时所有 Python 脚本都已完成，以下为后续操作
echo "所有 Python 脚本执行完毕。"
```

确保将 `your_script.py` 替换为你的 Python 脚本的路径，该脚本应有处理单个文件的逻辑。变量 `file_list` 包含指向文件列表的路径，其中每个文件的路径占一行。

`&` 符号将 Python 脚本推入后台运行，`$!` 返回最近一个后台作业的进程 ID（PID），`pids` 数组用来收集所有后台作业的 PID。循环结束后，脚本将遍历所有 PID 并使用 `wait` 命令等待这些后台任务完成。这意味着 shell 脚本会在这些 Python 脚本运行完成后继续执行。

要注意的是，当在后台运行多个进程时，如果这些进程会影响到相同的资源（比如写入同一个文件），就需要在 Python 脚本内做好并发控制，避免冲突和数据损坏。
