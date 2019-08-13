## 布局优化
* 不卡的最佳fps大概在60fps、即所有逻辑要求在16ms内绘制完成
* android系统的Profile GPU Rendering : 检测绘制时间
* android系统的Enable GPU Overdraw: 检测绘图层次（是否有过度绘制）
* 优化布局
	* 减少view树
	* 尽量少用linearLayout， 使用relativeLayout
	* 避免嵌套无用布局
		* 使用include重用布局
		* 使用<ViewSub>延迟加载，需要的时候再加载
	        > GONE是先加载，然后再不显示布局
		* Hierarchy Viewer: 强大的分析优化布局的工具
		
## 内存优化
### 内存机制
安卓应用的沙箱机制，内存太低会被触发LMK（Low Memory Killer）
通常我们说的内存指的手机的RAM
* 寄存器（Register）：速度最快、程序无法控制
* Stack：存放基本类型的数据和对象的引用（注意不是对象本身）
* Heap：存放new的对象和数组。由java虚拟机的GC（Gabbage Collection）来管理
* Static Field（静态存储区）：管理特殊的数据变量，如static定义的
* Constant Pool（常量池）：储存常量
> !!! 注意栈是存放对象的引用，堆是对象本身。所以对象使用完毕也不会被释放是要等待GC来管理

### 内存优化实例
1. Bitmap优化： Bitmap是内存占用过高的最大威胁
	1. 使用合适图片
	2. 及时回收内存（bitmap.recycle()）
	3. 使用图片缓存
2. 代码优化

## 使用各种工具来分析、优化
* Lint
* Android Studio : Memory Monitor
* (Log) TraceView 优化APP性能
* MAT工具分析内存状况
