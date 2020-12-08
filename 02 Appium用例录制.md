# 二、Appium用例录制
## （一）Android自动化前提依赖
1.adb工具

2.模拟器或真机 or 模拟器

&ensp; 1）模拟器：网易mumu  genimotion  或者sdk自带模拟器

&ensp; 2）真机需要root权限

3.Appium Desktop：入门学习工具

## （二）appium desktop功能介绍
1.主要功能：

&ensp; 1）UI分析

&ensp; 2）录制用例

&ensp; 3）元素查找测试

&ensp; 4）Attach 已有的session

&ensp; 5）云测试

2.运行环境是否成功

1）验证环境是否成功

&ensp; ① 首先打开appium desktop，点击star server，不报错

&ensp; ② 其次准备一个Android设备，真机或者模拟器， 

- 链接到电脑上并且通过adb device 查看设备是否连接

&ensp; ③ 最后编写测试脚本，运行脚本

3.获取app的信息

1）APP信息

&ensp; ①获取当前界面元素：adb.shell dumpsys activity top (推荐) （重点）

&ensp; ②获取任务列表：adb shell dumpsys activity activities

2）app入口

① abd logcat |grep -i displayed (推荐) （重点）

② aapt dunp badging mobike.apk |grep launchable-activity

③ apkanalyzer 最新版本的sdk中才有

3）启动应用的某个页面
```
adb shell am start -W -n com.xueqiu.android/.common.MainActivity（重点）
``` 

## （三）利用appium desktop生成用例模板

1.利用desktop生成用例模板
![image](E5361382FAE74B50B4A55F79C03B68F7)

示例：
```
from appium import  webdriver

desire_caps ={
    "platformName":"android",
    "deviceName": "127.0.0.1:62001 device",
    "appPackage":"com.xueqiu.android",
    "appActivity":".view.WelcomeActivityAlias",
    "noReset" :True
}
driver=webdriver.Remote("http://localhost:4723/wd/hub", desire_caps)
driver.implicitly_wait(10)
el4 = driver.find_element_by_id("com.xueqiu.android:id/home_search")
el4.click()
el5 = driver.find_element_by_id("com.xueqiu.android:id/search_input_text")
el5.send_keys("alibaba")
el6 = driver.find_element_by_xpath("/hierarchy/android.widget.FrameLayout/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.FrameLayout/android.view.ViewGroup/android.widget.FrameLayout/android.widget.LinearLayout/android.widget.RelativeLayout/android.widget.FrameLayout/android.widget.LinearLayout/androidx.recyclerview.widget.RecyclerView/android.widget.RelativeLayout")
el6.click()
el7 = driver.find_element_by_id("com.xueqiu.android:id/action_close")
el7.click()

```

注：noRest 表示默认是登录状态。
driver=webdriver.Remote("http://localhost:4723/wd/hub", desire_caps) 是固定写法。
