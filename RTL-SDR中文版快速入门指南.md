# RTL-SDR 中文版快速入坑指南

翻译自英文页面：https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/

*英文版本的版权归原作者所有，如果侵犯到原作者权利请联系本人，我会在收到消息之后尽快删除*



---------------------------------------------------------------------

### 免责声明

**请在遵守当地法律法规的前提下操作无线电设备**，请注意许多国家规定在未经许可的频段上发射无线电信号是违法行为，对于不清楚本文在讲什么的读者，请先查询当地关于无线电的规定；
如果你持有所在国家的无线电操作执照，应该清楚哪些操作是合法的，哪些操作是非法的，请遵守所在地区的法律法规。

文章中提到的产品与购买链接翻译自原文，如果要购买其中的产品，请到原网站[RTL-SDR.com](https://rtl-sdr.com)仔细查看相关说明之后决定是否购买，必要时请查阅[英文原文](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/)，译文没有对任何产品做出过任何保证。

本文仅供参考，译者不对因参照本文而造成的任何损失负责。

------------------------------------------------------------------------



常见名词解释：

【SDR】 软件定义收音机

【RTL-SDR】 基于Realtek生产的一款电视棒芯片及其附属天线设备与常见的家用计算机等共同搭设的软件定义收音机

【接收器】 翻译自 原文中的 “dongle” 一词，是指通过USB连接至计算机的RTL芯片构成的无线电信号接收器，因为此芯片本来用作电视接收用途，该设备俗话称为“电视棒”，与别处中文文档中的类似词汇应意指同一设备


--------------------------------

## 快速入门指南

这个指南用于帮助任何人在一台Windows计算机上以尽可能便宜和快速的方式入坑RTL-SDR。如果你在安装的过程中遇到任何问题，请点击页面下方的[常见问题指南]链接。对于Linux和OSX用户，我们也提供了一份简洁的指南，请在下方的链接处获取。

请注意，RTL-SDR不是即插即用硬件，你需要一点基本的计算机技术，例如了解如何解压文件，安装软件，移动和复制文件。

### RTL-SDR Blog V3 用户

我们建议以如下的顺序阅读相关资料：

1. 快速入门指南：[rtl-sdr.com/QSG](https://rtl-sdr.com/QSG) - 指引你安装软件，部署你的接收器；
2. V3功能指南：[rtl-sdr.com/V3](https://rtl-sdr.com/V3) - 学习如何使用特别的V3功能，例如直接高频采样模式，以及T型偏置器模式；
3. SDR# 用户指南：[rtl-sdr.com/SDRSHARP](https://rtl-sdr.com/SDRSHARP) - 学习SDR#的设置；
4. 偶极子天线指南：[rtl-sdr.com/DIPOLE](https://rtl-sdr.com/DIPOLE) - 学习如何使用你的RTL-SDR Blog多用途偶极子天线（如果你买了还装了的话）

RTL-SDR Blog V3 用户：请注意存在假冒伪劣产品。有奸商在我们的 “RTL-SDR Blog” 品牌下卖各种各样的接收器，蓝色或绿色外壳，或者银色方形盒子每面四颗螺丝（共八颗），或者标榜 “Pro版” 的并非 RTL-SDR 的产品，这些假冒伪劣产品用了低质量的电子元件，还用了廉价的设计，还有可能并不支持所有V3版本的功能，这些假冒伪劣产品不支持新功能，而且我们也不能为它们提供支持，请直接在我们的[商店](www.rtl-sdr.com/store)处购买。

---------------

### 设备指南：

目前，最普遍的 RTL-SDR 接收器是 R820T或者R820T2，售价大概在20美刀左右（也就是一百五十人民币左右，译者注）。请在[购买RTL-SDR接收器](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)处获得更多购买相关的信息。

要想流畅运行SDR相关的软件，你至少需要一个双核处理器的计算机，当然以命令行运行的软件或者广播式自动相关监视译码器（我不知道这是什么东西，翻译自原文 “ADS-B decoders” ，译者注）也许能在配置更低一些的计算机上运行。

你需要一根正经的天线来获得比较好的RTL-SDR使用体验，我们的[整合包](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)里面包含的偶极子天线就不错，请确保天气好的时候把天线放在室外比较高的地方（打雷的时候就别这么干了，太危险，译者注）这样能获得比较好的接收效果，测试的时候可以找一根长点的鞭形天线凑活用，但是这样做总归不太好。最好用的室外天线是[碟形天线](https://amzn.to/1PnZRQY) ，因为他们在宽频带接受方面表现不错，当然你也可以自己用披萨大小的金属板制作一个便宜版本的宽频带蝶形天线：[平面碟形天线.pdf](http://www.wa5vjb.com/references/PlanarDiskAntennas.pdf)

### SDR#（SDRSharp）安装指南（已在Win7/8/10 32/64位 测试）(XP/Vista 不兼容)

SDR# 是最推荐在Windows上使用的SDR程序，我们因为它在易于安装使用方面和在与RTL-SDR兼容性比较好方面的原因推荐它。

1. 购买一个RTL-SDR解密狗，最便宜且应用广泛的是R820T/R820T2，附上[购买信息](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)

2. 你需要4.6及以上版本的 Microsoft .Net Framework，Win10已经预装了此环境，Win10以下版本尚未安装此环境的，可在此处下载[.Net Framework](https://www.microsoft.com/en-us/download/details.aspx?id=55167) ，Windows XP不支持此环境，XP用户请跳过本段，查看HDSDR或SDR-Console的安装教程，如果你的电脑没有安装 [Microsoft VC++ Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=8328)，你也需要一并安装。

3. 在 [www.airspy.com](https://www.airspy.com) 页面顶部菜单中点击下载，在打开的页面中寻找并下载 sdrsharp-x86.zip ；

4. 新建一个文件夹，在其中解压sdrsharp-x86.zip，请勿在解压前的压缩包中直接执行任何程序，也不要在任何会在安装过程中自动创建文件夹的地方解压压缩包，例如Program Files中；

5. 在解压好的文件中双击install-rtlsdr.bat文件，这将会启动一个命令提示符，以下载所需的驱动，命令提示符会在下载完成之后自动关闭，如果该下载过程正常，在文件夹中将会看到rtlsdr.dll和zadig.exe，如果下载不成功，请排查问题，包括批处理文件运行失败，网络问题，杀毒软件自动阻止，文件夹被设定为只读，或者这是Program Files中的文件夹；

   如果下载dll文件或者zadig文件失败，请[手动安装驱动](https://rtl-sdr.com/manual-installation-of-sdr)，如果zadig文件小于5MiB，则说明该文件下载失败，请[手动下载zadig](https://zadig.akeo.ie/downloads/)

   ![指向install-rtlsdr.bat的鼠标指针](https://www.rtl-sdr.com/wp-content/uploads/2013/04/install-bat_sdrsharp.png)

6. 插入你的接收器，**不要安装附带的任何软件（如果它带了的话）**（当然如果你打算把它当电视棒用的话请随便装，译者吐槽），然后确保你等待了一段时间让Windows的即插即用向导**尝试**安装接收器的驱动（这个过程要么失败，要么会安装一个Windows自带的DVB-T TV驱动），如果你已经安装了比如说制造商附送的安装光盘中的DVB-T驱动的话，先把它们卸载了；

7. 在你解压的文件夹中找到zadig.exe，然后右键点击它，选择“以管理员运行”；

8. 在打开的Zadig页面中，点击“Options->List All Devices”（选项->列出所有的设备，译者注），确保这个选项已经勾上，如果你使用的是Win10，有时候你需要把“Ignore Hubs or Composite Parents”（忽略集线器和复合设备中的父设备，译者注）选项前面的勾去掉；

   ![在Zadig中点击选项后弹出的菜单](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_1.png)

9. 在下拉菜单中选择“Bulk-In, Interface(Interface 0)”，注意在有些计算机中你将会看到名如“RTL2832UHIDIR”或“RTL2832U”的设备取代了Bulk-In, Interface的位置，出现这种情况的时候，选这个也可以。不要选择**USB Receiver (Interface 0)或者 Interface 1或者这之外的任何选项，不然你会把不该覆写的驱动覆写掉！**，反复检查以确保USB ID项显示“0BDA 2838 00”，表明现在是接收器作为选中的设备；

  （译者在这里再强调一下，仔细看看你是不是选择了正确的驱动，不要在不确认到底选择了什么的情况下乱点下一步，因为乱点的话你可能会把鼠标键盘的驱动搞坏，或者把USB网卡的驱动搞坏，那样你就只能手机发帖求助了，仔细看清楚待选设备是不是“Bulk-In, Interface(Interface 0)”或者RTL2832U一类可以确定是RTL电视棒的东西）

10. 我们需要安装WinUSB驱动，所以请确保右边被绿色箭头指向的方框中WinUSB也被选中了（这应该是默认选项）。

    *有人对这一步感到疑惑，这一步的目的是安装WinUSB驱动，所以，箭头左边的方框里是现在安装好的驱动，右边方框里的是下一步中即将要安装的驱动，当你第一次打开Zadig的时候，左边的方框中要么显示“None”，要么就是Windows默认安装的DVB-T驱动（RTL2832UUSB)，显示什么取决于你的系统版本和设置*

    ![点击“替换驱动”前的zadig.exe页面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_3.png)

11. 点击“Replace Driver”（替换驱动，译者注），有些计算机会提示“无法验证的发布者”，（按照微软的规定，在Windows上安装的驱动必须有驱动签名来担保没有恶意行为或者不完善的部分，如果你试图安装的驱动没有签名就会有这个提示，但是驱动签名这种东西一般只有硬件制造商才能拿到，而现在正在进行的是破解硬件的工作，安装的驱动必然没有签名，读者自行决定是否信任这篇教程并自行承担接下来的风险，译者注），但是不用管提示，点击“Install this driver software anyway”（无论如何安装这个驱动），这一步将会安装那些必要的将接收器作为SDR使用的驱动，注意假如你把接收器插到了别的USB口，或者想同时使用两个以上的接收器的时候，你需要重新运行zadig.exe以便再次替换驱动；

    ![Windows的未签名驱动提示框](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_warning.png)

12. 打开SDRSharp.exe并且在“Source”（源）标签中的下拉菜单里选中“RTL-SDR (USB)”，这个“源”标签在上面左侧，（注意初次这么做的时候你可能会看到一个弹出的消息框，说Windows正在保护你的计算机，这是一个错误的报警，点击“更多信息”然后再点击“无论如何继续运行”）；

13. 点击播放按钮（朝右的三角形）。你的RTL-SDR软件应该就可以使用了！如果一切工作都正常，你应该可以调频了。

    ![SDRSharp.exe页面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/rtlsdrsource.png)

14. 重要的是，不要忘记调整射频接收设置，你可以按配置按钮（顶部播放键旁边的齿轮状图标），默认情况下射频接收设置为0，设置为0的情况下可能除了比较强的FM广播之外什么都收不到，调大接收设置直到你收到其他信号，如果想用一个V3收到高频信号，请查看我们的[V3用户手册](https://www.rtl-sdr.com/v3)

    ![RTL-SDR Controller界面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/gain.png)

#### 接下来的步骤

在设置好SDR#这个软件之后，你的RTL-SDR也就设置好了，我们建议你尝试下面的部分：

1. 如果你使用的是rtl-sdr.com的V3接收器，查看我们的[V3用户手册](https://www.rtl-sdr.com/v3)学习如何使用特殊功能，例如直接高频采样模式，或者T型偏置器模式；
2. 从[SDR# 用户手册](https://www.rtl-sdr.com/sdrsharp-users-guide/)中获取SDR#的每项设置的含义；
3. 查看我们所有的[成果展示文章](https://www.rtl-sdr.com/category/article/)，查看所有RTL-SDR相关的项目和教程；
4. 升级增益天线，为了更好地接收信号，你需要一个在户外固定在房顶的天线，何种天线更好取决于你感兴趣的频率和项目，通常来看，我们认为更好的天线是[碟形天线](https://amzn.to/1K363vp)或者[平面碟形天线](http://www.wa5vjb.com/references/PlanarDiskAntennas.pdf)；
5. 如果你正在用你的RTL-SDR进行直接的高频采样，或者将它作为上变频器，我们建议你使用[使用特别驱动的SDR#](https://www.rtl-sdr.com/new-sdr-rtl-sdr-driver-lnamixervga-gain-settings-decimation/)，这些可以帮助你在较小的失真下放大高频的小带宽信号；
6. 在[我们的商店](https://www.rtl-sdr.com/store)查看更多的射频周边产品，例如滤波器，低噪声放大器和天线。

#### 常见问题

- 在SDR#中打开接收器时遇到了“No Device Selected”（没有检测到设备）的报错
  
  确保你运行了install-rtlsdr.bat这个文件，并且它成功向SDR#文件夹下载了rtlsdr.dll。如果它没有下载，检查你的文件夹是否被设定为了“只读”，另外一个常见的原因是你在Zadig中将WinUSB驱动装进了Bulk Interface 1而不是Bulk Interface 0，如果你真的这么做了，那么SDR#将无法识别出你的接收器，遇到这种情况，需要在控制面板的【设备和打印机】中卸载Bulk Interface 1的驱动；
- 在SDR#中打开接收器时遇到了“No compatible devices found”（没有找到兼容的设备）的报错
  
  劣质长USB拓展线有时可能会导致这样的问题，有些USB 3.0的拓展坞也和接收器不兼容，也会导致这样的报错，有的用户非常幸运地通过在安全模式中安装zadig而修复了这样的问题。最后，还有很小的概率是因为接收器完全坏掉了才导致这样的问题，如果同一个接收器在数台计算机上产生了相同的这类错误，那么应该是接收器坏了，需要换一个接收器；
- Zadig在我尝试安装驱动的时候挂起了
  
  有用户提出这是由于Windows Update升级失败并且一直挂在后台运行导致的。另一个解决方案是下载备选的zadig工具，尝试[用于安装WinUSB驱动的工具](http://visualgdb.com/UsbDriverTool)；
- Zadig在驱动安装窗口显示了NONE（也许指的是什么都没有显示？原文说“Zadig shows NONE in the driver install screen”，请读者自行甄别这句话的含义，译者注）
  
  有用户认为这是一个待解决的问题，但是这很正常，因为这个窗口左边的方框表示现在已经安装的驱动，右边的方框里面是在点击安装按钮之后即将安装的驱动；
- 运行Zadig的时候报错 “This app can't run on your PC”（该应用程序无法在你的计算机上运行），或者提示“The version of this file is not compatible with the version of Windows you're running”。我使用的是64位计算机。
  
  这是你计算机的某些设置导致的，尽管目前还不清楚是哪些设置导致的，有人发现使用Chrome手动下载也会导致这个问题，但是使用Edge下载就可以正常运行。所以试着用Edge从[Zadig网站](https://zadig.akeo.ie/)，或者使用另一个工具，在这个地方下载该工具：http://visualgdb.com/UsbDriverTool
  
  （译者注：32位计算机装32位驱动，64位计算机装64位驱动，如果还有问题就看看[Zadig的FAQ](https://github.com/pbatard/libwdi/wiki/FAQ#Zadig)，个人不太相信是因为浏览器导致的下载到其他平台的版本，尽管浏览器UA里面确实会有系统位数的字段，但是正常情况下应该不会报出错误的系统位数）
- 我的接收器昨天还好好的，今天突然就不能运行了
  
  这种情况99%的原因是Windows自动更新替换了SDR的驱动，然后装了个DVB-T的驱动，确保Windows的自动驱动升级是[关闭](http://winsupersite.com/windows-10/stop-automatic-driver-updates-windows-10)的，然后用zadig重新安装WinUSB驱动
  
  （链接中提到的winsupersite网站现在也是关闭的，现在应该是搬到[thurrott.com](https://www.thurrott.com/) 了吧，也许这篇文章现在在里面？译者注）
- Windows 10 更新毁了我的接收器！
  
  Win10更新有时候会覆写SDR驱动，重新运行zadig，重装相关驱动就可以解决这个问题了
  
  （Win10自动更新的策略人嫌鬼憎啊，译者吐槽）
- 我的接收器变得特别热并且停止工作，或者完全不工作。测试USB电流远大于0.3A
  
  正常情况下工作中的接收器是会变得特别热，但是仍有一小部分（我们估测大概有0.3%）的RTL8232U芯片出场的时候就是坏的，它们会在USB上搞出大电流，变得特别热，最终会坏掉，有些芯片在显露出这些问题之前得工作几分钟到几个小时，也有一些上电之后立刻就坏了，如果你有USB电流检测设备，你可以查看接口电流是否大于0.3A，如果超过的话说明你的RTL2832U芯片上面有什么毛病，如果你认为你的芯片有质量问题请联系商家退货或者更换
- 报错 “1 compatible device have been found but are all busy” （检测到1个兼容设备，当前没有空闲设备）或者 “libusb Open error -12” （libusb 打开错误：-12）
  
  首先检查一下是不是有别的程序正在使用你的RTL-SDR，或者USB3.0口是坏的，换到USB2.0口试试，有些用户通过在安全模式安装所有程序的方式成功了。
  
  确保你在zadig里面没有选“USB Reciever (Interface 0)”；确保你的驱动安装的是Bulk in Interface，或者是别的说明它是RTL2838UHIDIR的东西，或者有RTL前缀的东西
  （如果你有Realtek USB网卡的话，注意RTL前缀也有可能是网卡，别把网卡驱动覆写了，译者注）
  如果你没看到正确的 Bulk in Interface，确保你在选项里面勾选了“列出所有设备”，并且去除了“忽略集线器和复合设备中的父设备”前的对勾，（英文分别是“Options->List All Devices”和“Options->Ignore Hubs or Composite Parents”），然后你应该能看到像是“RTLSDR(composite)”一类的你应该在zadig里选择的实体。特别地，如果你使用Windows10，阅读[这篇论坛文章](https://www.rtl-sdr.com/forum/viewtopic.php?f=7&t=1797)
  
  另一方面，你应当尝试关掉Windows驱动自动安装，你可以在[此处](https://support.microsoft.com/kb/2500967?wa=wsignin1.0)找到关闭它的指南。如果你的计算机挂起过，那么也有可能发生这样的问题，试着拔掉接收器然后再插上它。

- SDR# 报错 “Unable to load DLL 'rtlsdr': the specified module could not be found. (Exception from HRESULT: 0x8007007E)” （无法加载dll'rtlsdr'：指定的模块无法找到。（错误码：0x8007007E），译者注）

  通常来说安装[VC++运行环境](https://www.microsoft.com/en-us/download/details.aspx?id=8328)将会解决这些问题，一般的计算都已安装了该运行时，但是如果你的电脑刚刚安装了操作系统，那么也许得自己来安装；
  
- SDR# 报错 “The application has failed to start because its side-by-side configuration is incorrect” （由于side-by-side配置有误，应用程序未能正常启动）

  如果你正在用64位系统，但是尝试使用32位软件就会出现这个问题（原文 If you are using the x64 version try the x86 version 怎么看都是有两个谓语的病句，如果认为指的是 if you are using the x64 version and you try the x86 version 就可以这么翻译，但是按常理x64系统会兼容x86软件，可以确定的是，这里表达的是系统位数和软件位数不符就会导致这样的报错，译者注），这也许说明你的计算机上的.Net安装有问题，尝试修复或者重装.Net也许会解决这个问题；


- 频谱中间有一个常驻的峰消除不掉

  这很正常，是大多数RTL-SDR接收器设计上的一个副作用导致的，这个东西可以被SDR#的算法移除掉，只需要点击 “Correct IQ” 就可以了。如果你用的是E4000型的接收器，那么就点“偏移量调整”。

  （Correct IQ 应指“正交校正”，“I/Q” 在射频中一般指 In-Phase 与 Quadrature ，In-Phase 是同相信号或信号的实部， Quadrature 是正交信号，译者注）

- 我看不见“Bulk-In, Interface (Interface 0)”
  
  确保“ Options->List All Devices ”已被勾选，有时候你还得取消掉“ Ignore Hubs or Composite Parents ”的勾选，有些人也提到这里会显示别的RTL开头的名称，像是“RTL2832U”或者“RTL2832UHIDR”一类的，选这些选项也可以，极少数情况下你的接收器的USB功能坏掉了，你需要换一个

  （再次提示，如果你正好用了Realtek家的USB无线网卡，务必确认你没有选中覆写RTL开头的USB无线网卡的驱动，译者再注）

- 插在USB3.0口上不工作

  有些劣质USB3.0控制器对USB2.0设备兼容性不好，通常来说，接收器应该能够在USB3.0口上正常工作，遇到这种情况请更换至USB2.0控制器的插口

- 运行install-rtlsdr.bat的时候提示“The system cannot find the file specified”，也没有下载sdrsharp目录

  这很可能是你没有解压文件导致的，请务必确保你完全解压了所有的文件再运行。

  （如果没有特殊需求，请将压缩文件文件解压之后再用，不要在解压软件窗口里面直接运行压缩包中的程序，这是一个基本且正常的计算机使用习惯，译者注）

- 当我点击了 install-rtlsdr.bat 之后屏幕上闪过一个CMD窗口并且立刻消失了，什么都没有安装

  这应该是一个bug或者是设置出了问题，有些版本的Windows有bug，不能运行批处理文件，解决方案是手动安装，请查看我们提供的这篇说明，了解[如何手动安装sdr](https://www.rtl-sdr.com/manual-installation-of-sdr/)，有些杀毒软件也会阻止这个批处理文件的运行，请关掉杀毒软件或者装一个聪明一点的，或者手动安装。

  （如果遇到cmd窗口一闪而过的情况，至少得搞明白窗口上面本来要提示什么，如果知道了错误提示，问题一般就容易解决了；假如遇到了cmd窗口一闪而过的情况，就应该打开一个空白的cmd窗口，然后在这个窗口中通过敲命令或者拖动bat文件进去的方式来运行 install-rtlsdr.bat ，观察它的运行结果，这样至少可以知道批处理文件报了什么错误，然后对症下药。 ---译者吐槽）

- SDR# 界面看到的信号很小，或者接收不到信号

  先确认你已经滑动过“RF Gain”（射频信号增益）滑块让它增大了，这个滑块可以在“Configure”（配置）按钮中找到；其次，在某些信号不好的地方，室内摆放的增益天线的效率很低，因此尽可能把天线放到露天的高的地方，有时候可能是增益天线到天线插座的连接不牢固导致信号传输极差，在极少数情况中，当你发现别的接收器能正常接收信号但你的接收器收不到信号，那就说明接收器坏了，换一个吧

- SDR# 报错 “ Application failed to initialize properly (0xc0000135).  Click OK to terminate. ”

  这是因为你没有正确安装[ Microsoft .Net Framework ](https://www.microsoft.com/en-us/download/details.aspx?id=48130)

- SDR# 报错 “ Object reference not set to an instance of an object ”

  这说明你没有正确地安装音频设备驱动；或者你禁止了声音输出设备，在Windows声音播放属性里面打开它

- 接收器时不时地断开连接

  首先排查是不是延长线或者集线器的问题：把接收器直接插在计算机的USB口上；如果它还是这样，那么是接收器的问题，换一个

- SDR# 在我的显示器休眠后卡住了

  这要么是SDR#的BUG，要么是Windows的BUG，最简单的解决方案是关掉显示器自动休眠；

- 接收器上面的灯不亮 / 接收器上面的LED不亮

  接收器坏了，换一个；

- 运行SDR#的时候我的计算机CPU负荷有100% / 运行SDR#的时候我的计算机变得很卡

  想要运行SDR#这种有图形用户界面的SDR软件，你至少需要一个双核处理器的计算机，如果你的CPU勉强达到这个水准以上但是还是感到负荷很重，那么就试着把采样频率降低到 1MSPS ，或者更低，减少快速傅里叶变换显示的分辨率（或者直接关掉它），关掉正交校正，减少滤波器等级

  （如果读者的处理器是Intel带“酷睿”二字的，或者是AMD后期的那些农机，那么处理器最少也是双核的，不应该遇到卡顿的问题，如果不是计算机上有病毒或者没必要安装的软件太多导致卡顿的话，去排查一下是不是采样频率过高、FFT显示的分辨率过高或者滤波等级太高导致的问题，译者注1）
  
  （如果读者的计算机确实像译者曾经用过的计算机一样不太行，比如处理器是早期奔腾，早期赛扬，或者那些AMD的早期作品，而且暂时也没有经济能力换新机的话，去看看磁盘还有没有地方，可以的话放弃Win7（XP和Vista用户应该没法运行SDR#），腾点地方装个没有图形界面的Linux，比如安装Ubuntu和Fedora的时候选择不安装图形界面，或者用那些默认不带有图形用户界面的发行版，比如Debian或者ArchLinux，然后去找一下Linux版本SDR的教程；至于如何给磁盘腾地方，如何安装Linux，还有Linux怎么用这里篇幅太小不够说，用此处给出的关键词和搜索引擎读者应当能自己完成剩下的部分，译者注2）

  （但是SDR的性能消耗大头应该是数字信号处理部分，图形不图形界面的真的对性能有影响吗？译者吐槽）

- Zadig把我的键盘/鼠标/其他USB设备搞坏了

  这肯定是因为你在zadig页面的下拉菜单里面选择了错误的设备还点下了安装键，所以不要在zadig里面乱点了，确保你在zadig里选择了正确的RTL-SDR设备 (Bulk-In Interface, Interface 0)。想要给其他设备恢复驱动你需要在Windows的设备管理器里面选择那些不能工作的设备，然后点击更新它们的驱动来修复它。

  （关于这个，你得看看这个[救命！Zadig把错误的驱动换掉了，我该怎么办？](https://github.com/pbatard/libwdi/wiki/FAQ#help-zadig-replaced-the-driver-for-the-wrong-device-how-do-i-restore-it)，译者注）

- 我运行诊断工具rtl_test的时候显示我的R820T2是个R820T

  R820T2和R820T是几乎完全相同的电子元件，R820T2用了更高质量的半导体，所以偶然情况下R820T2的最大中频滤波器带宽和R820T有一些微小的不同，一般来说R820T2更好的硅材料让它有更好的表现，产品间的出厂差异也很小；但是因为它们的电路部分没有任何差异，所以R820T2在计算机看来就是R820T，要想确认它到底是不是R820T2，你需要检查芯片上的标识。

- 我的杀毒软件说SDR#是个病毒

  这绝对是错的！SDR#经常更新，有时候供下载的压缩包每天都会更新，有些破烂杀毒软件会假定任何不经常被人下载的软件文件都是病毒，SDR#更新得过于频繁，可能下载新版本的人不多，因此需要慢慢和杀毒软件公司建立信任。

  （如果是Chrome的话，它几乎会对每个下载的软件都报“这个软件可能会危害你的计算机”，因此如果是Chrome报的可以暂时先别管，如果确实是杀毒软件报的，首先检查一下你下载的途径是不是前面提供的[下载途径](https://www.airspy.com/)，如果不是，那么删掉你下载的文件，在这个airspy网址里面重下，如果你确实是在这里下载的，而且杀毒软件还为此报毒，除非当天他们的服务器遭到攻击并且提供下载的文件被黑客替换了，否则这个软件没理由有病毒，也许是时候换一个杀毒软件了，译者注）

- SDR# 界面中的模式选择按钮有毛病，我按不了

  这可能是由于Windows的“自定义缩放级别”设置导致的，[将这个选项设置为默认值](http://www.tenforums.com/tutorials/5990-dpi-scaling-level-displays-change-windows-10-a.html)也许能够帮助你解决这个问题

  （或者直接点击打开[显示设置](ms-settings:display?activationSource=SMC-IA-4027860)，或者从[微软的网页](https://support.microsoft.com/zh-cn/windows/%E6%9F%A5%E7%9C%8B-windows-10-%E4%B8%AD%E7%9A%84%E6%98%BE%E7%A4%BA%E8%AE%BE%E7%BD%AE-37f0e05e-98a9-474c-317a-e85422daa8bb)打开它，译者注）

- 关闭SDR#的时候，报错“An error occurred loading a configuration file: Access to the path 'C:\Program Files\SDR\s14i12qq.tmp' is denied. (C:\Program Files\SDR\SDRSharp.exe.Config) ---> System.UnauthorizedAccessException: Access to the path 'C:\Program Files\SDR\s14i12qq.tmp' is denied.”

  这通常是因为你将SDR#安装进了一个只读的目录引起的，Windows的“C:\Program Files”目录一般是只读的，为了解决这个问题，你可以把SDR#的文件放在一个不是Program Files的目录里面，比如说“C:\SDR”

  （或者你也可以放进 `C:\users\%username%\appdata\local\RTL-SDR` 里面，如果不想让磁盘的根目录太乱的话，译者注）

- 我的接收器还带了个遥控器，这是用来干嘛的？

  有些卖家会卖给你接收器的时候会附赠一个遥控器（毕竟这东西叫电视棒嘛，译者吐槽），这个遥控器是用来换台的，它只在接收器用作原来的用途的时候——作为DVB-T 高清电视电视棒的时候起作用，当接收器作为软件定义收音机的一部分的时候，这个遥控器是没用的。

  （接收器能收到遥控器发出的红外线，也许你可以考虑把遥控器拿来做点别的用途？译者吐槽）

- 我想用接收器看DVB-T电视，怎么办？

  （这条我懒得翻了，中国没有DVB-T电视，别试了；如果你人在国外，或者人是其他简体中文区的，可以到[原网站](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide)中的“I want to watch DVB-T with my dongle, how do I do it?”条目查看解决方案，简单来说就是卸载掉现在的驱动，重装一个DVB-T驱动——卖家附赠的或者默认的Windows DVB-T驱动。DVB-T驱动不能和SDR的驱动共存，译者注）

- 我有一个RTL-SDR V3 ，但是高频部分不能工作

  要想获得高频接收，你必须打开直接采样模式，请查看[V3用户手册](https://www.rtl-sdr.com/rtl-sdr-blog-v-3-dongles-user-guide/)获取打开直接采样模式的方法；

- 我在rtl-fm，rtl-test，T型偏置器软件一类的CMD程序页面看到了报错“rtlsdr_demod_write_reg failed with -9”

  这一般来说是你的计算机上的USB口无法正常工作导致的，试试别的USB口。以及确保你的接收器在其他计算机上确实能够正常工作，要是坏了就换一个。

- 我有一块现代的Ryzen（锐龙）主板，上面只有USB3.0/3.1插口，没有软件能检测到接收器，我也没法运行我的RTL-SDR

  这要么是libUSB的BUG，要么是新主板不兼容导致的，我们已经发布了[“rtl-sdr-blog”版的驱动](https://github.com/rtlsdrblog/rtl-sdr-blog/releases)，在SDR#目录里面用我们提供的librtlsdr.dll文件换掉原来的rtlsdr.dll，然后把librtlsdr.dll重命名为rtlsdr.dll，有的人也用[这里发布的已修复的DLL文件](https://www.rtl-sdr.com/forum/viewtopic.php?f=4&t=4411)解决了问题。

  要是你还有问题，欢迎来[我们的论坛](https://www.rtl-sdr.com/forum)的Troubleshooting版块讨论

#### 怎么设置增益

增益可以通过在SDR#中点击那个长得像齿轮一样的配置按钮来设定，调整信号增益以便让你接收到尽可能强的增益，同时保持本底噪声尽可能地低。从低增益开始，慢慢地调大增益滑块，看着频谱，让信号强度增大，然后在本底噪声快要开始升起的时候停止调大增益。

本底噪声指的是频谱中没有信号的部分。

#### SDRSharp的插件

你可以在这里找到[SDRSharp官方插件列表](http://www.sdrsharp.com/#plugins)，

同样你也可以在这里获得由我们提供的[SDRSharp非官方插件列表](http://www.atouk.com/SDRSharpQuickStart.html)

#### SDRSharp 用户手册

你可以在这里找到一份[讲述如何使用SDR#以及SDR#各个选项有什么功能的手册](http://www.atouk.com/SDRSharpQuickStart.html)，这里还有一份非常不错的[有插图的SDR#手册](http://tylerwatt12.com/tips-for-using-sdr/)


### HDSDR设置指南 （已在Windows XP以及以上版本中测试过）

1. 购买一个RTL-SDR接收器。最便宜也是最棒的是R820T/R820T2电视棒。你可以在这里找到[购买信息](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)

2. 插入接收器，不要安装任何附带的驱动，如果你之前已经安装了它附带的驱动，先把这些驱动卸载了

3. 在这里[下载Zadig](http://zadig.akeo.ie/)

（下载的时候别忘了看看[Zadig使用常见问题指南](https://github.com/pbatard/libwdi/wiki/FAQ#Zadig)，**一定要打开先看一下！** ——译者注）

4. 打开zadig，确保 Options->List All Devices 选项已经打勾；

5. 在下拉菜单中选择“Bulk-In, Interface (Interface 0)”，确保在下方的“Driver”一栏中显示选中了WinUSB，在有些计算机上可能看到的不是bulk in interface，而是RTL2832UHIDIR或者RTL2832U，这也是可以的，但是，**!!!请勿选择USB Receiver (Interface 0)，绝对不要!!!**

  ![zadig界面](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_3.png)

6. 点击“Install Driver”（安装驱动）。你可能会收到一条有关发布者未经过验证的提示，如果你信任这个软件的话就点击无论如何安装这个驱动，这将安装那些足以让你的接收器转变为软件定义收音机的驱动，注意要是你把接收器挪到别的USB口，或者是想要几个接收器一起用的话，就得再运行zadig.exe一次。

  ![zadig警告](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_warning.png)

7. 访问[HDSDR高清软件定义收音机的网站](http://hdsdr.de/)，在底部的下载按钮处下载HDSDR软件；

8. 运行你下载好的安装程序，安装HDSDR软件；

9. 在[HDSDR硬件相关](http://hdsdr.de/hardware.html)页面上方的“RTLSDR (DVB-T/DAB with RTL2832) USB”表项中下载ExtIO_RTL2832U.dll文件，或者直接下载这个[动态链接库文件](http://hdsdr.de/download/ExtIO/ExtIO_RTL2832.dll)

10. 将ExtIO_RTL2832U.dll复制到HDSDR的安装目录（如果你没更改过安装设置，默认的目录应该是 C:\Program Files (x86)\HDSDR （64位Windows）或者 C:\Program Files\HDSDR （32位Windows））

11. 打开HDSDR软件，如果你上一步复制文件的步骤没有出错，那么应该会没有什么提示地顺利打开；但假如弹出一个窗口要求你选择一个dll文件，那么也是正常的，只需要在窗口中选中你在上一步中刚刚复制过来的ExtIO_RTL2832U.dll文件，然后点击“打开”按钮应该就没问题了

  ![HDSDR弹出选择额外硬件的窗口](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image017-1024x554.jpg)

12. 点击底部左下角的Soundcard按钮（或者按下F5键）选择你的输出声卡。最重要的选项是“RX Output (to Speaker)”，将它设置为你想要设置的送话器，或者软件管道；
  
  ![声卡设置](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image019.jpg)

13. 点击Bandwidth按钮（或者按下F6键）打开带宽设置，如果想要获得通常的NFM信号（根据[Sigidwiki对NFM的解释](https://www.sigidwiki.com/wiki/NFM_Voice)这应当是指对讲机一类的信号，译者注），将采样率设置为48000Hz，如果想要获得宽带调频信号，例如FM广播信号，将采样率设置为192000Hz。

  ![采样频率](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image021.jpg)

14. 按下Start按钮（或者按下F2键），这样收音机就开始工作了；

15. 如果想要设置RTL-SDR的采样频率、增益、频率校正，点击ExtIO按钮；

  ![ExtIO设置窗口](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image023.jpg)

16. 调整本地振荡器(Local Oscillator)的频率到你感兴趣的频道附近的频率，然后你可以通过点击频谱或者使用台号来调到你想听的频道。

  ![调台按钮](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image024-300x67.jpg)

17. 你可以通过"Zoom"字样左侧的滑条来放大或者缩小频谱；

  ![Zoom滑条](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image025-1024x62.jpg)

18. 你可以通过模式选择按钮来选择所需要的模式；

  ![模式按钮](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image026.jpg)

19. 按下FM模式的按钮以后，调频带宽就可以通过FM-BW滑条手动调整了；

  ![调频带宽滑条](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image027.jpg)

20. 如果想听一个典型的宽频FM广播频道，你得把声音采样频率设置为192000Hz。

  - 首先你需要点击带宽(Bandwidth)按钮（或者按下F6键），打开带宽设置，这样你就可以调整输出采样率了。

  - 将输出采样率调整为192000Hz，就能收听FM广播了。


### Cubic SDR 指南（已在Windows XP及以上版本的系统经过测试）

1. 买一个RTL-SDR接收器。最便宜也是最好的选择是R820T/R820T2接收器，此处提供了[购买信息](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)

2. 插入接收器，不要安装它自带的任何软件，确保“即插即用程序”停止尝试为它自动安装驱动，如果你已经安装了任何它携带的驱动，先卸载它们

3. 前往[Zadig网站](https://zadig.akeo.ie/)下载Zadig

4. 打开Zadig，前往选项->列出所有设备，确保所有选项已被选上 

5. 在下拉菜单中选择“Bulk-In, Interface(Interface 0)”。在有些个人计算机上，你可能会看到诸如“RTL2832UHIDIR”或者“RTL2832U”而不是前述的选项，那就选择这样的选项。进行下一步前先反复确认USB ID已经显示为“0BDA 2838 00”，这就说明接收器已经被选中了。

**警告** 不要选择任何其它的选项，不要对其他选项做出操作，不然的话你可能会覆写掉其他设备的驱动。不要在Zadig上漫无目的地点击，否则鼠标、键盘或者音频播放器之类的USB设备会因此而无法正常工作。

6. 选择安装驱动。也许你会看到一条有关无法验证的发布者的提示信息，选择无论如何安装。这将会安装软件定义收音机所必要的驱动。请注意，假如你将接收器移动到了另一个USB口，或者想要同时使用几个接收器的话，就得重新运行Zadig。

  ![zadig_warning.png](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_warning.png)

7. 前往[cubicsdr.com](https://cubicsdr.com/)，进入下载页面。找到软件的最新版本。根据你的Windows操作系统的情况选择合适的下载对象。

8. 运行CubicSDR的安装向导。

9. 向计算机上插入接收器，然后运行安装好的CubicSDR软件。

10. 你将会看到一个SDR设备的目录，在其中选择你的RTL-SDR然后点击“使用选中的选项”("Use Selected", English Version, 注)按钮。

11. CubicSDR将会自动开始工作。

12. 在频谱瀑布上随意点击并收听。

###  其他能够与RTL-SDR兼容的Windows上SDR软件

你可以在[软件向导](https://www.rtl-sdr.com/big-list-rtl-sdr-supported-software/)处找到其他兼容RTL-SDR的软件

## 在Linux上开始你的SDR

对于Linux用户我们建议你首先看[Ranous的快速入门指南文档](https://ranous.files.wordpress.com/2018/02/rtl-sdr4linux_quickstartv2-18.pdf)(PDF文档)。

对于Debian系Linux用户，最简单的方式是通过`apt-get`安装RTL-SDR。我们建议使用最现代化的Linux操作系统以便找到合适的驱动。

（译者：什么叫 the most modern version of Linux OS 啊， Latest么？ 以及有没有驱动还是得看发行版软件仓库的情况）

你可以通过如下命令在Debian系Linux上安装RTL-SDR：

`sudo apt-get update`

`sudo apt-get install rtl-sdr`

手动安装RTL-SDR驱动的方法见[Rtl-sdr - rtl-sdr - Open Source Mobile Communications](https://osmocom.org/projects/rtl-sdr/wiki/Rtl-sdr)。

我们在下面摘录了指令的部分：

`sudo apt-get install libusb-1.0-0-dev git cmake`

`git clone git://git.osmocom.org/rtl-sdr.git`

`cd rtl-sdr/`

`mkdir build`

`cd build`

`cmake ../ -DINSTALL_UDEV_RULES=ON`

`make`

`sudo make install`

`sudo cp ../rtl-sdr.rules /etc/udev/rules.d/`

`sudo ldconfig`

安装这些库之后，你应当卸除一般会被Linux默认使用的DVB-T驱动。你可以用指令`sudo rmmod dvb_usb_rtl28xxu`来暂时地卸除这些驱动。该指令的效果会在你重新插入接收器，或者重启计算机之后失效，届时DVB-T驱动将会重新加载。

如果你想永久禁用DVB-T驱动，可以在`/etc/modprobe.d`目录下编辑名为`rtlsdr.conf`的文本文档（如果不存在就创建该文档），在其中添加一行`blacklist dvb_usb_rtl28xxu`，以便屏蔽DVB-T驱动。

你可以运行如下指令，以便使计算机自动执行能实现上述效果的类似操作：

`echo 'blacklist dvb_usb_rtl28xxu' | sudo tee – append /etc/modprobe.d/blacklist-dvb_usb_rtl28xxu.conf`

现在你可以重启你的计算机（原文为Device意指设备，根据语义应为计算机）了。待计算机进入待命状态之后，插入接收器并在终端执行`rtl_test`，它就应该可以开始运行了。

某些设备例如Orange Pi zero的当前主流发行版操作系统（原文"current mainline OSes"，并没有说具体哪个版本，也没有提时效性）中也许存在某些瑕疵，因此在这些操作系统中，你可能会需要用`blacklist dvb_usb_rtl2832u`语句代替上述`blacklist dvb_usb_rtl28xxu`语句。

如果你是通过`apt-get`自动安装驱动和软件的，你也会需要按上述操作手动编辑或创建`/etc/modprobe.d/rtl-sdr-blacklist.conf`屏蔽DVB-T驱动。

在安装了二进制资源库并且屏蔽了DVB-T驱动之后，我们建议你从"GQRX"开始，"GQRX"是一个在操作方面类似"SDR#"的SDR软件。你可以通过自己使用的发行版操作系统包管理器从软件仓库下载安装，或者从[Download Gqrx SDR – Gqrx SDR](https://gqrx.dk/download)下载。

我们也推荐使用跨平台的CubicSDR，你可以通过[CubicSDR | Cross-Platform and Open-Source Software Defined Radio Application](https://cubicsdr.com/)下载。

如果你想使用GNU Radio我们推荐你使用Marcus Leech的脚本，你可以通过这条指令执行这个脚本。该脚本也会同时帮助你安装RTL-SDR的驱动。

`wget http://www.sbrac.org/files/build-gnuradio && chmod a+x ./build-gnuradio && ./build-gnuradio`

注意，如果你在虚拟机中运行Linux，VirtualBox糟糕的USB传输速度表现让它不是一个好的选择，Vmware Player虚拟机的USB传输速度比较令人满意因此可以获得不错的SDR表现，但这需要你将默认虚拟机硬件设置中的使用USB1.1协议更改为使用USB2.0协议。

上面提到的Kenn Ranous还写过另外一本不错的教程[rtl-sdr4linux_quickstartv10-16](https://ranous.files.wordpress.com/2016/03/rtl-sdr4linux_quickstartv10-16.pdf)（pdf）。

## 在OSX上开始使用RTL-SDR

由于OSX上的SDR软件有非常严重的缺陷，我们建议在其他平台例如Linux或者Windows上搭建和使用SDR。

然而[GQRX，一个SDR软件](https://gqrx.dk/download)在OSX上表现良好。

[跨平台的CubicSDR](https://cubicsdr.com/)也是一个在OSX上使用SDR的选择。

（译者：所以有严重缺陷的是哪个？brew install来的吗？）

----------------------------------------------------------------

### （已被原网站删除，因此本部分残缺，可以跳过）SDR-RAIDO V2 搭建指南（已在Windows XP及以上版本的系统经过测试）

为了给RTL-SDR系统安装SDR-RADIO需要按照以下指南操作：

1. 买一个RTL-SDR接收器。最便宜也是最好的选择是R820T/R820T2接收器，此处提供了[购买信息](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/)

2. 插入接收器，不要安装它自带的任何软件，确保“即插即用程序”停止尝试为它自动安装驱动，如果你已经安装了任何它携带的驱动，先卸载它们

3. 前往[Zadig网站](https://zadig.akeo.ie/)下载Zadig

4. 打开Zadig，前往选项->列出所有设备，确保所有选项已被选上

5. 在下拉菜单中选择“Bulk-In, Interface(Interface 0)”，确保旁边写着“Driver”的方框中选中了“WinUSB”。（注意在某些PC上你可能看到类似RTL2832UHDIR或者RTL2832U而不是Bulk in Interface，这个选项也是可以的）。但无论如何，都千万不要选择“USB Receiver (Interface 0)”

  ![zadig_3.png](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_3.png)

6. 选择安装驱动。也许你会看到一条有关无法验证的发布者的提示信息，选择无论如何安装。这将会安装软件定义收音机所必要的驱动。请注意，假如你将接收器移动到了另一个USB口，或者想要同时使用几个接收器的话，就得重新运行Zadig。

  ![zadig_warning.png](https://www.rtl-sdr.com/wp-content/uploads/2013/04/zadig_warning.png)

7. 从网站获取SDR-RADIO installer：[Downlaod SDR-Radio](http://v2.sdr-radio.com/Software/Download1)

    (译注：2021年4月29日 05:59:07测试，该地址内容不可获取，服务器[http://v2.sdr-radio.com/](http://v2.sdr-radio.com/)似乎已经无法正常工作)

    (译注：根据某全球搜索引擎提供的结果，类似的软件现在可能是在[sdr-radio.com](https://www.sdr-radio.com/old-kits)处提供，但是对此链接不作任何保证，请自行鉴别自己负责，或者自行寻找软件源)

8. 使用安装程序安装SDR-RADIO

9. 下载[RTL-SDR支持库](https://m3ghe.blogspot.com/p/adding-support-for-rtl-sdr-usb-dongles.html)，或者从[镜像](https://mega.nz/#!X8p3wbZa!rnpXTq2FBJ6HfB3f3QBhxf10K2no3xNigRNK5waAwsM)处下载

10. 打开下载的压缩文件，对于 AMD64 / x86_64 计算机，

   如果安装了64位RTL-SDR软件，在`C:\Program Files\SDR-RADIO-PRO.com`处解压`x64`文件夹中的`SDRSourceRTL2832U.dll` `rtlsdr.dll` `libusb-1.0.dll`文件，
   
   如果安装了32位RTL-SDR软件，在`C:\Program Files (x86)\SDR-RADIO-PRO.com`处解压`x32`文件夹中的`SDRSourceRTL2832U.dll` `rtlsdr.dll` `libusb-1.0.dll`文件，
    
 对于32位 x86 计算机，请解压`x32`文件夹中的`SDRSourceRTL2832U.dll` `rtlsdr.dll` `libusb-1.0.dll`文件到`C:\Program Files\SDR-RADIO-PRO.com`

 (这里没有按照原文翻译，因为我认为原文的操作是错的)

 > 原文

 > Extract the SDRSourceRTL2832U.dll, rtlsdr.dll and libusb-1.0.dll files from the x64 folder into the C:\Program Files\SDR-RADIO-PRO.com folder. Or if you have a 32-bit PC extract the files from the x32 folder into C:\Program Files (x86)\SDR-RADIO-PRO.com folder.

11. 打开SDR-RADIO。之后你会首先看到一个选择收音机的窗口，以及一条“List is empty - add radio definition now?”(列表为空，是否现在添加收音机？)选Yes，如果没有出现这个提示，点击“+ Definitions”按钮。

12. 在新出现的窗口打开“Search”(搜索)下拉菜单，选择RTL SDR(USB)。操作完成之后应该会看到RTL-SDR被添加到Radio Definitons列表中，点击OK保存退出

  ![Radio Definitions Search List](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image030.jpg)

  ![Radio Definitions List](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image031.jpg)

13. 在RTL-SDR上点击，点一次选中它，在下面选择你想要的采样率，然后点击“开始”

  ![Select Radio](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image032.jpg)

14. 点击Span按钮，将跨度调整到你上一步里设置的采样率带宽，这将会让你看到整个频谱。

  ![Span and Spectrum](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image033.jpg)

15. 如果需要调整接收模式的话，使用在frequency标签下面左侧的菜单。在这里你也可以调整信号带宽，典型的NFM(窄带FM)信号应该在12kHz宽左右，而典型的FM广播信号应该在192kHz宽左右。

  ![Frequency Explorer](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image034.jpg)

16. 如果需要调整频率的话，使用右边的VFO tuning窗口，如果你没看到的话，也许需要点击VFO tuning标签来让它显示，或者也许是你的窗口过小的原因，你可能需要扩展窗口让它显示出来。你也可以立刻点击滑动条来立刻调整到你想要的频率。

  ![VFO tuning Box](https://www.rtl-sdr.com/wp-content/uploads/2013/04/image035.jpg)

17. 请确保已用Home标签下方区域顶部的射频增益按钮调整过射频增益。默认情况下它会被设置为自动调整。

  ![RF Gain Button](https://www.rtl-sdr.com/wp-content/uploads/2013/04/sdrconsolegain.png)


18. 

--------------------------------------------------------

## 更多

![The Hobbyist's Guide to the RTL-SDR: Really Cheap Software Defined Radio](https://www.rtl-sdr.com/wp-content/uploads/2013/04/The-Hobbyists-Guide-PSD-_-MODDED_THUMB1.png?ffccfa&ffccfa)

[Picture's Amazon Link](https://www.amazon.com/gp/product/B00KCDF1QI/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B00KCDF1QI&linkCode=as2&tag=book0674-20&linkId=RSP53QLYXP4IS32X)

如果你需要一本更全面的有关RTL-SDR的书籍，你可能会对我们在Amazon上出售的书籍感兴趣。这本书有实体版和电子版以供使用。

[业余爱好者们的RTL-SDR指南：物美价廉的软件定义收音机](https://www.amazon.com/gp/product/B00KCDF1QI/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B00KCDF1QI&linkCode=as2&tag=book0674-20&linkId=RSP53QLYXP4IS32X)

---------------------------------------------------------

[Share on Twitter](https://twitter.com/intent/tweet?text=Quick+Start+Guide&url=https%3A%2F%2Fwww.rtl-sdr.com%2Frtl-sdr-quick-start-guide%2F)

[Share on Facebook](https://www.facebook.com/share.php?u=https%3A%2F%2Fwww.rtl-sdr.com%2Frtl-sdr-quick-start-guide%2F)

[Share on Reddit](https://www.reddit.com/submit?url=https%3A%2F%2Fwww.rtl-sdr.com%2Frtl-sdr-quick-start-guide%2F)

[Share on Vote](https://news.ycombinator.com/submitlink?u=https%3A%2F%2Fwww.rtl-sdr.com%2Frtl-sdr-quick-start-guide%2F&t=Quick%20Start%20Guide)

[Share via E-mail](mailto:?subject=Quick%20Start%20Guide&body=This%20page%20is%20a%20guide%20aimed%20at%20helping%20anyone%20set%20up%20a%20cheap%20radio%20scanner%20based%20on%20the%20RTL-SDR%20software%20defined%20radio%20as%20fast%20as%20possible%20on%20a%20Windows%20system.%20If%20you%20have%20any%20trouble%20during%20the%20installation%2C%20please%20see%20the%20troubleshooting%20guide%20further%20down%20the%20page.%C2%A0We%20also%20have%20brief%20instructions%20for%20getting%20started%20on%20Linux%20and%20OSX%20at%20the%C2%A0end%C2%A0of%20this%20page.%20Please%20note%20that%20the%20RTL-SDR%20is%20not%20a%C2%A0plug%20and%20play%20device.%20You%20will%20need%20to%20have%20sufficient%C2%A0skills%20to%C2%A0perform%20basic%20PC%20operations%20such%20as%20unzipping%20files%2C%20installing%20software%2C%20moving%20and%20copying%20files%20and%20have%20the%20motivation%C2%A0to%20learn%C2%A0new%20software.%20%2A%2A%2A%2A%2A%2A%2A%0D%0A%0D%0ARead More Here: %20https%3A%2F%2Fwww.rtl-sdr.com%2Frtl-sdr-quick-start-guide%2F)

-----------------------------------------------------------------------------------------------------------

暂时先翻译到这里，原网页下面还有许多问题和解决方案，更新前如果遇到更多问题先查阅[英文原文](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/)
