安装

```shell
brew install jenkins-lts
```

启动（包含开机启动）

```shell
brew services start jenkins-lts
```

停止

```shell
brew services stop jenkins-lts
```

重新启动

```shell
brew services restart jenkins-lts
```

更新

```shell
brew upgrade jenkins-lts
```

```
To start jenkins-lts now and restart at login:
  brew services start jenkins-lts
Or, if you don't want/need a background service you can just run:
  /opt/homebrew/opt/openjdk@17/bin/java -Dmail.smtp.starttls.enable\=true -jar /opt/homebrew/opt/jenkins-lts/libexec/jenkins.war --httpListenAddress\=127.0.0.1 --httpPort\=8080
```

修改httpListenAddress为0.0.0.0以使局域网访问Jenkins。文件位置可能会有不同，可根据下一条线索去查找

```shell
/opt/homebrew/Cellar/jenkins-lts/2.414.2/homebrew.mxcl.jenkins-lts.plist
```

mac根据系统版本或芯片或设置的不同，以上文件的位置也会不同，可以从以下文件中找到java运行环境的安装位置，反向再找jenkins的安装位置

```shell
/Users/blowfire/Library/LaunchAgents/homebrew.mxcl.jenkins-lts.plist
```

开启访问Jenkins的UserContent目录html文件的权限

```
在配置文件中添加：<string>-Dhudson.model.DirectoryBrowserSupport.CSP=true</string>
通过Jenkins界面去设置：System.setProperty("hudson.model.DirectoryBrowserSupport.CSP", "")
```
