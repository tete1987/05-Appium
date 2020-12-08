# 四、app控件定位
## （一）android/ios 基础知识
1.Android是通过容器的布局属性来管理子控件的位置关系，布局过程就把界面上的所有控件根据他们的间距大小，摆放在正确的位置上。

2.Andriod 七大布局

&ensp; 1）LinearLayout （线性布局）

&ensp; 2）RelativeLayout（相对布局）

&ensp; 3）FrameLayout（帧布局）

&ensp; 4）AbsoluteLayout（绝对布局）

&ensp; 5）TableLayout（表格布局）

&ensp; 6）GridLayout（网格布局）

&ensp; 7）ConstraintLayout（约束布局）

3.android四大组件

&ensp; 1）anctivity 与用户交互的可视化界面

&ensp; 2）service 实现程序后台运行的解决方案

&ensp; 3）content provider 内容提供者，提供程序所需要的数据

&ensp; 4）broadcast receiver 广播接收器，监听外部事件的到来（比如来电）

4.常用的控件：

&ensp; 1）TextView （文本控件）

&ensp; 2）Button（按钮），ImageButton（图片按钮），ToggleButton（开关按钮）

&ensp; 3）ImageView（图片控件）

&ensp; 4）CheckBox（复选框控件），RadioButton（单选框控件）

5.布局是一种可用于放置很多控件的容器，它可以按照一定的规律调整内部控件的位置，从而编写出精美的界面。当然，布局的内部出了放置控件外，也可以放置布局，通过多层布局的嵌套，我们就能够完成一些比较复杂的界面。

6.IOS的基础知识

1）ios介绍

&ensp; ①由苹果公司为iPhone开发的操作系统，主要给iPhone，iTouch，ipad使用

&ensp; ②原名为iPhoneOS，2010年WWDC大会改名为ios

&ensp; ③目前ios最新版本是ios13

2）布局：ios去掉了布局的概念，直接用变量之间的相对关系完成位置的计算

3）开发环境

&ensp; ①系统：MacOS X

&ensp; ②开发工具：Xcode

&ensp; ③开发语言：ObjectC

&ensp; ④安装文件：.ipa文件/.app文件

4）注意：使用Appium测试ios应用需要使用macOS操作系统

7.元素定位

1）元素定位，实际上就是定位控件

2）要想一个脚本同时支持android/ios两个系统，就得保证元素属性（id，aid，xpath等）一致

## （二）dom结构解读
1.dom：Document Object Model 文档对象模型

1）dom应用：最早应用于html和js 的交互。用于表示界面的控件层级，界面的结构化描述，常见的格式为html、xml。核心元素为节点和属性。

2）xpath：xml路径语言，用于xml中的节点定位

3）Android应用的层级结构与html不一样，是一个定制的xml

4）app source 类似于dom，表示app的层级，代表了界面里面所有的控件树的结构。

5）每个控件都有它的属性（resourceid，xpath，aid），没有css属性

6）node

7）attribute：

&ensp; ① clickable

&ensp; ② content-desc

&ensp; ③ resource-id

&ensp; ④ text

&ensp; ⑤ bounds

8）ios与Android 的区别

&ensp; ① dom属性和节点结构类型

&ensp; ② 名字和属性的命名不同（比如：android resourceid，ios name，android content-desc,ios accessibility-id）

## （三）id、aid、xpath定位方法

1.测试步骤三要素：定位、交互、断言

2.定位方法：

1）id定位：

&ensp; ① driver.find_element_by_id(resource-id属性值)

&ensp; ② driver.find_element(MobileBy.ID,"resource-id")

2）accessibility_id定位

&ensp; ① driver.find_element_by_accessibility_id(content-desc属性值)

&ensp; ② driver.find_element(MobileBy.ACCESSIBILITY_ID,"content-desc:属性")

3）xpath定位

&ensp; ① driver.find_element_by_xpath(xpath属性值)

4）classname定位（不推荐）

3.http://www.freeformatter.com/xpath-tester.html#ad-output格式化xml

## （四）uiautomatorviewer定位工具使用

1.uiautomatorviewer工具（only android）（推荐使用，sdk路径下的工具）

windows环境的话找到C:\Users\Administrator\AppData\Local\Android\android-sdk\tools路径下，直接点击 uiautomatorviewer.bat 进行启动


2.Appium inspector 工具
