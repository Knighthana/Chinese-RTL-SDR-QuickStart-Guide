# RTL-SDR 中文版快速入坑指南

翻译自英文页面：https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/

*英文版本的版权归原作者所有，如果侵犯到原作者权利请联系本人，我会在收到消息之后尽快删除*



---------------------------------------------------------------------

### 免责声明

**请在遵守当地法律法规的前提下操作无线电设备**，请注意许多国家规定在未经许可的频段上发射无线电信号是违法行为，对于不清楚本文在讲什么的读者，请先查询当地关于无线电的规定；
如果你持有所在国家的无线电操作执照，应该清楚哪些操作是合法的，哪些操作是非法的，请遵守所在地区的法律法规。

文章中提到的产品与购买链接翻译自原文，如果要购买其中的产品，请到原网站[RTL-SDR.com](rtl-sdr.com)仔细查看相关说明之后决定是否购买，必要时请查阅[英文原文](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/)，译文没有对任何产品做出过任何保证。

本文仅供参考，译者不对因参照本文而造成的任何损失负责。

------------------------------------------------------------------------



常见名词解释：

【SDR】 软件定义收音机

【RTL-SDR】 基于Realtek生产的一款电视棒芯片及其附属天线设备与常见的家用计算机等共同搭设的软件定义收音机

【加密狗】 翻译自 原文中的 “dongle” 一词，应当是指通过USB连接至计算机的RTL芯片


---------------------------------

## 快速入门指南

这个指南用于帮助任何人在一台Windows计算机上以尽可能便宜和快速的方式入坑RTL-SDR。如果你在安装的过程中遇到任何问题，请点击页面下方的[常见问题指南]链接。对于Linux和OSX用户，我们也提供了一份简洁的指南，请在下方的链接处获取。

请注意，RTL-SDR不是即插即用硬件，你需要一点基本的计算机技术，例如了解如何解压文件，安装软件，移动和复制文件。

### RTL-SDR Blog V3 用户

我们建议以如下的顺序阅读相关资料：

1. 快速入门指南：rtl-sdr.com/QSG - 指引你安装软件，部署你的加密狗；
2. V3功能指南：rtl-sdr.com/V3 - 学习如何使用特别的V3功能，例如直接高频采样模式，以及T型偏置器模式；
3. SDR# 用户指南：rtl-sdr.com/SDRSHARP - 学习SDR#的设置；
4. 偶极子天线指南：rtl-sdr.com/DIPOLE - 学习如何使用你的RTL-SDR Blog多用途偶极子天线（如果你买了还装了的话）

RTL-SDR Blog V3 用户：请注意存在假冒伪劣产品。有奸商在我们的 “RTL-SDR Blog” 品牌下买各种各样的加密狗，蓝色或绿色外壳，或者银色方形盒子每面四颗螺丝（共八颗），或者标榜 “Pro版” 的并非 RTL-SDR 的产品，这些假冒伪劣产品用了低质量的电子元件，还用了廉价的设计，还有可能并不支持所有V3版本的功能，这些假冒伪劣产品不支持新功能，而且我们也不能为它们提供支持，请直接在我们的[商店](www.rtl-sdr.com/store)处购买。

---------------

### 设备指南：

目前，最普遍的 RTL-SDR 加密狗是 R820T或者R820T2，售价大概在20美刀左右（也就是一百五十人民币左右，译者注）。请在[购买RTL-SDR加密狗](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)处获得更多购买相关的信息。

要想流畅运行SDR相关的软件，你至少需要一个双核处理器的计算机，当然以命令行运行的软件或者广播式自动相关监视译码器（我不知道这是什么东西，翻译自原文 “ADS-B decoders” ，译者注）也许能在配置更低一些的计算机上运行。

你需要一根正经的天线来获得比较好的RTL-SDR使用体验，我们的[整合包](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/) 里面包含的偶极子天线就不错，请确保天气好的时候把天线放在室外比较高的地方（打雷的时候就别这么干了，太危险，译者注）这样能获得比较好的接收效果，测试的时候可以找一根长点的鞭形天线凑活用，但是这样做总归不太好。最好用的室外天线是[碟形天线](https://amzn.to/1PnZRQY) ，因为他们在宽频带接受方面表现不错，当然你也可以自己用披萨大小的金属板制作一个便宜版本的宽频带蝶形天线。[平面碟形天线.pdf](http://www.wa5vjb.com/references/PlanarDiskAntennas.pdf)

### SDR#（SDRSharp）安装指南（已在Win7/8/10 32/64位 测试）(XP/Vista 不兼容)

SDR# 是最推荐在Windows上使用的SDR程序，我们因为它在易于安装使用方面和在与RTL-SDR兼容性比较好方面的原因推荐它。

1. 购买一个RTL-SDR解密狗，最便宜且应用广泛的是R820T/R820T2，附上[购买信息](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)

2. 你需要4.6及以上版本的 Microsoft .Net Framework，Win10已经预装了此环境，Win10以下版本尚未安装此环境的，可在此处下载[.Net Framework](https://www.microsoft.com/en-us/download/details.aspx?id=55167) ，Windows XP不支持此环境，XP用户请跳过本段，查看HDSDR或SDR-Console的安装教程，如果你的电脑没有安装 [Microsoft VC++ Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=8328)，你也需要一并安装。

3. 在www.airspy.com页面顶部菜单中点击下载，在打开的页面中寻找并下载 sdrsharp-x86.zip ；

4. 新建一个文件夹，在其中解压sdrsharp-x86.zip，请勿在解压前的压缩包中直接执行任何程序，也不要在任何会在安装过程中自动创建文件夹的地方解压压缩包，例如Program Files中；

5. 在解压好的文件中双击install-rtlsdr.bat文件，这将会启动一个命令提示符，以下载所需的驱动，命令提示符会在下载完成之后自动关闭，如果该下载过程正常，在文件夹中将会看到rtlsdr.dll和zadig.exe，如果下载不成功，请排查问题，包括批处理文件运行失败，网络问题，杀毒软件自动阻止，文件夹被设定为只读，或者这是Program Files中的文件夹；

   如果下载dll文件或者zadig文件失败，请[手动安装驱动](https://rtl-sdr.com/manual-installation-of-sdr)，如果zadig文件小于5MiB，则说明该文件下载失败，请[手动下载zadig](https://zadig.akeo.ie/downloads/)

   ![指向install-rtlsdr.bat的鼠标指针](https://www.rtl-sdr.com/wp-content/uploads/2013/04/install-bat_sdrsharp.png)

6. 插入你的加密狗，**不要安装附带的任何软件（如果它带了的话）**（当然如果你打算把它当电视棒用的话请随便装，译者吐槽），然后确保你等待了一段时间让Windows的即插即用向导**尝试**安装加密狗的驱动（这个过程要么失败，要么会安装一个Windows自带的DVB-T TV驱动），如果你已经安装了比如说制造商附送的安装光盘中的DVB-T驱动的话，先把它们卸载了；

7. 在你解压的文件夹中找到zadig.exe，然后右键点击它，选择“以管理员运行”；

8. 在打开的Zadig页面中，点击“Options->List All Devices”（选项->列出所有的设备，译者注），确保这个选项已经勾上，如果你使用的是Win10，有时候你需要把“Ignore Hubs or Composite Parents”（忽略集线器和复合设备中的父设备，译者注）选项前面的勾去掉；
   ![在Zadig中点击选项后弹出的菜单](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_1.png)

9. 在下拉菜单中选择“Bulk-In, Interface(Interface 0)”，注意在有些计算机中你将会看到名如“RTL2832UHIDIR”或“RTL2832U”的设备取代了Bulk-In, Interface的位置，出现这种情况的时候，选这个也可以。不要选择**USB Receiver (Interface 0)或者 Interface 1或者这之外的任何选项，不然你会把不该覆写的驱动覆写掉！**，反复检查以确保USB ID项显示“0BDA 2838 00”，表明现在是加密狗作为选中的设备；

10. 我们需要安装WinUSB驱动，所以请确保右边被绿色箭头指向的方框中WinUSB也被选中了（这应该是默认选项）。*有人对这一步感到疑惑，这一步的目的是安装WinUSB驱动，所以，箭头左边的方框里是现在安装好的驱动，右边方框里的是下一步中即将要安装的驱动，当你第一次打开Zadig的时候，左边的方框中要么显示“None”，要么就是Windows默认安装的DVB-T驱动（RTL2832UUSB)，显示什么取决于你的系统版本和设置*
    ![点击“替换驱动”前的zadig.exe页面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_3.png)

11. 点击“Replace Driver”（替换驱动，译者注），有些计算机会提示“无法验证的发布者”，（按照微软的规定，在Windows上安装的驱动必须有驱动签名来担保没有恶意行为或者不完善的部分，如果你试图安装的驱动没有签名就会有这个提示，但是驱动签名这种东西一般只有硬件制造商才能拿到，而现在正在进行的是破解硬件的工作，安装的驱动必然没有签名，读者自行决定是否信任这篇教程并自行承担接下来的风险，译者注），但是不用管提示，点击“Install this driver software anyway”（无论如何安装这个驱动），这一步将会安装那些必要的将加密狗作为SDR使用的驱动，注意假如你把加密狗插到了别的USB口，或者想同时使用两个以上的加密狗的时候，你需要重新运行zadig.exe以便再次替换驱动；
    ![Windows的未签名驱动提示框](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_warning.png)

12. 打开SDRSharp.exe并且在“Source”（源）标签中的下拉菜单里选中“RTL-SDR (USB)”，这个“源”标签在上面左侧，（注意初次这么做的时候你可能会看到一个弹出的消息框，说Windows正在保护你的计算机，这是一个错误的报警，点击“更多信息”然后再点击“无论如何继续运行”）；

13. 点击播放按钮（朝右的三角形）。你的RTL-SDR软件应该就可以使用了！如果一切工作都正常，你应该可以调频了。
    ![SDRSharp.exe页面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/rtlsdrsource.png)

14. 重要的是，不要忘记调整射频接收设置，你可以按配置按钮（顶部播放键旁边的齿轮状图标），默认情况下射频接收设置为0，设置为0的情况下可能除了比较强的FM广播之外什么都收不到，调大接收设置直到你收到其他信号，如果想用一个V3收到高频信号，请查看我们的[V3用户手册](https://www.rtl-sdr.com/v3)
    ![RTL-SDR Controller界面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/gain.png)

#### 接下来的步骤

在设置好SDR#这个软件之后，你的RTL-SDR也就设置好了，我们建议你尝试下面的部分：

1. 如果你使用的是rtl-sdr.com的V3加密狗，查看我们的[V3用户手册](https://www.rtl-sdr.com/v3)学习如何使用特殊功能，例如直接高频采样模式，或者T型偏置器模式；
2. 从[SDR# 用户手册](https://www.rtl-sdr.com/sdrsharp-users-guide/)中获取SDR#的每项设置的含义；
3. 查看我们所有的[成果展示文章](https://www.rtl-sdr.com/category/article/)，查看所有RTL-SDR相关的项目和教程；
4. 升级增益天线，为了更好地接收信号，你需要一个在户外固定在房顶的天线，何种天线更好取决于你感兴趣的频率和项目，通常来看，我们认为更好的天线是[碟形天线](https://amzn.to/1K363vp)或者[平面碟形天线](http://www.wa5vjb.com/references/PlanarDiskAntennas.pdf)；
5. 如果你正在用你的RTL-SDR进行直接的高频采样，或者将它作为上变频器，我们建议你使用[使用特别驱动的SDR#](https://www.rtl-sdr.com/new-sdr-rtl-sdr-driver-lnamixervga-gain-settings-decimation/)，这些可以帮助你在较小的失真下放大高频的小带宽信号；
6. 在[我们的商店](https://www.rtl-sdr.com/store)查看更多的射频周边产品，例如滤波器，低噪声放大器和天线。

#### 常见问题

- 在SDR#中打开加密狗时遇到了“No Device Selected”（没有检测到设备）的报错
  确保你运行了install-rtlsdr.bat这个文件，并且它成功向SDR#文件夹下载了rtlsdr.dll。如果它没有下载，检查你的文件夹是否被设定为了“只读”，另外一个常见的原因是你在Zadig中将WinUSB驱动装进了Bulk Interface 1而不是Bulk Interface 0，如果你真的这么做了，那么SDR#将无法识别出你的加密狗，遇到这种情况，需要在控制面板的【设备和打印机】中卸载Bulk Interface 1的驱动；
- 在SDR#中打开加密狗时遇到了“No compatible devices found”（没有找到兼容的设备）的报错
  劣质长USB拓展线有时可能会导致这样的问题，有些USB 3.0的拓展坞也和加密狗不兼容，也会导致这样的报错，有的用户非常幸运地通过在安全模式中安装zadig而修复了这样的问题。最后，还有很小的概率是因为加密狗完全坏掉了才导致这样的问题，如果同一个加密狗在数台计算机上产生了相同的这类错误，那么应该是加密狗坏了，需要换一个加密狗；
- Zadig在我尝试安装驱动的时候挂起了
  有用户提出这是由于Windows Update升级失败并且一直挂在后台运行导致的。另一个解决方案是下载备选的zadig工具，尝试用[这个工具](http://visualgdb.com/UsbDriverTool)安装WinUSB驱动；
- Zadig在驱动安装窗口显示了NONE（也许指的是什么都没有显示？原文说“Zadig shows NONE in the driver install screen”，请读者自行甄别这句话的含义，译者注）
  有用户认为这是一个待解决的问题，但是这很正常，因为这个窗口左边的方框表示现在已经安装的驱动，右边的方框里面是在点击安装按钮之后即将安装的驱动；
- 运行Zadig的时候报错 “This app can't run on your PC”（该应用程序无法在你的计算机上运行），或者提示“The version of this file is not compatible with the version of Windows you're running”。我使用的是64位计算机。
  这是你计算机的某些设置导致的，尽管目前还不清楚是哪些设置导致的，有人发现使用Chrome手动下载也会导致这个问题，但是使用Edge下载就可以正常运行。所以试着用Edge从[Zadig网站](https://zadig.akeo.ie/)，或者使用另一个工具，在这个地方下载该工具：http://visualgdb.com/UsbDriverTool
  （译者注：32位计算机装32位驱动，64位计算机装64位驱动，如果还有问题就看看[Zadig的FAQ](https://github.com/pbatard/libwdi/wiki/FAQ#Zadig)，个人不太相信是因为浏览器导致的下载到其他平台的版本，尽管浏览器UA里面确实会有系统位数的字段，但是正常情况下应该不会报出错误的系统位数）
- 我的加密狗昨天还好好的，今天突然就不能运行了
  这种情况99%的原因是Windows自动更新替换了SDR的驱动，然后装了个DVB-T的驱动，确保Windows的自动驱动升级是[关闭](http://winsupersite.com/windows-10/stop-automatic-driver-updates-windows-10)的，然后用zadig重新安装WinUSB驱动
  （链接中提到的winsupersite网站现在也是关闭的，现在应该是搬到https://www.thurrott.com/了吧，也许这篇文章现在在里面？译者注）
- Windows 10 更新毁了我的加密狗！
  Win10更新有时候会覆写SDR驱动，重新运行zadig，重装相关驱动就可以解决这个问题了
  （Win10自动更新的策略人嫌鬼憎啊，译者吐槽）
- 我的加密狗变得特别热并且停止工作，或者完全不工作。测试USB电流远大于0.3A
  正常情况下工作中的加密狗是会变得特别热，但是仍有一小部分（我们估测大概有0.3%）的RTL8232U芯片出场的时候就是坏的，它们会在USB上搞出大电流，变得特别热，最终会坏掉，有些芯片在显露出这些问题之前得工作几分钟到几个小时，也有一些上电之后立刻就坏了，如果你有USB电流检测设备，你可以查看接口电流是否大于0.3A，如果超过的话说明你的RTL2832U芯片上面有什么毛病，如果你认为你的芯片有质量问题请联系商家退货或者更换
- 报错 “1 compatible device have been found but are all busy” （检测到1个兼容设备，当前没有空闲设备）或者 “libusb Open error -12” （libusb 打开错误：-12）
  首先检查一下是不是有别的程序正在使用你的RTL-SDR，或者USB3.0口是坏的，换到USB2.0口试试，有些用户通过在安全模式安装所有程序的方式成功了。
  确保你在zadig里面没有选“USB Reciever (Interface 0)”；确保你的驱动安装的是Bulk in Interface，或者是别的说明它是RTL2838UHIDIR的东西，或者有RTL前缀的东西
  （如果你有Realtek USB网卡的话，注意RTL前缀也有可能是网卡，别把网卡驱动覆写了，译者注）
  如果你没看到正确的 Bulk in Interface，确保你在选项里面勾选了“列出所有设备”，并且去除了“忽略集线器和复合设备中的父设备”前的对勾，（英文分别是“Options->List All Devices”和“Options->Ignore Hubs or Composite Parents”），然后你应该能看到像是“RTLSDR(composite)”一类的你应该在zadig里选择的实体。特别地，如果你使用Windows10，阅读[这篇论坛文章](https://www.rtl-sdr.com/forum/viewtopic.php?f=7&t=1797)
  另一方面，你应当尝试关掉Windows驱动自动安装，你可以在[此处](https://support.microsoft.com/kb/2500967?wa=wsignin1.0)找到关闭它的指南。如果你的计算机挂起过，那么也有可能发生这样的问题，试着拔掉加密狗然后再插上它。



暂时先翻译到这里，原网页下面还有许多问题和解决方案，更新前如果遇到更多问题先查阅[英文原文](https://support.microsoft.com/kb/2500967?wa=wsignin1.0)