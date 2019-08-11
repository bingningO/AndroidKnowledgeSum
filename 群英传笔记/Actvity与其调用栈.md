## Activity的生命周期与工作模式
### 各种状态的切换
* Active/Running
  * 此时Activity处于栈的最顶层，可见并可以交互。
  * onCreate()中创建基本的元素
  * onResume()中view添加到PhoneWindon里进行显示
* Paused
  * （部分）被挡住。失去交互。保留状态信息、成员变量。只有内存极低的情况下被回收掉。
  * onPause()释放系统资源，如camera、sensor、receiver
> ！！！所以receiver的申请与清除应该在onResuem()与onPause()里进行。
  
* Stopped
  * （全部）被另一个activity覆盖。不可见。保留状态信息、成员变量。
  * onStop()清除资源
  * 每当activity由可见到不可见，都会调用onStart()
>！！！ 但是onCreate()只是最开始调用，在这里进行UI初始化，可以提供UI利用率。防止一直被注销又创建。
* Killed
  * onDestroy()：销毁引用。 **但注意线程不会被清除，需要手动清除开启的线程**

*！！以下两张图结合理解*

![](https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/lifecycle2.png)

![](https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/lifecycle1.jpg)

*（补充）onSaveInstanceState(), onRestoreInstanceState()
  * 如果系统长期处于stoped()，且此时系统内存不够，就会回收activity
  * 这个过程系统会通过onSaveInstanceState()保存activity状态
  * 开发者也可以增加额外的键值存入Bundle保存其他状态
  * ！！！ 如果用户使用finish()方法就不会调用onSaveInstanceState()

```
  Resumed ---> （onSaveInstanceState()）---> Destroyed
  
  onCreated()
      |
  Created --->(onRestoreInstanceState())---> Resumed
```

## Activity调用栈管理
通过栈（Task）来管理各个activity
> 一个task中的activity可以来自不同的app，同一个app的activity也可能不在一个task中。
> !!!就是这里app的activity资源不是独立在各自的虚拟机中间的，是统一管理的哦～

### Launch Mode
* standard
  * 每次都会创建新的activity，插在栈顶
* singleTop
  * 意思：top一定是single的
  * 实际操作： 判断栈定，如果是需要的activity就直接引用。不是就新创建
  * 例子：QQ接收消息后弹出activity，如果当前activity在running状态（栈定），那就直接刷新使用咯～
* singleTask
  * 意思：整个栈该activity一定是single的（注意理解这个task就是栈的意思）
  * 实际操作： 如果存在该activity，则其上其他activity都销毁，使需要的activity在栈定
  * 例子：用来退出整个应用。主activity设置成singleTask。需要退出时跳转主activity（其上其他activity都会被清除），在主activity中重写onNewIntent(), 加上一句finish()，即可以结束掉该主activity从而安全退出应用。
* singleInstace
  * 该activity会存在新的任务栈中，且有且只有该activity
  * 例子：应用A创建一个activity，B应用想创建同样的activity时可以直接引用。常用在与程序分离的界面。如SetupWizard中调用紧急呼叫。
  
### 启动模式设置
1. 在Manifest里设置
2. 用IntentFlag
  * Intent.FLAG_ACTIVITY_NEW_TASK: 创建一个新的栈，并创建新的activity实例放在里面
  * Intent.FLAG_ACTIVITY_SINGLE_TOP： 即singleTop
  * Intent.FLAG_ACTIVITY_CLEAR_TOP： 即singleTask
  * Intent.FLAG_ACTIVITY_NO_HISTORY： activity不会保存在栈里（就是不留历史）
  > standard就是什么flag都不加哈～
  
### 清空任务栈
在AndroidManifest的<activity>里设置
* clearTaskOnLaunch: 每次调用该activity时，都讲其上的activity都清除（！！类似singleTask呀）
* finishOnTaskLaunch: finish掉自己。当离开所处Task再返回该activity时，会被finish掉（！！可以直接用来退出应用吧～）
* alwaysRetainTaskState: "免死金牌"，如果为true，将不接收任何clear命令。 

> 任务栈滥用很难调试，一定要根据实际需要小心使用。
