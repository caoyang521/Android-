# 《Android群英传》笔记
##Android体系与系统架构
##Android开发工具新接触
###Android studio
  - 1.IDE配置
  - 2.高级使用技巧
  - 3.ADB命令
  - 4.Genymotion
##Android控件结构与自定义控件详解
##ListView使用技巧
##Android Scroll分析
##Android绘图机制与处理技巧
##Android动画机制与使用技巧
##Activity与Activity调用栈分析
 - Activity是与用户交互的第一接口，它提供了一个用户完成指令的窗口。当开发者创建Activity之后，通过调用setContentView(View)方法来给该Activity指定一个显示的界面，并以此为基础提供给用户交互的接口。系统采用Activity栈的方式来管理Activity。
 - 生命周期
 - 启动与销毁过程
   - 在系统调用onCreate()之后，就会马上调用onStart(),然后继续调用onResume()以进入Resumed()状态，最后就会停在Resumed状态，完成启动.系统会调用onDestroy()来结束一个Activity的生命周期让它回到Killed状态。
   - onCreate()中：创建基本的UI元素
   - onPause()与onStop():清除Activity的资源，避免浪费
   - onDestroy()中：因为引用会在Activity销毁的时候销毁，而线程不会，所以清除开启的线程。
 - 暂停与恢复过程
   - 当栈顶的Activity部分不可见后，就会导致Activity进入Pause形态，此时就会调用onPause()方法，当结束阻塞后，就会调用onResume()方法来恢复到Resume状态。
 - 停止过程
   - 栈顶的Activity部分不可见时，实际上后续会有两种可能，从部分不可见到可见，也就是恢复过程；从部分不可见到完全不可见，也就是停止过程。系统在当前Activity不可见的时候，总会调用onPause()方法。
 - 重新创建过程
   - 如果你的系统长时间处于stopped形态而且此时系统需要更多内存或者系统内存极为紧张时，系统就会回收你的Activity，而此时系统为了补偿你，会将Activity状态通过onSaveInstanceState()方法保存到Bundle对象中，当然你也可以增加额外的键值对存入Bundle对象以保存这些状态。当你需要重新创建这些Activity的时候，保存的Bundle对象就会传递到Activity的onRestoreInstanceState()方法与onCreate()方法中，也就是onCreate()方法中参数——Bundle savedInsatnceState的来源。

###Android任务栈简介
- standard
  - 默认启动模式，每次都会创建新的实例。每次点击standard模式创建Activity后，都会创建新的MainActivity覆盖在原Activity上
- singleTop
  - 启动时，系统会判断当前栈顶Activity是不是要启动的Activity，是则直接引用这个Activity，不是则创建新的Activity。这种启动模式通常适用于接收到消息后显示的界面。例如QQ接收到消息后弹出的Activity，如果一次来10条消息，总不能一次弹出10个Activity。这种启动模式虽然不会创建新的实例，但是系统仍然会在Activity启动时调用onNewIntent()方法。
- singleTask
  - singleTask模式与singleTop模式类似，只不过singleTop是检测栈顶元素是否需要启动的Activity，而singleTask是检测整个Activity栈中是否存在当前需要启动的Activity。如果存在，则将该Activity置于栈顶，并将该Activity以上的Activity都销毁。这种启动模式通常可以用来退出整个应用：将主Activity设为singleTask模式，然后在要退出的Activity中转到主Activity，从而将主Activity之上的Activity都清除，然后重写主Activity的onNewIntent()方法，在方法中加上一个句finish(),将最后一个Activity结束掉。
- singleInstance
  - 与使用的浏览器工作原理类似，在多个程序中访问浏览器时，如果当前浏览器没有打开，则打开浏览器，否则会在当前打开的浏览器中访问。申明为singleInstance的Activity会出现在一个新的任务栈中，而且该任务栈中只存在这一个Activity。


###AndroidMainifest启动模式
###Intent Flag启动模式
###清空任务栈
###Activity任务栈使用
##Android系统信息与安全机制
##Android性能优化
##搭建云端服务器
##Android5.X新特性详解
##Android实例提高
###拼图游戏
###2048
