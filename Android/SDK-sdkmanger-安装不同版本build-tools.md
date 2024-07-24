要使用命令行安装Android SDK中的特定版本的Build Tools（例如30.0.3），您可以遵循以下步骤：

### 1. 准备工作
确保你的环境变量已经正确配置，包括`ANDROID_HOME`和`PATH`。这些环境变量应该指向Android SDK的路径。

例如，在Unix/Linux或macOS上，你可以在`~/.bashrc`或`~/.zshrc`中添加：
```sh
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools
```

在Windows上，你可以通过系统属性的环境变量设置界面添加这些路径。

### 2. 使用`sdkmanager`安装
确保你已经安装了`sdkmanager`工具，它通常位于`tools/bin`目录中。然后，你可以通过命令行安装指定版本的Build Tools。

打开你的终端（对于Windows，可以使用命令提示符或PowerShell），然后执行以下命令：
```sh
sdkmanager "build-tools;30.0.3"
```

### 示例步骤
1. **导航到sdkmanager工具所在的位置**（如果没有将其添加到PATH中）：
   ```sh
   cd $ANDROID_HOME/tools/bin
   ```
2. **执行安装命令**：
   ```sh
   ./sdkmanager "build-tools;30.0.3"
   ```
   或者如果`sdkmanager`已经在`PATH`中，可以直接运行：
   ```sh
   sdkmanager "build-tools;30.0.3"
   ```

### 3. 验证安装
安装完成后，你可以验证是否正确安装了指定版本的Build Tools：
```sh
ls $ANDROID_HOME/build-tools/
```
你应该会看到`30.0.3`目录存在。

### 注意事项
- 如果你是第一次使用`sdkmanager`，可能会提示你接受许可协议。需要按照提示接受许可协议才能继续安装。
- 确保你的网络连接正常，因为`sdkmanager`需要从网上下载相应的工具。

执行这些步骤后，你应该就成功通过命令行安装了Android SDK的Build Tools 30.0.3版本。
