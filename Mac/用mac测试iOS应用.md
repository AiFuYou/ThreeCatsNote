## 用M芯片的Mac运行iOS包
1. 系统信息-->硬件-->预置UUID，将ID添加到开发者证书
2. 打包机更新证书
3. 下载ipa包双击即可安装到mac（第一次打开app时会提示不安全，设置-->隐私与安全性-->仍要打开）
- 在mac上运行时，会将mac当作 `iPad` 设备
- 下载的bundle存放目录 `Library/Containers/App名称/Data/Documents`
