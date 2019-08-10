## Android 控件架构

*ViewGroup* 与 *View*

viewGroup即父控件，可以包含多个View控件，并管理他们。

整体形成树形结构。

```
        ViewParant
           |  
        ViewGroup
           |
      ---------------
      |        |     |
   ViewGroup  View  View
      |
   -------
   |     |
 View    View
```

* Activity UI界面架构
```
Activity 
   -- PhoneWindow
     -- DecorView
        -- TitleView
        -- ContentView
```
  * 每个Activity都包含一个Window对象，通常就是PhoneWindow
  * phoneWindow将一个DecorView设置成根View
  * DecorView即使窗口界面的顶层视图，封装了一些窗口操作的通用方法。
    * WindowManagerService：所有View的监听事件，并通过Activity回调onClickListener
  * ContentView: 即通过Activity里面的setContentView()来设置一个layout文件
    * BTW，onCreate()中调用setContentView()后，WindowManagerService会回调onResume()。此时系统才会把整个DecorView添加到PhoneWindow里，并让其显示出来，最终完成界面的绘制。
  
*上述步骤的标准视图树*

```
        DecorView
           |  
        ViewGroup
        (Decor Parent)
           |
      ------------------
      |                |
   ActionBar         FrameLayout
   (container)        (content)
      |                |
   ActionBar         RelativeLayout
                      (activity_main.xml)
                       |
                     TextView
                     (HelloWorl)
```

## View的测量与绘制
* View的测量在onMeasure()中进行

## 事件拦截机制

### 触摸事件（Touch Event）
* MotionEvent类：触摸事件类
* Action： ACTION_DOWN, ACTION_UP, ACTION_MOVE （点击一个按钮，若不小心还滑动一点，都会触发这三个事件）
### 在View树里面的事件拦截
*事件处理过程*
![](https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/event_process.png)
* *事件向下传递*与*事件向上处理*过程
* 事件传递：默认false，向下传递；true，即拦截，直接交递自己的onTouchEvent处理
* 事件处理：默认false，给上级处理；true，自己处理，不用上级审核
