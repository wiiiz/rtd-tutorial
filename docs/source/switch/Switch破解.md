参考网站：
https://nh-server.github.io/switch-guide/
[SwitchHackingIsEasy](https://rentry.co/SwitchHackingIsEasy)
[Homebrew Guide](https://switch.homebrew.guide/index.html) 这个比较旧了
[switchbrew](https://switchbrew.org/wiki/Main_Page)

### 准备

#### 东西

- switch，充满电的更好
- 有type-c口的数据线，能传数据的那种，一般手机送的线应该都可以。
switch端接器（最好有，省事儿） ^d3a894
- 机器里的tf卡最好是大于64GB的
- tf卡读卡器
- 我的打包文件
- switch短接器

#### 一些术语

- RCM : ReCovery Mode  恢复模式
- firmware：固件，就像更低级的系统，比如主板的固件有BIOS、UEFI。
- OFW : offical firmware 官方固件 （就是不能为所欲为的原装合法系统）
- CFW  : custom firmware 修改过的固件，这里使用的CFW就是Atmosphere（大气层），运行在CFW上拥有更多的权限，比如安装自制软件，修改内存，导出存档等。
- NAND :闪存， 一种存储介质，SSD、tf卡、u盘用的都是NAND，电脑现在一般用SSD，安卓手机用的是UFS，switch使用的是个32G的eMMC，里边有固件（switch原装固件的code name是Horizon，破解团队的魔改固件叫Atmosphere也是有点好笑）。
- EmuNAND : 模拟NAND，就是重新在tf卡上画了一部分空间出来，把它伪装成是机器的原本存放固件的闪存。机器启动的时候读取的是tf卡里的内容，这样在这里乱搞就不会影响到原装固件，方便在需要的时候切换
- emuMMC : 当前正在使用的EmuNAND
- SysNAND : 系统NAND/真实系统 （就是可以为所欲为的合法系统，不建议用，会污染合法系统，一般用EmuNAND）

#### 注意！

- 拔tf卡（microSD卡）之前先[[Switch破解#^a597f5|彻底关机]]。（因为正在跑着的虚拟固件是在tf卡里，直接拔tf卡就像把开着的电脑的硬盘给拔了。不过这么干应该只是有风险，我开机的时候拔过倒是没坏）
- 在使用EmuNAND的时候，因为安装了很多“非法“的东西，在连接到任天堂的服务器的时候，老任检测到设备中的自制软件、盗版软件之类的东西，就会把这个机器ban掉（这个机器就不能使用老任的网络服务了）。有些情况会把账号ban掉（此账号就无法使用任天堂的网络服务了）。为了防止这些，在使用Atmosphere（破解系统）的时候不要使用任天堂的网络服务如：系统升级、eshop、联机游戏。为了更安全，最好屏蔽任天堂的服务器。屏蔽方法：[Blocking Nintendo Servers](https://nh-server.github.io/switch-guide/extras/blocking_nintendo/) 、 [Setup Exosphere / DNS MITM](https://rentry.org/ExosphereDNSMITM) ，屏蔽后可以连接网络，但是无法访问任天堂相关的服务。

#### 检查机器是不是可以破解

看一下序列号：
![[serial_switch.png]]
或者在switch里边，**系统 -> 序列号** 也可以看到。

可以通过网站查询
https://ismyswitchpatched.com/
patched就是漏洞已经被修补了不能破解，unpatched就是漏洞还在，可以破解。

还可以通过查询 [论坛](https://gbatemp.net/threads/switch-informations-by-serial-number-read-the-first-post-before-asking-questions.481215/) 汇总的常见的序列号，来确认switch是否可以破解，见下图

|序列号开头|可以破解|有可能可以破解|破解不了|
|:---|:---|:---|:---|
|XAW1| XAW10000000000 to XAW10074000000 |XAW10074000000 to XAW10120000000|XAW10120000000 and up|
|XAW4|XAW40000000000 to XAW40011000000|XAW40011000000 to XAW40012000000|XAW40012000000 and up|
|XAW7|XAW70000000000 to XAW70017800000|XAW70017800000 to XAW70030000000|XAW70030000000 and up|
|XAJ1|XAJ10000000000 to XAJ10020000000|XAJ10020000000 to XAJ10030000000|XAJ10030000000 and up|
|XAJ4|XAJ40000000000 to XAJ40046000000|XAJ40046000000 to XAJ40060000000|XAJ40060000000 and up|
|XAJ7|XAJ70000000000 to XAJ70040000000|XAJ70040000000 to XAJ70050000000|XAJ70050000000 and up|
|XAK1|N/A|XAK10000000000 and up|N/A|

没出现的其他序列号机器都不能破解。

#### 一些操作

##### 彻底关机：长按电源键->电源选项->关闭电源 ^a597f5

##### 进入RCM：将switch彻底关机后，插上短接器（也就是把pin10接地），先按住音量+不放，再按一下开机键，即可进入RCM，具体如下

^04bfff

把 **右侧** joycon拿下来，可以看到switch右侧露出的用来安装右侧joycon的滑轨：

![[20230130_150812.jpg]]

红色圈圈圈出来的地方，从上往下看是这样的：

![[20230130_151338.jpg]]

红色圈圈圈出来的地方是10个金手指触点，**从左往右**给它们依次编号为1-10

参考[Nintendo_Switch_Reverse_Engineering](https://github.com/dekuNukem/Nintendo_Switch_Reverse_Engineering)10个触点的作用为：

| Joycon Connector Pin |            Function           |                                                       Remarks                                                                       |
|:--------------------:|:-----------------------------:| ----------------------------------------------------------------------------------------------------------------------------------- |
|           1          |              GND              |                                                          -                                                                          |
|           2          |              GND              |                                                          -                                                                          |
|           3          |              Jdet             | HIGH when connected to console via Bluetooth. Joy-Con will not send serial data post-handshake unless pin is pulled LOW by console. |
|           4          |               5V              |                                              Joy-Con power and charging                                                             |
|           5          | Serial data console to Joycon |                                             Inverted level (idle at GND)                                                            |
|           6          |              JRST             |                                      Joy-Con reset signal , high level is reset                                                     |
|           7          |              GND              |                                                          -                                                                          |
|           8          | Serial data Joycon to console |                                            Standard level (idle at 1.8V)                                                            |
|           9          |           Power output        |                             Joy can output power to Ring Fit Adventure or starlink toy                                              |
|          10          |          Flow control         |                             Joy-Con will only send data to console when this line is HIGH                                           |

注：GND是ground，就是电气里边的“地”。

**将switch彻底关机后，把pin10接地，先按住音量+不放，再按一下开机键，即可进入RCM模式** ^9ac4c2

也就是短接10pin和1/2/7中的任何一个都行。短接就是用导电的金属连接相应的pin。

进入RCM成功的标志是switch没有任何反应，还是黑屏，如果看到任何画面，比如开机了什么的，就是没有成功，应该就是没有接好需要[[Switch破解#^a597f5|彻底关机]]重新来一次。

成功后就可以不用短接了，短接器什么的就可以取下来了。不取也没问题，就是右joycon没地儿装...

所以关键问题就是怎么10pin接地，可以自己找点厨房锡纸搓成导线来接，不过还是万能的淘宝买个**短接器**吧，我买的那个等下用微信发你，小小的，插进滑轨就行了。就像这样：

![[jig.gif]]

##### 注入payload（就是把一个``**.bin``程序塞进switch内存，并让它运行）

^61f0a8

1.  运行``switch破解\TegraRcmGUI_v2.6_portable\TegraRcmGUI.exe``
2.  **如果是第一次使用**，需要点 `Settings` 标签, 点 `Install Driver` 装下switch的驱动.
    -  如果装驱动有啥问题叫我
3.  使switch[[Switch破解#^9ac4c2|进入RCM]]，并用数据线连接switch和电脑。
4.  点击电脑上TegraRcmGUI的 `Payload` 标签。
    -  TegraRcmGUI会检测到switch，并且软件界面左下角的switch会变成绿色。
5.  点 `Inject payload`旁边的小文件夹图标, 然后找到你需要的payload也就是相应的`.bin` 文件。
    -  按照流程你第一次需要注入的应该是 `switch破解\bins\TegraExplorer.bin`
6.  点 `Inject payload` 就搞定了，switch上会有反应.

tip：注入payload也可以使用别的设备完成如linux、macOS、Android。具体见[sending_payload](https://nh-server.github.io/switch-guide/user_guide/sysnand/sending_payload/)

### 开搞

#### 第一步，给tf卡重新分区

提前备份：先将switch[[Switch破解#^a597f5|彻底关机]]，取出tf卡，插读卡器，插电脑，把tf卡根目录下的``Nintendo``文件夹拷出来，这个里边是你安装在tf卡的游戏和游戏更新。

**重新插回tf卡！！！**

1.  给switch[[Switch破解#^61f0a8|注入]]`switch破解\bins\TegraExplorer.bin`
    -  忘记了的话翻前边的[[Switch破解#注入payload（就是把一个``**.bin``程序塞进switch内存）]]
2.  switch会进入TegraExplorer的界面，拿起switch，装上joycon，点 `Partition the sd` 点按钮 A 进入格式化tf卡的界面。
    -  记得提前插存储卡兄弟
3.  调到 `Fat32 + EmuMMC` 点 A 。
4.  点 Yes
    -  SD卡格式化了，希望你备份了
    -  应该会几秒就搞定
5.  随便按个什么键回到主菜单。
6.  调到 `Reboot to RCM` 按 A 会自己重启并进入RCM. 让后拔了卡准备下一步。

#### 第二步，往tf卡里拷东西

电脑最好可以显示文件后缀，就是`.exe` `.txt` 之类的。

打开我的电脑->点击上方的 查看 -> 勾选偏右侧有个 `□文件扩展名` 即可

1. 把文件夹 `switch破解\tf卡` 里的所有内容全部拷进tf卡的根目录
2. 把之前备份的内容拷回来
3. 把卡插回switch

#### 第三步，制作虚拟系统（EmuMMC）、备份keys、备份NAND

因为虚拟系统里会安装很多自制程序、盗版游戏之类的（任天堂不允许），所以如果在虚拟系统中使用网络的时候任天堂会知道（这个只联网应该不会，刚刚已经有相应措施来预防了）知道就会ban机（这台机器就不能使用任天堂的网络服务了），所以为了避免ban机，稳妥点是在使用虚拟系统的时候不要联网（使用飞行模式）。所以推荐现在直接正常打开switch，来到网络设置，把所有的已知的wifi全删了，等破解以后使用正版官方系统需要联网的时候再添加使用即可（因为马上制作的虚拟系统是官方系统的拷贝，提前删除wifi，在使用虚拟系统的时候就不用烦神网络的事情了）。

##### 制作emuMMC

1.  [[Switch破解#进入RCM：将switch彻底关机后，插上短接器（也就是把pin10接地），先按住音量+不放，再按一下开机键，即可进入RCM，具体如下|进入RCM]]，[[Switch破解#^61f0a8|注入]]`switch破解\bins\hekate_ctcaer_6.0.1.bin`
2.  使用触屏点击进入 `emuMMC` 菜单
3.  点击 `Create emuMMC`，然后点击 `SD Partition`
4.  点 `Part 1` 。 就开始制作 emummc 了。 完成后点`Close`回到 emuMMC 菜单
5.  点 `Change emuMMC` -> `SD RAW 1`
6.  右上角 `close` 回到主菜单

##### 制作NAND备份

就是备份系统，以免玩脱。

1.  [[Switch破解#进入RCM：将switch彻底关机后，插上短接器（也就是把pin10接地），先按住音量+不放，再按一下开机键，即可进入RCM，具体如下|进入RCM]]，[[Switch破解#^61f0a8|注入]]`switch破解\bins\hekate_ctcaer_6.0.1.bin`
2.  使用触屏进入 `Tools` 菜单，点 `Backup eMMC`
3.  点 `eMMC BOOT0 & BOOT1`
4.  等一下完成
5.  点 `Close` , 然后点 `eMMC RAW GPP`
6.  这个时间长，可能10min-1h （看tf卡的质量了）
7.  如果卡的剩余容量小于32GB，备份可能会分成几个1GB或2GB的文件。
    -   如果在这个时候空间不足了，Hekate就会停住，这个时候：
    -   关机
    -   拔出tf卡连上电脑
    -   把`tf根目录\backup`文件夹里的所有东西剪切出来存在电脑里
    -   重新把卡插回去
    -   [[Switch破解#进入RCM：将switch彻底关机后，插上短接器（也就是把pin10接地），先按住音量+不放，再按一下开机键，即可进入RCM，具体如下|进入RCM]], [[Switch破解#^61f0a8|注入]]`switch破解\bins\hekate_ctcaer_6.0.1.bin` ，点 `Tools` > `Backup eMMC` > `eMMC RAW GPP` 继续备份
    -   重复以上步骤直到备份完成
8.  点 `Close` > `Home` 

##### 备份机器的keys

这个是恢复机器的时候和刚刚备份的NAND一起用的。

1.  点 `Payloads` 选项, 选 Lockpick_RCM.bin
2.  如果 Lockpick_RCM 让你选 SysNAND 或 EmuNAND, 使用音量键选 SysNAND 点电源键确定。 如果没问就直接下一步
3.  Lockpick_RCM 完成了会说keys存在 `/switch/prod.keys` 了
4.  点任何键回到主菜单
5.  用音量键选择 'Power off' 按电源键确认
6.  把tf卡连接电脑
7.  把 `switch` 文件夹里的 `prod.keys` 和根目录上一步创建的 `backup` 文件夹保存好，然后卡里的对应文件就可以删除了。

#### 完成，开始使用自由的自制系统"Atmosphere"吧

**使用自制（虚拟/破解）系统的时候别联网！被老任发现会被ban机！！**

不要在自制系统做联网行为比如：玩各种线上的内容，比如在线对战，交换精灵啥的，浏览eShop什么的。想联机了**重启到正版系统里再联**！！

**插回tf卡**

1.  [[Switch破解#进入RCM：将switch彻底关机后，插上短接器（也就是把pin10接地），先按住音量+不放，再按一下开机键，即可进入RCM，具体如下|进入RCM]]，[[Switch破解#^61f0a8|注入]]`switch破解\bins\hekate_ctcaer_6.0.1.bin`
2.  触屏点 `Launch`
3.  选 `Atmosphere FSS0 EmuMMC` 也就是虚拟系统

好了，现在就进入了可以为所欲为的运行在EmuMMC的自制系统（基于原系统的修改版）里了，这个系统的名字是

[[Switch破解#[Atmosphere](https //github.com/Atmosphere-NX/Atmosphere)|Atmosphere  大气层]]

注意：每次彻底关机后如果想进大气层都需要重新注入`hekate_ctcaer_*.*.*.bin`（因为[[Switch破解#[hekate](https //github.com/CTCaer/hekate)|hekate]]是启动器，用来引导大气层启动）。所以如果机器好久不用断电了，或者什么原因死机了机器重启了，或者自己彻底关机了，需要重新进RCM并注入，不过也不算太麻烦

有的时候会忘记自己在什么系统里边，可以在switch 设置 -> 系统里边看当前的系统版本，如果版本号（这里是9.0.0）的旁边还有个AMS 意味着这个是自制系统，后边的E代表EmuNAND，如果只有9.0.0就是官方原装系统了。

![[launching-cfw-emummc-settings.jpg]]

### 日常使用

自制软件菜单hbmenu一般通过点击 **相册** 来打开，里边有一些常用的软件，就是之前往tf卡里拷贝东西拷贝进去的`.nro`结尾的文件。（想正常打开相册的话，在点击相册的时候按住肩键R即可）

-   [DBI](https://github.com/rashevskyv/dbi/blob/main/README_ENG.md)可以用来安装和管理游戏，也可以使电脑可以通过usb来管理switch内部tf卡文件。
-   [EdiZon SE](https://github.com/tomvita/EdiZon-SE) 内存修改器，可以实时修改游戏数据，就像电脑上的Cheat Engine。
-   [JKSV](https://github.com/J-D-K/JKSV/) 存档管理器，存档导入导出什么的，比如导出宝可梦的存档改数据什么的。替代品有[checkpoint](https://github.com/Flagbrew/Checkpoint)
-   FTPD 可以让电脑通过网络连接到switch从而传输管理switch文件，switch上运行后电脑上用 WinSCP 连接 switch的ip:5000 就可以了，不过都不联网了这个也就别用了，还是usb传吧，用DBI。
-   NX-Shell swithch文件管理器
-   NXThemeInstaller 可以安装自制theme
-   Daybreak 用来离线升级系统的（不是不能联网嘛）
-   Reboot to Payload就是重启到指定payload
-   linkalho

自制软件一般就是一个`.nro`文件，如果自己想安装额外的应用，拷贝文件到tf卡的switch文件夹里就可以了。

通过相册中打开的hbmenu来启动自制应用会有一定的限制，比如可使用的内存更小等，有的时候可能会有问题，**这个时候**(如：使用nxmp播放比较大的视频文件、使用Daybreak更新系统)可以按住肩键R再启动任何已安装的游戏（等到选完用户hdmenu启动成功后再松R）来启动hbmenu，之后再运行自制程序。一般来说直接相册打开没有问题。
#### [Atmosphere](https://github.com/Atmosphere-NX/Atmosphere)

Atmosphere就是一个魔改过的switch系统，行话叫CFW -- customized firmware ，它使得switch的系统拥有了最高的权限，可以为所欲为。
##### 更新
在这下载latest [release](https://github.com/Atmosphere-NX/Atmosphere/releases) 的zip压缩包如`atmosphere-1.5.5-master-4fe9a89ab+hbl-2.4.3+hbmenu-3.5.1.zip`
将swtich[[Switch破解#^a597f5|彻底关机]]后取出tf卡插电脑，把zip压缩包的内容直接解压到tf卡根目录，如果提示覆盖的话直接覆盖（是否需要更新switch固件？可以同时把固件文件也一起拷贝，详情见[[Switch破解#固件升级（系统升级）|系统（固件）升级]]，也可以把[[Switch破解#[hekate](https //github.com/CTCaer/hekate)|hekate]]也一起更新了，也要拷贝文件）。
插入存储卡，[[Switch破解#^04bfff|进RCM]]， [[Switch破解#^61f0a8|注入]] kekate（`hekate_ctcaer_*.*.*.bin`），选择emuMMC即可启动。
#### [hekate](https://github.com/CTCaer/hekate)

hekate是一个多功能的启动器（bootloader），可以在启动的时候选择不同的系统如真实系统、虚拟系统还需许多其他功能。他需要注入软件（如windows:[TegraRcmGUI](https://github.com/eliboa/TegraRcmGUI/releases) Android:[Rekado](https://github.com/MenosGrante/Rekado/releases) switch开着的时候hbmenu中的Reboot to Payload也可以进入）把bin文件注入RCM状态下的switch使用。
##### 更新

记得看看 release notes ，里边会有一些软件的更新信息。

1. switch彻底关机。
2. 下载 [Hekate](https://github.com/CTCaer/Hekate/releases/) ( `hekate_ctcaer_(version).zip`).
3. 直接把压缩包中的 `bootloader` 文件夹拷贝到 SD 卡根目录。如果问是不是覆盖就选是。
4. tf卡插switch，进RCM，注入Hekate。
5. 点右上角的option标签，检查右下角的"Update Reboot 2 Payload" 开关，如果是 ON就不动，不是的话就ON，然后点屏幕下方的 "Save Options" 。
6. 启动emuEMMC

#### 固件升级（系统升级）

一般没什么必要升级固件，但是一些新游戏需要新的固件才可以启动。
在升级系统固件之前请查看一下正在使用的Atmosphere是否支持最新版本的固件（一般来说Atmosphere会跟着官方固件更新一起更新），**先升级Atmosphere**，再把固件升级到Atmosphere支持的最新版本。
或许试试看这个[aio-switch-updater](https://github.com/HamletDuFromage/aio-switch-updater) 它可以下载各种东西，包括固件，CFW，HB软件等。
##### 操作
[Darthsternie's Firmware Archive](https://darthsternie.net/switch-firmwares/) 这个网站可以下载到固件([switch520](https://www.gamer520.com/)也可以)。版本记录：我老switch是日版的机器。
将固件解压到一个单独的文件夹后拷贝到tf卡中即可。
使用应用模式打开hbmenu（不是平时的点击相册启动，而是按住R启动任意游戏，在选完任天堂账号后看到hbmunu后再松开R），启动Daybreak升级。
具体操作见：[upgrade switch](https://rentry.org/UpgradeDowngrade)

#### 联机

面对面连接的时候好像是wifi和蓝牙都可以。
需要联机的游戏版本号一样
需要机器的固件大版本一样，如13.1和13.2的大版本号一样，但是12.1和13.1不一样。（真的吗？）
[switch-lan-play](https://github.com/spacemeowx2/switch-lan-play)
[lan-play](http://www.lan-play.com/)
[Radmin](https://www.radmin-vpn.com/)
zerotier
tailscale
parsec这个是个串流工具。

#### cheat
[Breeze-Beta](https://github.com/tomvita/Breeze-Beta) [Wiki](https://github.com/tomvita/Breeze-Beta/wiki) [releases](https://github.com/tomvita/Breeze-Beta/releases) [用profile打开](https://gbatemp.net/threads/what-happens-to-profile.601072/)
Breeze好像是Edizon作者[tomvita](https://github.com/tomvita)新弄的。

cheat位置，还可以放在edizon或者Breeze的指定位置，这个是大气层指定的位置。
`sd:/atmosphere/contents/<title_id>/cheats/<build_id>.txt`
#### 常用软件

##### [Fizeau](https://github.com/averne/Fizeau)
调整屏幕颜色之类的

##### [Haku33](https://github.com/StarDustCFW/Haku33)
Perform a Hard Reset of the switch, and leave it as if it had just left the box

[ldn_mitm](https://github.com/spacemeowx2/ldn_mitm)
[switch-lan-play](https://github.com/spacemeowx2/switch-lan-play)
这两个大概是相互配合的，用来联机游戏。

[SysDVR](https://github.com/exelix11/SysDVR)
把switch游玩画面串流到电脑！！！
试了试，没弄成，大概还是用采集卡吧...

[nxmp](https://github.com/proconsule/nxmp)
switch的播放器。
添加网络连接的格式
```
win = smb://user:passwd@192.168.1.101/D
Treasure = smb://user:passwd@192.168.1.120/Media/
```
但是这个播放器有个致命的问题，它不能读取外部的subtitles，这个很难受，我看看可不可以把它改改。

[DeepSea](https://github.com/Team-Neptune/DeepSea)
这个是个综合项目，整合了很多HomeBrew软件包，自己也有一些原创的工具。

**[aio-switch-updater](https://github.com/HamletDuFromage/aio-switch-updater)**

**[MissionControl](https://github.com/ndeadly/MissionControl)**、
蓝牙使用别的平台的手柄。
### 问题
更新固件、大气层后启动系统的时候，显示Failed to apply nosigchk，可能会导致部分游戏打不开，但是暂时还没有遇到。
https://gbatemp.net/threads/failed-to-apply-nosigchk.590842/
https://gbatemp.net/threads/how-to-fix-switch-games-not-booting-after-a-fw-cfw-update.563960/
已经解决了，重新拷贝了[Sigpatches](https://gbatemp.net/threads/sigpatches-for-atmosphere-hekate-fss0-fusee-package3.571543/)