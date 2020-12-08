# 五、app控件交互
## （一）元素的常用方法
1.常用方法：

1）点击方法：element.click()

2）输入操作：element.send_keys("appium")

3）设置元素的值：element.set_value("appium")

4）清除操作：element.clear()

5）是否可见：element.is_displayed()  返回True/False

6）是否可用：element.is_enable() 返回True/False

7）是否被选中：element.is_selected() 返回True/False

8）获取属性值：get_attribulte(name)

 - get_atrribute()方法能获取的属性，元素的属性几乎都能获取到，属性名和uiautomatorviewer里面的一致。
 - 源码地址：https://github.com/appium/appium-uiautomator2-server/blob/master/app/src/main/java/io/appium/uiautomator2/handler/GetElementAttribute.java
 - {text,name} ：text(返回 text)
 - {class,className} ：（返回class，只有API=> 18 才能支持）
 - {resource-id,resourceId}：（返回resource-id，只有API=> 18 才能支持）
 - {content-desc,contendDescription}：（返回contend-desc 属性）
 - checkable,checked,clickable,enabled,focusable,focused,{long-clickable,longClickable},package,password,scrollable,selection-start,selection-end,selectde,bounds,displayed,contentSize：  返回True/False
 
## （二）元素的常用属性

1.获取元素文本：
- 格式：element.text

2.获取元素坐标：
- 格式：element.location
- 结果：{'y':19,'x':498}

3.获取元素尺寸（高和宽）
- 格式：element.size
- 结果：{'width':500,'height':498}

4.案例：

1）打开【雪球】应用

2）定位首页的搜索框

3）判断搜索框的是否可用，并查看搜索框name属性值

4）打印搜索框这个元素的左上角坐标和它的宽高

5）向搜索框输入：alibaba

6）判断【阿里巴巴】是否可见

7）如果可见，打印“搜索成功”点击，如果不可见，打印“搜索失败”


示例：
```
import pytest
from appium import webdriver
class TestAppSearch:
    def setup(self):
        caps = {}
        caps["platformName"] = "android"
        caps["deviceName"] = "127.0.0.1:62001"
        caps["appPackage"] ="com.xueqiu.android"
        caps["appActivity"] ="com.xueqiu.android.common.MainActivity"
        caps["noReset"] ="true"
        caps["skipDeviceInitialization"] ="true"
        caps["unicodeKeyBoard"] ="true"
        caps["resetKeyBoard"] ="true"

        # caps["dontStopAppOnReset"] ="true"
        self.driver = webdriver.Remote("http://localhost:4723/wd/hub", caps)
        self.driver.implicitly_wait(10)

    def teardown(self):
        self.driver.back()
        self.driver.back()
        self.driver.quit()

    def  test_attr(self):
       '''
        1）打开【雪球】应用
        2）定位首页的搜索框
        3）判断搜索框的是否可用，并查看搜索框name属性值
        4）打印搜索框这个元素的左上角坐标和它的宽高
        5）向搜索框输入：alibaba
        6）判断【阿里巴巴】是否可见
        7）如果可见，打印“搜索成功”点击，如果不可见，打印“搜索失败”
       :param self:
       :return:
       '''
       element_search=self.driver.find_element_by_id("com.xueqiu.android:id/tv_banner")
       search_enable = element_search.is_enabled()
       print(element_search.text)
       print(element_search.location)
       print(element_search.size)
       if search_enable == True:
           element_search.click()
           self.driver.find_element_by_id("com.xueqiu.android:id/search_input_text").send_keys("阿里巴巴")
           alibaba_element = self.driver.find_element_by_xpath(
               "//*[@resource-id='com.xueqiu.android:id/name' and @text='阿里巴巴']")

           element_disaply= alibaba_element.get_attribute("displayed")
           #get_attribute 返回值是 字符串‘true’
           if element_disaply == 'true':
               print("搜索成功")
           else:
               print("搜索失败")


if __name__ == '__main__':
        pytest.main()

```
