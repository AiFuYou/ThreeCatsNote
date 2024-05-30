`firebase` 命令行安装：
```shell
brew install node
npm install -g firebase-tools
```

`firebase` 配置：
```shell
# 登录
firebase login
# 查看当前登录的用户
firebase login:list
```

上传描述符文件
```shell
firebase crashlytics:symbols:upload --app=FIREBASE_APP_ID PATH/TO/SYMBOLS
```

需要注意描述符文件上传之后发生的crash才可以正常解析，以前的无法再解析