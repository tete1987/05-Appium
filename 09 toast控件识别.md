# 九、toast控件识别
## （一）toast定位
1.toast介绍

Toast，简易的消息提示框

&ensp; 1）为了给当前视图显示一个浮动的显示块，与dialog不同，它永远不会获得焦点

&ensp; 2）Toast类的思想：尽可能不引人注意，同时还向用户显示信息希望他们看到

&ensp; 3）Toast显示的时间有限，Toast会根据用户设置的显示时间后自动消失

&ensp; 4）Toast本身是个系统级别的控件，它归属于系统settings，当一个app发送消息的时候，不是自己造出来的这个弹框，它是发给系统，由系统统一进行弹框，这类的控件不再app内，需要特殊的控件识别方法


1.appium使用uiautomator底层的机制来分析抓取toast，并且把toast放到控件树里面，但本身不属于控件。

2.automationName：uiautomator2

3.getPageSource是无法找到的

4.必须使用xpath查找
- //*[@class='android.widgt.Toast']
- //*[contains(@text,'XXXXX')]

![toast内容](https://github.com/tete1987/picture_resource/blob/master/toast%E5%86%85%E5%AE%B9.png)

示例：

先使用 adb shell dumpsys window | grep mCurrent 查看当前启动的包和页面名称。如果Windows上不能直接使用grep，可下载Grep for Windows 插件，并配置环境变量：C:\Program Files (x86)\GnuWin32\bin 
```
from appium import webdriver
from appium.webdriver.common.mobileby import MobileBy

class TestApiDemo:
    def setup(self):
        caps = {"platformName": "android",
                "deviceName": "127.0.0.1:62001",
                "appPackage": "com.example.android.apis",
                "appActivity": "com.example.android.apis.view.PopupMenu1",
                "skipDeviceInitialization": "true",
                "unicodeKeyBoard": "true",
                "resetKeyBoard": "true",
                "automationName": "uiautomator2"
                }
                
        self.driver = webdriver.Remote("http://localhost:4723/wd/hub", caps)
        self.driver.implicitly_wait(5)

    def teardown(self):
        self.driver.quit()

        def test_api(self):
        self.driver.find_element(MobileBy.XPATH,'//*[@text="MAKE A POPUP!"]').click()
        self.driver.find_element(MobileBy.XPATH,'//*[@text="Search"]').click()
        # print(self.driver.find_element(MobileBy.XPATH, '//*[@class="android.widget.Toast"]').text)
        #或也可以这样写：
        print(self.driver.find_element(MobileBy.XPATH, '//*[contains(@text,"Clicked popup")]').text)

```
注：automationName是工作引擎。
