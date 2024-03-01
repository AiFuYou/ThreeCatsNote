拷贝文件/文件夹到远程，新老文件一并替换
```shell
aws s3 cp $localpath $s3Path
```

从远程同步文件/文件夹到本地，该命令只会同步新文件
```shell
aws s3 sync $s3Path $localPath --exclude "*" --include "*.txt" --dryrun
```
`--exclude "*"` 忽略所有文件<br>
`--include "*.txt"` 包含txt后缀文件<br>
`--dryrun` 有此参数，则只对比差异，告诉你那些文件将被同步，无此参数，则会直接进行同步
