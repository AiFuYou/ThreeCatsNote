#### 要使用awscli刷新CDN缓存，您可以执行以下步骤：
1. 安装和配置`AWS CLI`：确保您已经在系统上安装了`AWS CLI`，并正确地配置了您的AWS凭证，使其能够与您的AWS账号相关联。
2. 创建一个`Invalidation`对象：使用以下命令创建一个包含要刷新的文件列表的`Invalidation`对象。
3. ```shell
    aws cloudfront create-invalidation --distribution-id DISTRIBUTION_ID --paths /path1/file1 /path2/file2 /path3/file3 ...
    ```
    在上面的命令中，将`DISTRIBUTION_ID`替换为您要刷新的CDN分发的ID。`/path1/file1 /path2/file2 /path3/file3`是您要刷新的文件列表。请注意，路径应该以斜杠（/）开头。
4. 等待CDN缓存刷新完成：刷新CDN缓存需要一些时间，具体取决于您的文件数量和CDN配置。您可以使用以下命令来检查Invalidation对象的状态。
    ```shell
    aws cloudfront get-invalidation --distribution-id DISTRIBUTION_ID --id INVALIDATION_ID 
    ```
    在上面的命令中，将`DISTRIBUTION_ID`替换为CDN分发的ID，将`INVALIDATION_ID`替换为`Invalidation`对象的ID。
5. 监控刷新进度：使用以下命令可以监视CDN缓存刷新的进度。
6. ```shell
    aws cloudfront list-invalidations --distribution-id DISTRIBUTION_ID
    ```
    上述命令将列出所有与指定CDN分发关联的Invalidation对象信息，包括每个Invalidation对象的状态和创建时间。

请确保在执行上述命令时，将实际的分发ID和文件路径替换为您自己的值。