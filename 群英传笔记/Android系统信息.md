## Android 系统信息获取
安卓市场的多样性，导致配置各种各样（开发者太难了～）

“安兔兔”： 手机跑分软件，国外也很出名

### android.os.Build
包含了系统编译时的大量设备、配置信息。例如：
* 系统定制商： Build.BRAND
* 设备参数： Build.DEVICE
* Builder类型： Build.TYPE
* ...

### SystemProperty
包含许多系统配置属性值和参数，很多信息与上面通过android.os.Build获取的值时相同的 
* OS版本等： os.version
* Java Class 路径： java.class.path
* ...

> ADB shell命令里有两个非常强大的命令集，PM和AM
## Apk应用信息获取： PackageManager
管理所有已经安装的Apk，重点获取包信息。例如
* ActivityInfo
* ServiceInfo
* ApplicationInfo
* ...

## Apk应用信息获取： ActivityManager
相对于PackageManager有所侧重，重点获取正在运行的应用程序信息
* 内存信息： MemoryInfo
* 运行进程： RunnningAppProcessInfo
* 运行服务： RunningServiceInfo
