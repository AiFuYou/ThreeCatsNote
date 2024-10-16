## 用M芯片的Mac运行iOS包
1. 系统信息-->硬件-->预置UUID，将ID添加到开发者证书
2. 打包机更新证书
3. 下载ipa包双击即可安装到mac（隐私与安全-->仍要打开）

- 在mac上运行时，会将mac当作 `iPad8,6` 设备（es可查）
- 下载的bundle存放目录 `Library/Containers/App名称/Data/Documents`，可手动更改目录中的文件进行一些调试
