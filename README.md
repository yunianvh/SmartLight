
### 初识Arduino
<hr/>

记得不久前写过一篇关于如何从一个Android小白程序员，最后逼成一个后台和运维通吃的苦逼程序员，那么今天来跟大家分享一下如何从一个IPTV全栈工程师（自封）到硬件开发小白的心酸过程。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019070617403126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
简单说Arduino是一款便捷硬件开发，这玩意有点像C，但又不像C，反正对于像我这种C基础不太好的苦逼程序员去快速了解硬件开发是一个很不错的选择。
### 安装Arduino IDE
<hr/>

以下的步骤是基于 Windows 操作系统，如果你使用的是其他操作系统，可以将其作为参考。
首先，你需要从官网下载最新版本的 Arduino IDE 软件。下载链接：
http://arduino.cc/en/Main/Software
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708115057487.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
在下载页右侧的列表中选择下载对应的安装包。对于 Windows 系统用户既可以选择下载 Windows installer（推荐初次使用者下载），也可以下载 Windows ZIP 安装包（需要手动安装驱动）。若选择的是 Windows installer，你可以直接执行安装程序，并跟随安装向导完成配置，驱动会在程序安装完成后自动安装。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708115203432.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
Arduino IDE 本身支持多种语言（包括中文），我们只需设置为中文即可。
打开 Fire->Preferences->Editor language,选择简体中文（Chinese（China）），然后重启 IDE。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708115320984.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
### ESP32 Blink（控制主板led）
<hr/>

#### 安装 FireBeetle Board-ESP32 开发板核心

Arduino IDE 安装包中不包含 FireBeetle Board-ESP32 开发板核心，需要手动添加。首先，要添加 FireBeetle Board-ESP32 支持，需要在 Arduino 开发板管理器里手动安装FireBeetle Board-ESP32 开发板核心。

（1）打开文件->首选项，在附加开发板管理器网址中，将以下网址复制进去：
https://git.oschina.net/dfrobot/FireBeetle-ESP32/raw/master/package_esp32_index.json
点击好，完成设置。

（2）打开工具->板子->开发板管理器
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019070811590757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
在打开的开发板管理器中，输入“FireBeetle”并等待信息加载完毕。版本号为 0.0.9
（或者最新版本并点击“安装”后耐心等待安装完成。整个过程会因网络状况持续 5-10 分钟。安装完成后，开发板信息会被标注“INSTALLED”），如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120012831.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)

==注意: 如果发现安装过程中一直处于卡顿现象，可能是网络原因引起的，您可以尝试强制重启 Arduino IDE，重新执行之前的步骤，或者通过翻墙软件加速网络，直到安装完成。其次，在安装过程中，有些关键程序可能会被防火墙或者杀毒软件拦截，请选择允许更改并添加至白名单。==

#### 连接 FireBeetle Board-ESP32 至电脑

正确安装完成 Arduino IDE 和 FireBeetle Board-ESP32 开发板核心后，即可将
FireBeetle Board-ESP32 通过 USB 数据线连接至电脑。正确连接时 FireBeetle
Board-ESP32 的 CHG 电源指示灯会闪烁（这是在查询有没有接入锂电池）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120224226.png#pic_center)

在编程之前，我们需要确保开发板被电脑识别，并找出连接了哪一个 COM 口（用于提供串口通信交互）。可以在接下来的步骤中确认。

首先打开“计算机管理”，打开“设备管理器”，点开“端口（COM 和 LPT）”。接上
FireBeetle Board-ESP32 的端口就会在列表中显示（这里是 COM4）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120316950.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
如果提示无法识别的设备，你需要下载 FireBeetle Board-ESP32 驱动到本机，并安装驱动，下载地址：https://github.com/Chocho2017/FireBeetle-Board-ESP32.git

将下载后的 FireBeetle-ESP32.inf 驱动文件保存到你的电脑（任意位置都可），右键点击 FireBeetle-ESP32，选择更新驱动程序软件，如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120500436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
选择浏览计算机以查找驱动程序软件，在地址栏中输入你刚刚保存的
FireBeetle-ESP32.inf 文件目录，点击下一步，然后根据提示完成驱动文件的安装，如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120538234.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
==注：上面方法不行就从这里下：https://gaic.alicdn.com/doc/hacklab/hqqro6.html?spm=a2c56.pc_iot_community_demo_detail.demo-detail.7.66a652064rUnqX==

#### 在 Arduino IDE 中进行编程

Arduino IDE 软件安装完成后，运行软件打开编程窗口。你可以在这个窗口里编辑并上传代码到 Arduino 开发板上，或是使用内置的串口监视器与开发板通信。Arduino IDE 界面如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019070812070468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
与常规C 语言程序不同的是，一段用于Arduino 的程序通常由 void setup()部分与 void loop()两部分构成。

“void setup()”用于放置初始化程序的代码，这部分代码在开发板上电后仅运行一次。需重复运行的代码需放置在”void loop()”中，这些代码会一直重复运行，使得开发板与外部进行交互。

#### 上传代码至 FireBeetle Board-ESP32 主板

在这一步，我们将演示如何上传事例程序”Blink”到FireBeetle Board-ESP32主板。”Blink”程序的功能是控制 D9 引脚上的 LED 灯间隔 1s 闪烁一次。FireBeetle Board-ESP32 主板与大部分 Arduino 相同，有一个板载的 D9 LED 信号灯，这意味着在本例中我们不需要连接其他的外设原件。LED 状态指示灯可在 FireBeetle Board-ESP32 主板上找到，如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708120830567.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
打开文件->事例->Basics->Blink，在上传之前，你应该首先确认代码中没有错误。点击“编译”确认。等待几秒，若没有错误，则会在信息窗口显示“编译完成”，表示编译成功。若出现错误可以返回检查程序是否完整。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708121016203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
编译成功后，选择工具->开发板->FireBeetle-ESP32。

然后再并根据 STEP4 中显示的FireBeetle Board-ESP32 所占用的端口号，我们应该选择“COM4”作为通信端口。COM和开发板选择完成后，开发板的信息和端口号就会在窗口右下角显示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708121201955.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
最后，点击“上传”烧写代码到 FireBeetle Board-ESP32 中。成功上传后，“上传成功”消息会出现在信息窗口。此时 FireBeetle Board-ESP32 板载的 D9 LED 灯会开始闪烁。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708121248395.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
简而言之，为 Arduino 上传代码可以分为以下三个步骤：

 ==1. 编译代码； 
 2. 选择开发板型号和端口号； 
 3. 上传！==

#### 我的错误记录

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708135551275.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
开始出现上图错误时还以为是自己电脑缺少python27.dll引起，网上一查发现关于arduino的资料还真少，折腾了一早上还是不行，最后重新卸载端口驱动，然后从新下载安装一遍就可以了。
下载地址：http://www.wch.cn/download/CH341SER_EXE.html
### LED灯光控制案例
<hr/>
经过一早上的折腾可算是把开发环境弄完了，迫不及待的要来跑一个简单的案例，对接阿里云，实现远程控制LED灯光。

#### 所需元件
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019070814103431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)

 1. 红色食人鱼 LED 
 2. 发光模块 x1 FireBettle Board-ESP32 x1
 3. FireBettle Gravity 扩展板x1 
 4. 智能手机 x1

#### 硬件连接
把 FireBettle Gravity 扩展板直插在 FireBettle Board-ESP32 主板上，再把红色 LED 模块接在扩展板的 D2 数字引脚上，确保电源引脚、接地引脚和信号引脚都连接正确。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708141220475.png#pic_center)
元件连接好后，使用 USB 线连接 FireBettle Board-ESP32 主板和电脑。硬件准备好后，接下来就需要我们在阿里云平台上创建相应的产品，设备，服务来建立物理设备和阿里云 IoT 平台之间的联系了。
#### Arduino 程序
打开 Arduino IDE，点击文件->示例->DFRobot_Aliyun->SmartLight 项目，如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708141648677.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
==注：如上图的案例代码是需要自己先下载好对应的库文件，存放到 Arduino IDE 安装目录下的libraries 文件中，具体如下：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708142125385.png#pic_center)
下载地址：http://www.dfrobot.com.cn/images/upload/File/20190327164350d56gcn.rar

#### 修改案例
将如下四点修改完成，即可上传代码，在手机端或阿里云IOT Stutio上进行控制设备了。
 1. WiFi 名称和密码的配置；
 2. 设备证书信息配置；
 3. 产品标识符配置；
 4. 上报和订阅 TOPIC 配置；
 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708142636570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MzUwNjU0,size_16,color_FFFFFF,t_70#pic_center)
==注：这些配置信息中，除了 WiFi 名和密码需要用户连接自己的 WiFi，其他的配置信息都需要从阿里云 IoT 平台上获取。详情参见阿里云物联网平台==

### 文章总结
对于我们这样的新手而言，主要工作量还是在于开发环境的搭建，其实连接个元器件，跑个栗子等这些后期工作对于大家来说都是很容易的事情。

其实熟悉阿里云IOT物联网平台的朋友可能都会知道，为了方便大家一站式开发，阿里云也推出了自己的[Hacklab](https://hl4481.hacklab.aliyun.com/#/home/hacklab/workspace)在线编译平台，在编程上其实和Arduino（[Arduino也有自己的在线编译平台](https://create.arduino.cc/editor/YuNianVH/24d93243-8140-498b-9983-78478b0856b8)）大同小异，从新搭建一个本地IDE也不是没有必要了，至少让我们更加熟悉Arduino的开发环境码。

下面放几张动力图，也许硬件开发真没用想象中那么困难，只要我们愿意迈出这一步，希望看到看不到这篇文章的你们都能月薪20K以上。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190708145422740.gif)
### 资源下载
Arduino IED：https://www.arduino.cc/en/Main/Donate <br/>
ESP32 USB串口驱动：http://www.wch.cn/download/CH341SER_EXE.html <br/>
CSDN Demo：https://blog.csdn.net/qq_35350654 <br/>
