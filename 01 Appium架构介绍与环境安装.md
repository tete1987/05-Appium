# 一、Appium架构介绍与环境安装
## （一）目前mobile自动化解决方案
1.ios自动化：

&ensp; 1）calabash-ios

&ensp; 2）Frank

&ensp; 3）UiAutomation

&ensp; 4）ios-driver

&ensp; 5）KeepltFunctional

2.Android

&ensp; 1）calabash-android

&ensp; 2）MonkeyTaik

&ensp; 3）Robotium

&ensp; 4）UiAutomator

&ensp; 5）selendroid

3.自动化工具选择

需考虑因素：
- 1）单平台测试or多平台测试？
- 2）是否有多设备同时测试的场景？
- 3）不局限于测试环境，任何版本任何环境都可以测试？
- 4）最擅长哪种开发语言？
- 5）当前市面是否有满足项目需求的测试工具？是否需要二次开发？

|工具名称| 被测系统| 测试| 脚本语言| 支持H5| 跨应用| 稳定性| SDK自动|
|----|----|----|----|----|----|----|----|----|----|
|MonkeyRunner|Android | 功能| python| 支持| 否| 稳定| 是|
|Instrumentation| Android(<4.1)| 功能| Java| 支持| 可以 | 稳定 |否|
|Uiautomator2| Android(>=4.1)| 功能| Java| 支持| 可以 |稳定| 是|
|Adb-For-Test| Android(>=4.1)| 功能| Java/python|  支持| 可以|  稳定| 否|
|Monkey| Android| 稳定| Java| 否| 否| 稳定 |是|
|CTS| Android |兼容 |Java| 支持|  可以 |稳定 |否|
|Uiautomation| ios| 功能| js| 支持|  可以| 稳定| xcode自带|
|Calabash| Android ios| 功能| Ruby| 支持 | 可以| 一般| 否|
|Appium |Android ios| 功能| Java/python/js/c/c#/perl| 支持 | 可以|一般| 否|
## （二）Appium介绍
&ensp; appium是一个移动端的自动化测试框架，可用于测试原生应用，移动网页应用和混合应用，且是跨平台的。可用于ios和Android操作系统。原生应用是指用Android或ios编写的应用，移动网页是指网页应用，类似于ios中safari应用或者chrome应用或者类似浏览器的应用。混合应用是指一种包裹webview的应用，原生应用网页内容交互性的应用。

&ensp;  重要的是appium是跨平台的。何为跨平台，意思是可以针对不同平台用一套api来编写脚本。

## （三）Appium框架介绍

1.推荐Appium
- 跨语言：Java、Python、nodejs
- 跨平台：Android、ios
         - windows   mac

- 底层引擎可以结合
- 生态丰富、社区强大

2.Appium引擎列表

1）Android：
- espresso
- selendroid
- uiautomator
- uiautomator2(推荐)

2）ios
- uiautomation
- xcuitest(推荐)

3）windows

4）mac

3.Appium的设计理念

1）webdriver是基于htttp协议的，第一连接会建立一个session会话，并通过post发送一个json告知服务端相关测试信息。

2）Client/Server设计模式
- 客户端通过webDriver json write 协议与服务端通讯
- 多语言支持

3）server可以放在任何地方

4）服务端NODEJS开发的http服务

5）appium使用appium-xcuitest-driver来测试iPhone设备，其中需要安装Facebook出的WDA（webdriver agent）来驱动ios测试

## （四）Appium环境安装
1.appium生态工具

1）adb：Android的控制工具，用于获取Android的各种数据和控制

2）Appium Destop：内嵌了appium server 和inspace 的综合工具

3）Appium Server：appium的核心工具，命令行工具

4）Appium client：各种语言的客户端封装库，用于连接appium server（python\java\ruby\roborframework-appium）

5）AppCrawler 自动遍历工具

2.环境安装：
- java1.8 版本
- Android sdk
- Node js（>=10版本）、npm（>=6版本）
- python3
- appium-desktop
- Appium python client

 1）安装JDK（1.8版本）
 
① 官网下载地址：http://www.oracle.com/technetwork/java/javase/downloads/index.html

② 安装（一直点下一步）完成，用默认路径即可

③ 配置环境变量：

JAVA_HOME ：D:\Android\Java\jdk1.8.0_25 (注意这里面的JAVA_HOME大写后面会用到)
classpath： .;%JAVA_HOME% \lib\dt.jar;%JAVA_HOME%\lib\tools.jar;(最前面加个点和分号)

path ： %JAVA_HOME% \bin;%JAVA_HOME% \jre\bin;

④ 检查java环境是否配置好

⑤ 进入命令行，输入 java -version 或javac -version，输出本编号信息即成功

2）安装SDK

①下载sdk：

Android studio地址：http://developer.android.com/studio/index.html

中文官网下载地址：http://tools.android-studio.org/index.php/sdk
    
② 安装sdk：

其实sdk就是个文件夹，下载之后需要手动更新，配上环境变量就可以使用，不需要手动安装

③ 配置android SDK环境变量如下：

ANDROID_HOME: C:\Users\Administrator\AppData\Local\Android\android-sdk

PATH: %ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools

④ 检查是否安装成功，cmd输出：
  - adb回车或者adb shell 然后回车

3）安装appium desktop（appium server + appium inspector工具） 

① 下载对应操作系统的安装包：https://github.com/appium/appium-desktop\releases
② 如果不需要appium inspector ，也可以通过npm 直接安装appium

③ 官方安装：npm install -g appium(不推荐)

淘宝提供（推荐）：

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

`cnpm install -g appium`
 
 ④ 运行 appium（不报错说明安装成功）
 
4）安装appium python client

① 方式1：pip install appium-python-client（推荐）

② 方式2：下载源码包：

下载地址：https://github.com/appium/python-client
 
 https://pypi.python.org/pypi/Appium-Python-Client

解压后在命令行中进入python-client-master目录，该目录下包含setup.py

执行命令python setup.py install 命令安装客户端

③ 安装成功之后，在cmd中输入：

```
python

from appium import webdriver

import appium
```
不报错，说明已经安装成功了。

5）安装appium-doctor检测appium的安装环境

`cnpm install appium-doctor`
