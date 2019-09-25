1.standard

不管有没有已存在的实例，都生成新的实例，并且放于栈结构的顶部

2.singleTop

跳转时系统会先在栈结构中寻找是否有一个FirstActivity实例正位于*栈顶*，如果有则不再生成新的，而是直接使用
不位于栈顶的话 就重新生成

3.singleTask

跳转时系统会先在栈结构中寻找是否有一个FirstActivity实例
如果有，其上的实例都会被迫出栈
另原来的FirstActivity实例处于栈顶

4.singleInstance

*多个栈结构*
这种启动模式比较特殊，因为它会启用一个新的栈结构，将Acitvity放置于这个新的栈结构中，并保证不再有其他Activity实例进入。
