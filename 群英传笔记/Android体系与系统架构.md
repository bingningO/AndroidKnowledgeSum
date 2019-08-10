## Android系统架构

* 应用程序(Applications)
* 应用程序框架(Application Frameworks)
* 系统运行库与Android运行环境(Libraris & Android Runtime)
* Linux内核(Linux Kernel)

_安卓系统结构示意图_
![android structure](https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/android_structure.png)

_安卓架构总览_
![android framework](https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/android_framework.png)

### Dalvik
Dalvik包含了一整套Android的运行环境虚拟机，每个APP都会被分配并保持独立。

特点是运行时编译。

### ART (Android Runtime)
启用ART模式后，系统在安装应用的时候会进行一次**预编译**，在安装应用程序时会先将代码转换为机器语言存储在本地，这样运行程序时就不会每次都进行一次编译了，将提高执行效率。

## Android App组件架构

### 四大组件
1. Activity
   the pages for users, show the information and processing results.
   
2. BroadCastReceiver
   get broadcast information 
   
   !!  communication with Yeahka Apps

3. ContentProvider
   get information from other APP
   
4. Service 
   caculating, downloading, processing in the background.
   !! like some 3ed service 
   
* 信使： intent 
  to communicate, message, change datas between 组件
  
### 应用运行上下文
创建上下文时间点
1. 创建Application
2. 创建Activity
3. 创建Service

（这三个组件也继承自context）
