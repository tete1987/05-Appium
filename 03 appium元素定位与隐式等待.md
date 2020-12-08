# 三、appium元素定位与隐式等待
## （一）desirecapability介绍
1.测试用例的重要部分

&ensp; 1）导入依赖

- `from appium import webdriver`

&ensp; 2）capabilitise设置

&ensp; 3）初始化driver

- `python webdriver.remote`

&ensp; 4）隐式等待，增强用例的稳定性

&ensp; 5）元素定位与操作 find+action

&ensp; 6）断言assert

2.capability设置

&ensp; 1）app apk 地址

&ensp; 2）appPackage包名

&ensp; 3）appActivity Activity名字

&ensp; 4）automationName 默认使用uiautomator2

（Android默认使用uiautomator2，ios默认使用xcuitest）

5）noReset fullReset

- 是否在测试前后重置相关环境（例如首次打开弹框，或者是登录信息）

- 演示雪球的首次启动弹框功能，noreset=True，norest=FALSE 情况

6）unicodeKeyBoard  resetKeyBoard 
- 是否需要输入非英文之外的语言并在测试环境完成后重置输入法

7）官方文档：https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/caps.md

8）dontStopAppOnReset：首次启动的时候，不停止app（可以调试或者运行的时候提升运行速度）

9）skipDeviceInitialization：跳过安装，权限设置等操作（可以调试或者运行的时候提升运行速度）

## （二）appium元素定位
1.常用的两种定位方式:id，accessbility_id

1）driver.find_element_by_id(resource-id)

2）driver.find_element_by_accessibility_id(content-desc)

2.三种经典等待方式

1）强制等待： sleep （不推荐）

2）隐式等待（全局性）：

&ensp;  ① 设置一个超时时间，服务端appium会在给定的时间内，不停的查找，默认值是0

&ensp; ② 用法：driver.manage().timeout().implicitlyWait(10,TimeUnit.SECONDS);

3）显示等待
```
Element=WebDriverWait(driver,10，0.5).
until(expected_conditions.visibility_of_element_located(MobileBy.ID,"com.android.settings:id/title"))
```

4）在客户端等待
