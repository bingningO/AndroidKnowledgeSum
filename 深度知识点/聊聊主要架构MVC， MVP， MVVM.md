
## 基本介绍
* MVC
<img src="https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/MVC.png" alt="drawing" width="400"/>

  * controller层去控制model的数据，并且返回给view做展示
	* 实践
		* view：.xml
		* model: java bean, repository 
		* controller: activity
	* 重大缺陷
		* view层仅为.xml，能做的事情太少了 
		* activity负责显示+逻辑控制controller，会比较庞大
		* ！！！view和model互相可知，存在耦合（开发、测试、维护都费时费力）
> MVC的缺点导致了MVP和MVVM的发展

* MVP
<img src="https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/MVP.png" alt="drawing" width="400"/>

  * presenter充当view和model的桥梁，实现解偶
	* 注意view和presenter的通信，通过接口实现。保证完全解偶和测试可行性。
	* ！！！最好fragment作为view层，activity用于创建view层和presenter的控制器（就有点像还是有controller的基础上，还增加了presenter）
	* 实践
		* model：和MVC一样，数据的定义获取
		* presenter：所有关于用户事件的转发
		*  view：.xml, activity, fragment
	* 缺点：
		* 若页面复杂，接口会有很多
		* 解决： 可以定义一些基类接口，把一些公共逻辑（如网络请求成功失败、toast等放进去）、再实际开发时添加新的接口、（另外接口要写好comment）
* MVVM
<img src="https://github.com/bingningO/AndroidKnowledgeSum/blob/master/images/MVVM.png" alt="drawing" width="400"/>
	
  * MVP的presenter换成了viewmodel
	* view和viewModel是相互绑定的关系，意味着当你更新viewmodel层的数据时，view层灰相应的变动ui
		* 实践：data binding, live data 
	* 问题：
		* data binding 解决了数据绑定的问题，但是view层还是会过重（如同MVC一样activity里需要实现对model的处理）

* 结合MVP+MVVM
	* google example: [GitHub - googlesamples/android-architecture: A collection of samples to discuss and showcase different architectural tools and patterns for Android apps.](https://github.com/googlesamples/android-architecture)
	* MVP+data binding :
		* 使用data binding框架去节省了类似findViewById和数据绑定的时间
		* 使用presenter去将业务逻辑和view层分离。
* 自定义更适合自己的框架
