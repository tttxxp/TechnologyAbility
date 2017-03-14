# Apk安装失败
---

## INSTALL_FAILED_UPDATE_INCOMPATIBLE / DELETE_FAILED_INTERNAL_ERROR
### 描述：
* 使用adb install -r Test.apk命令出现INSTALL_FAILED_UPDATE_INCOMPATIBLE
* 使用adb uninstall package命令时出现DELETE_FAILED_INTERNAL_ERROR

### 解决办法：
当对测试硬件具有root权限时
* adb shell进入/data/app或/data/data或/system/app删除对应的apk文件及包名目录
* 退出adb shell，执行adb pull /data/system/packages.xml
* 删除packages.xml对应的包含apk包名的一段数据，保存退出
* adb push packages.xml data/system/packages.xml
* adb reboot重启之后重新安装，即可安装成功