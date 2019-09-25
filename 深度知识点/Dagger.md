## 依赖倒置原则
高层次的模块不应该依赖于低层次的模块，他们都应该依赖于抽象
MVP中，P属于高层次，V属于低层次，所以V需要实现接口，让P来依赖。

反例：如果P中拿到的是avitivity的对象，如果真调用的activity的方法，P和V就会产生很强的耦合，无法单纯使用junit进行单元测试。
另外，如果想将activity换成fragment或者view时，也需要大量的修改P

## 依赖注入
一般处理：
constructor里面new XXXX()，这个就是依赖具体实现

### setter 注入
使用fun setXXX(xxx)从外部进行set

### 构造器注入
```
constructor(xxx) {
   this.xxx = xxx
}
```

### 接口注入
创建一个接口，让高层去实现接口
```
// 接口
public interface InjectFinder {
    void injectFinder(MovieFinder finder);
}

// 实现接口
class MovieLister implements InjectFinder {
    ...
    public void injectFinder(MovieFinder finder) {
      this.finder = finder;
    }
    ...
}
```

### injector （注入器）
负责初始化依赖，并将依赖注入到上层模块中

### 总结
依赖注入降低了依赖和被依赖类型间的耦合，在修改被依赖时，不需要修改依赖类型的实现。同时，可以更方便使用mocking object替代原有的被依赖类型完成UT

---

*Dagger2是首个使用生成代码实现完整依赖注入的框架，极大减少了使用者的编码负担*

* 很好的资料： [使用Dagger 2进行依赖注入](http://codethink.me/2015/08/06/dependency-injection-with-dagger-2/)

简单的Dagger 2 DI实现
1. @Module 构建依赖
2. @Component 注入器，是依赖与被依赖的桥梁
3. 完成依赖注入，在mainActivity里实现@Inject之前定义的component
