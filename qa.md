# BanGround内测 Q&A手册

欢迎各位BanGrounder参加BanGround先行内测

本次内测为封闭测试，请各位自己体验游戏交互、美术等方面，并给我们提出您宝贵的合理的意见或建议，您的支持会让这个游戏变得更好

特别提示：请您仔细阅读群公告与Q&A手册的内容，**询问群公告与Q&A手册中已有内容将会受到警告**，Q&A手册可以解答您的大部分疑问

由于手册更新有延迟，最新动态**以群内公告为准**

先行内测主要测试游戏本体，谱面相关问题恕不解答

内测报名人数较多，且为了能更好地完成测试任务，本群将定期清理不活跃的内测用户

_不活跃：指两周内没有登录游戏的记录_

## 安装游戏

**先看群公告**，群公告告知了游戏的最新版本

### 安卓

在内测群的群文件中，找到**Android**文件夹，从里面下载最新版本安装

### iOS

1. 越狱设备

	在内测群的群文件中，找到**iOS**文件夹，从里面下载ipa文件直接安装

2. 非越狱设备

	在内测群的群文件中，找到**iOS**文件夹，从里面下载ipa文件，然后通过**Mac、装有黑苹果或黑苹果虚拟机的PC**进行自签

	> [通过macOS自签教程](/insmacos)

	*原来的Appcake方法已经失效*

***由于不明原因，证书版会出现掉签的情况，所以不再提供证书版下载，原先购买证书版的可以选择退款或等社区建设完成后可以获得额外1个月Supporter Ⅳ资格作为补偿***


### Windows

在内测群的群文件中，找到**Window**文件夹，从里面下载最新版本安装

## 进入游戏

安装好游戏后，点击游戏图标启动游戏。首次启动需要**auth key**

获取auth key请在内测群使用`/auth register`指令，机器人会将密钥通过私聊的形式发送给你

auth key遗忘或丢失请在内测群使用`/auth view`指令，机器人会将你拥有的密钥通过私聊的形式发送给你

**安卓用户**以及**Windows用户**更新游戏后，原有auth key可以继续使用

**苹果用户**更新游戏后，请先使用`/auth view`查询原有auth key的id，再使用`/auth clear id`清除设备信息

[_更多机器人指令_](/qa?id=auth-key-相关)

如果你有多个设备需要测试，请联系管理员为你申请新的auth key

## 获取/导入谱面

### 获取谱面

1. 群文件

	内测群的群文件的**测试导入包**文件夹里，有各种各样的谱面可以下载测试

2. 群机器人

	你可以在群里或私聊**一只摸鱼的鱼**使用`小站`指令，它会告诉你小站的地址。你可以在里面下载谱面

	你也可以使用`kirapack`+`bestdori自制谱谱面id`指令，它会帮你转换并告诉你谱面下载地址

3. Windows 端转谱器

	可以转换 bestdori，官谱，bangbangboom v2

通过以上途径得到的文件是以`.kirapack`作为后缀的文件

### 导入谱面

#### 安卓

下载后直接打开文件，文件类型选择**其它**，然后在应用列表里使用**BanGround-Unity**打开

如果你之前启动了游戏没有退出，请开始一次演出后退出，或重启游戏，谱面就会自动加载了

如果找不到直接打开的选项，请尝试把kirapack文件手动移动到以下路径：
```
/Android/data/fun.BanGround.Game/files/Inbox/
```
然后启动游戏

#### iOS

下载后直接打开文件，选择`拷贝到BanGround-Unity`，然后启动游戏

也可以使用`隔空投送`，但请确保游戏没有在前台启动

如果无法导入，请打开Files应用，尝试把kirapack文件移动到以下路径：
```
我的iPhone/iPad > BanGround
```
然后启动游戏

#### Windows

先运行一次游戏，谱面下载后直接打开文件

如果你之前启动了游戏没有退出，请开始一次演出后退出，或重启游戏，谱面就会自动加载了

如果直接打开文件没有成功导入，请尝试把kirapack文件手动移动到以下路径：
```
%LocalAppdata%Low\Kirakira Games\BanGround-Unity\InBox
```
然后启动游戏

## 延迟调节

目前还没有可视化调节延迟的选项，需要根据自己平时的经验进行调节

您也可以尝试下列的任一方法进行调节：

1. **设置**的**判定**选项卡里，调节**音频偏移**，效果为BanG Dream本家的17倍

2. **设置**的**判定**选项卡里，打开**显示PERFECT的E/L**选项。进入游戏正常游玩后，观察结算界面的 Early/Late 数目和平均偏移，遵循**Early多调大，Late多调小**的原则调节**音频偏移**，**Early多调小，Late多调大**的原则调节**判定偏移**，直至数目和平均偏移相近为止

3. **设置**的**判定**选项卡里，将**音频偏移**和**判定偏移**均设置为0，关闭**显示 PERFECT的E/L**选项。进入游戏正常游玩后，观察结算界面的 Early/Late 数目和平均偏移，按以下公式计算得到**判定偏移**的值：

$$
judge=\begin{cases}
\overline{Early}-40,\overline{Early}>\overline{Late} \\
40-\overline{Late},\overline{Early}\leq\overline{Late} \\
\end{cases}
$$

4. 打击音延迟大请尝试减小缓冲区

_注意：调节偏移的单位为毫秒，使用“Offset Rhythm Test”谱面进行上述调节可以获得更好的效果_

## 爆音/没有声音

1. 调整缓冲区

	调大缓冲区，建议调整到无爆音的最小值

2. 切换音频引擎

	在**设置**的**声音**选项卡里，选择另一个音频引擎，然后重启再试

3. 使用群文件里的**爆音修复版(fmod1)**

_注意：以上选项变更后都需要重启游戏_ 


## 其他问题

小站相关问题请找猫猫

kirapack导入失败请在群里附上错误信息截图

**游戏本体其他问题请自行提交issue：[https://github.com/BanGround/BanGround-Unity/issues](https://github.com/BanGround/BanGround-Unity/issues)** 或通过机器人提交

*始终推荐自行提交，支持markdown，通过机器人提交issue请不要试图使用特殊格式(html/markdown/etc)，还会有奇怪的bug*

##### 通过机器人提交issue

1. 在群里发送`/issue create`，然后与机器人私聊

2. 根据机器人提示依次发送**问题标题**、**问题描述**、**如何复现问题**、**设备信息**、**补充截图**、**确认发送**

- 您可以通过机器人收到issue的最新动态

[_更多机器人指令_](/qa?id=issue-相关)

## 群机器人指令

`/help` 获取机器人帮助

#### auth key 相关

`/auth register` 注册用户

`/auth view` 查看所拥有的key(获得以下指令id参数)

`/auth login [id]` 查询最近登陆信息

`/auth clear [id]` 清除设备信息

#### issue 相关

`/issue create` 创建issue

`/issue create` 创建issue

`/issue list` 查看我创建的issue(获得以下指令id参数)

`/issue view [id]` 查看issue详情

`/issue comment [id]` 评论并订阅issue

`/issue unsubscribe [id]` 取消订阅issue(创建者不能取消订阅)

## 其他资源

- 游戏Wiki：[https://wiki.banground.fun](https://wiki.banground.fun)

- 项目进展：[https://github.com/orgs/BanGround/projects/2](https://github.com/orgs/BanGround/projects/2)

- ebbb在线制谱器：[https://editor.bangbangboom.moe/](https://editor.bangbangboom.moe/)   

	_ebbb国内线路_
[*(gitee)*](https://reikohaku.gitee.io/ebbb) [*(小站)*](http://212.64.10.35:8081/)

- 摸鱼小站：[http://212.64.10.35/](http://212.64.10.35/)

***

手册版本：V1.5.5

更新日期：2020/04/09