我们先在系统/资源库/Extensions找到一个驱动

*AppleGraphicsControl.kext*

我们把它复制到你的桌面，右键显示包内容*/Contents/PlugIns/AppleGraphicsDevicePolicy.kext*右键显示包内容*/Contents/Info.plist*可以使用文本编辑打开或者其他软件，usb键盘按住win+f调出搜索，ps2按住alt+f，搜索ConfigMap，看到下面以mac开头的id了吗？

![截屏2020-03-15 下午5.29.17.png](http://bbs.pcbeta.com/data/attachment/forum/202003/15/172945qvznq5l8ldd1elll.png)



下面展示OC的方法，打开occ选择自己的机型

找到以后我们查看自己的Board-id（就是左边那一条而已）

![截屏2020-03-15 下午5.31.33.png](http://bbs.pcbeta.com/data/attachment/forum/202003/15/173339uvnpkm4tk049nuk9.png)



再展示clover的方法，打开cc

![截屏2020-03-15 下午5.34.59.png](http://bbs.pcbeta.com/data/attachment/forum/202003/15/173652cbeshzqp3vvccxnc.png)



然后咱们把自己的Board-id复制，在刚刚的配置文件找到带有none字样的ID把咱们的ID替换上面的ID，看不懂的话以下图为参考 

![截屏2020-03-15 下午5.39.33.png](http://bbs.pcbeta.com/data/attachment/forum/202003/15/174326d7w5vchae77lwh5c.png)



替换或添加完你的机型Board-ID就可以保存了，之后14系统直接使用Kext Utility注入我们改好的驱动AppleGraphicsControl，注意必须要最外层的驱动注入单个AppleGraphicsDevicePolicy.kext是无效的。

15.x.x输入以下代码打开系统读写权限

1. ```
   sudo su
   sudo mount -uw /
   killall Finder
   ```

   

**bigsur 请查看我的. 解锁sip.md**

其次我直接上传我已经修改好的即可

记得按照sip那一篇手动刷新系统缓存

然后注入驱动，重启即可享用HDMI(在重启的时候可能会出现panic,请直接关机开机)
