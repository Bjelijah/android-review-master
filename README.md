# Android

## 必问
### Q:kotlin相关：
### 委托原理
类委托：by
属性委托 by Delegate()

延迟变量 by lazy
可观察委托 obserable  vetoable
多个属性映射Map by map

类 委托对应java代理模式，委托类(代理类)持有真实类的对象，然后委托类（代理类）调用真实类的同名方法，最终真正实现的是方法的是真实类，这其实就是代理模式
属性委托 set/get
### 协程原理

### Q:Handler工作流程
A：1）创建Lopper，消息队列，handler对象 2）handler发送message到消息队列 3）Looper取出，分发给handler 4）handler 接受message，处理。1thread 1 lopper n个handler
### Q：Handler内存泄漏
A：Handler为匿名内部类，又将外部实例Activity传入，handler的message引用handler实例 handler引用Activity。message未处理未消耗掉GC无法回收Activity。
处理：Handler 1 静态内部类 2 activity结束时清空handler消息队列 removeCallbacksAndMessage
### Q：Handler线程 
A：主线程 创建lopper lopper死循环->MessageQueue的next最终native层挂起 会block,但是60帧 16.6ms会发送Sync同步信号，FrameDisplayEvenetReceiver会发送消息添加进来，事件也发消息给looper
系统阻塞和唤醒pipe
### Q：View绘制流程：
https://cloud.tencent.com/developer/article/1601353
A：View的绘制，有三个步骤：测量（measure），布局（layout），绘制（draw）, 从DecorView自上而下遍历整个View树，
Measure：测量视图大小。从顶层父View到子View递归调用measure方法，measure方法又回调OnMeasure。
Layout：确定View位置，进行页面布局。从顶层父View向子View的递归调用view.layout方法的过程，即父View根据上一步measure子View所得到的布局大小和布局参数，将子View放在合适的位置上。
Draw：绘制视图。ViewRoot创建一个Canvas对象，然后调用OnDraw()。六个步骤：①、绘制视图的背景；②、保存画布的图层（Layer）；③、绘制View的内容；④、绘制View子视图，如果没有就不用；⑤、还原图层（Layer）；⑥、绘制滚动条。
View 渲染
setView——> Handler->mTraversalRunnable-> performTraversals() -> measure –> layout –> draw ->
ViewRootImpl (measure,layout,draw)->drawSoftware-> canvas
### Q:MVVM,ViewModel LiveData LifeCycle 源码实现
https://github.com/xfhy/Android-Notes/tree/master/Blogs/Android/%E7%B3%BB%E7%BB%9F%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90
A：Model,View,ViewModel, Activity 继承LifeCycle ,Activity ViewModelProviders.of .get 创建ViewModel ViewModel new LiveData，Activity obser liveData，ViewModel postValue



