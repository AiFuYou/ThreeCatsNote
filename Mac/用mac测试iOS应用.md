## 用M芯片的Mac运行iOS包
1. 系统信息-->硬件-->预置UUID，将ID添加到开发者证书
2. 打包机更新证书
3. 下载ipa包双击即可安装到mac（第一次打开app时会提示不安全，设置-->隐私与安全性-->仍要打开）
- 在mac上运行时，会将mac当作 `iPad` 设备
- 下载的bundle存放目录 `Library/Containers/App名称/Data/Documents`
- app关闭后会在后台驻留一段时间，过一会才会真正关闭。如果需要立即关闭，操作 `强制退出` （左上角苹果logo-->强制退出或活动监视器里强制退出）
- 可以在mac启动台（DashBoard）长按删除
