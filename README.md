## ASUS-A450J-X450JF--EFI

### Clover - 10.15.7
### Opencore 0.6.4 - 11.0.1
```shell
华硕ASUS-A450J(X450JF) EFI
i7 - 4700hq
hd4600
gt745m
光驱 日立LG GU71N
alc269
无线网卡 高通ar9285（蓝牙不可用）
在BIGSUR已更改为博通94532HMB（接力 随航都ok）
详情请到我的csdn
```



### 配置图

[![DYDYMF.jpg](https://s3.ax1x.com/2020/11/23/DYDYMF.jpg)](https://imgchr.com/i/DYDYMF)

### 完成程度
```
修复核显
修复hdmi及其音频
修复触摸板及外设
定制USB
修复麦克风
修复睡眠
修复网卡（94352hmb）
值得一提的是，如果采用oc软件，扫描kexts请删除4360那个博通驱动，否则不开机

默认开启跑码-v
默认关闭sip
```

[![Dye3jJ.png](https://s3.ax1x.com/2020/11/28/Dye3jJ.png)](https://imgchr.com/i/Dye3jJ)
[![DyeGu9.png](https://s3.ax1x.com/2020/11/28/DyeGu9.png)](https://imgchr.com/i/DyeGu9)
[![DyeJBR.png](https://s3.ax1x.com/2020/11/28/DyeJBR.png)](https://imgchr.com/i/DyeJBR)
[![Dye1c4.png](https://s3.ax1x.com/2020/11/28/Dye1c4.png)](https://imgchr.com/i/Dye1c4)

## 个人历程

从一开始，开机不会用苹果的键盘大小写*（大小写按键变为win的shift）*

*(ctrl变为alt就是command按键)*

最开始请咸鱼的修复网卡驱动之类巴拉巴拉，大约七七八八花了60，诶后面发现，好多都不行，我就自己爬heipg.cn的文档，再不停的爬远景和哔哩哔哩。

最后的问题就在于无线网卡ar9285和核显hd4600。

#### 核显

问题在于设备pci总线，配置的时候要带一个hda-gfx = 0的参数才会生效

但是这样引导的核显会花屏，无论改不改fbmen和stolenmen这些个参数，无效，并且在短短一个晚上诠释了排列组合。

在今天早上尝试用最简单的fakeid方式成功完成引导。
#### 声卡
alc269
我没有采用applealc，原因是驱动不完美，仅仅有输入输出。
因此继续采用voodohda，在启动项注入*alcid=35*


#### 网卡

（ar9285）

首先苹果删除了10.14.4以后的这款驱动，这里有两个办法。

**1.**给ar9285刷硬件id，你可以到远景论坛获取相关资料，值得一提的是需要在win8.1及其以下系统操作，win10无论禁用驱动签名与否，都没有办法运行。

（我采用吻妻的win7）

**2.**（不推荐）在10.15以后，你需要先解锁sle

`sudo mount -uw /`

`killall Finder`

然后再进行文件的替换，不过这里值得一提的是，由于玄学问题，你可能会遇到系统崩溃然后重装。

并且默认的网卡硬件id是2b，所以在sle的文件，你还需要对后缀为40的插件，info.plist进行修改数值，再运行一次kext重载缓存。

后续已经更换为94252hmb,完美使用接力与随航
值得一提，你需要把机型更新为18年以后的pro，并且校验三码过后，蓝牙连接一次airpods，播放音乐，ipad关闭今天视图，并且尝试用数据线连接电脑。
成功以后就可以在局域网使用随航和接力了。

### 安装必看
请各位留意config.plist
kernel---apple***cfg**

开头横着有两个请勾选
