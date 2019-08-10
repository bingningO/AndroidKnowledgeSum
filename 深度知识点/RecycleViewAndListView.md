refer: [我们为什么要使用recylerView](http://zjutkz.net/2016/08/10/%E6%88%91%E4%BB%AC%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E4%BD%BF%E7%94%A8RecyclerView/)

> The RecyclerView widget is a more advanced and flexible version of ListView. This widget is a container for displaying large data sets that can be scrolled very efficiently by maintaining a limited number of views. Use the RecyclerView widget when you have data collections whose elements change at runtime based on user action or network events.

* advenced，更支持大数据量

* 回收机制：
  * ListView继承自AbsListView，就是滑出去的view就废弃，再需要的时候就添加
  * RecyclerView的回收器Recycler里，有很多缓存的list，在获取view的时候会先从这些缓存中查找
  * 结论：
  > 从这里我们可以看出，RecyclerView提供了比AbsListView更加完善的回收机制，配以细节的优化和postOnAnimation方法所保证的”Android 16ms”机制，RecyclerView在滑动性能上确实会比AbsListView更出色。
  
  > 但是虽然经过了优化，但是就像我前面说的RecyclerView并不是万能，对于一些非常复杂的item布局，一旦处理不好，RecyclerView所表现出来的性能也ListView是相差无几的
  
* 应该用哪个
  * RecyclerView虽然被标上了加强版AbsListView的标记，但是它们其实是两个不同的控件。
  * AbsListView的子类们有着完善的功能，如果你的滑动组件只想简单的使用滑动显示这个功能，并且想轻松的使用divider，header，footer或者点击事件这些功能，那么使用AbsListView是完全没有问题的。
  * RecycleView 更方便灵活（定制化），动画配以局部刷新，点击事件处理，天生支持嵌套滑动（可以很好的配合NestedScrollView或者CoordinatorLayout）
