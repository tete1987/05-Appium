# 八、 appium显示等待机制
## （一）Wait等待
1.等待方式：

&ensp; 1）强制等待：sleep（不推荐）

&ensp; 2）全局隐式等待：
- 在服务器等待

`driver.implicitly_wait(TIMEOUT)`

&ensp; 3）显示等待
- 在客户端等待
```
WebDriverWait(self.driver,10).
until(expected_conditions.visibility_of_element_located(LOCATOR)
```

2.显示等待

&ensp; 1）显示等待与隐式等待相对，显示等待必须在每个需要等待的元素前面进行声明

&ensp; 2）是针对与某个特定的预算怒设置的等待时间，在设置时间内，默认每隔一段时间检测一次当前页面某个元素是否存在

&ensp; 3）如果在规定的时间内找到了元素，则直接执行，即找到元素就执行相关操作。

&ensp; 4）如果超过设置时间检测不到则抛出异常。默认检测频率为0.5s，默认抛出异常为：NoSuchElementException

&ensp; 5）显示等待用到的两个类：
- WebDriverWait
- expected_condition

&ensp; 6）显示等待可以等待动态加载的ajax元素，显示等待需要使用ExpectedConditions来检查条件

&ensp; 7）一般页面上元素的呈现
- title出现：首先出现title
- dom树出现：presence，还不完整
- css出现：可见 visibility
- js出现，js特效执行：可点击clickable

&ensp; 8）html文档是自上而下加载的

&ensp; 9）js文件加载会阻塞HTML内容的加载，有些js异步加载的方式来完成js的加载
&ensp; 10）样式表下载完成之后会跟之前的样式一起进行解析，会对之前的元素重新渲染

3.WebDriverWait用法

&ensp; 1）WebDirverWait用法
- WebDriverWait(driver.timeout,poll_frequency=0.5,ignore_exceptions=None)
- driver：浏览器驱动
- timeout：最长超时时间，默认以秒为单位
- poll_frequency：检测的间隔步长，默认为0.5s
- ignored_exceptions：超时后的抛出异常信息，默认抛出NoSuchElementException异常

&ensp; 2）WebDriverWait的until()和until_not()方法：
- method：在等待期间，每隔一段时间（__init__中的poll_frequency）调用这个传入的方法，直到返回值不是False
- message：如果超时，抛出异常TimeoutException，将message传入异常
- until_not：与until 相反，until是当某元素出现或什么条件成立则继续执行，until_not 是当某元素消失或什么条件则继续执行，参数也相同

4.expected_conditions 类

1）presence_of_element_located 判断元素是否被加到了DOM树里，并不代表该元素一定可见
- 用法：WebDriverWait().until(expected_conditions.presence_of_element_located(元素对象))
 
2）visibility_of_element_located 判断某个元素是否可见，可见代表元素非隐藏，并且元素的宽和高都不等于0

- 用法：WebDriverWait().until(expected_conditions.visibility_of_element_located(元素定位))

示例：
```
    def test_search(self):
        print("搜索测试用例")
        '''
        1.打开 雪球 app
        2.点击搜索输入框
        3.向搜索输入框里输入“阿里巴巴”
        4.在搜索结果里面选择“阿里巴巴”，然后进行点击
        5.获取这只香港 阿里巴巴的股价，并判断股价的价格>170
        6.增加显示等待
        '''
        self.driver.find_element_by_id("com.xueqiu.android:id/tv_banner").click()
        self.driver.find_element_by_id("com.xueqiu.android:id/search_input_text").send_keys("阿里巴巴")
        self.driver.find_element_by_xpath("//*[@resource-id='com.xueqiu.android:id/name' and @text='阿里巴巴']").click()
        locator = (MobileBy.XPATH,"//*[@text='09988']/../../..//*"
                                                               "[@resource-id='com.xueqiu.android:id/current_price']")
        WebDriverWait(self.driver,10).until(expected_conditions.element_to_be_clickable(locator))
        ele = self.driver.find_element(*locator)
        print(ele.text)
        current_price=float(ele.text)
        expect_price = 170
        assert current_price > expect_price
```
注：MobileBy 方法继承了By方法，增加了移动端的一些功能，所以可以直接调用。

5.使用lambda表达式


WebDriverWait(driver,time).until(lambda x:x.find_element_by_id("someId"))返回一个元素

```
    def test_search(self):
        print("搜索测试用例")
        '''
        1.打开 雪球 app
        2.点击搜索输入框
        3.向搜索输入框里输入“阿里巴巴”
        4.在搜索结果里面选择“阿里巴巴”，然后进行点击
        5.获取这只香港 阿里巴巴的股价，并判断股价的价格>170
        6.增加显示等待
        '''
        self.driver.find_element_by_id("com.xueqiu.android:id/tv_banner").click()
        self.driver.find_element_by_id("com.xueqiu.android:id/search_input_text").send_keys("阿里巴巴")
        self.driver.find_element_by_xpath("//*[@resource-id='com.xueqiu.android:id/name' and @text='阿里巴巴']").click()
        locator = (MobileBy.XPATH,"//*[@text='09988']/../../..//*"
                                                               "[@resource-id='com.xueqiu.android:id/current_price']")
        
        ele = WebDriverWait(self.driver,10).until(lambda x:x.find_element(*locator))
        print(ele.text)
        current_price=float(ele.text)
        expect_price = 170
        assert current_price > expect_price
```

### 总结三种等待方式
1.隐式等待，尽量默认都加上，时间限定在3-6s，不要太长，为了所有的find_element 方法都有一个很好的缓冲

2.显示等待，用来处理隐式等待无法解决的一些问题，比如：文件上传（可设置长一点），文件上传需要设置20s以上，但是如果设置隐式等待，它会在每个find方法都等这么长时间，一旦发现没有找到元素，就会等20s以后才抛出异常，影响case的执行效率，这时候就需要用显示等待，显示等待可以设置的长一点

3.强制等待：一般不推荐，前两种基本解决绝大部分问题，如果某个控件没有任何特征，只能强制等待，这种情况比较少
