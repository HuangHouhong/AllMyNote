# 简介

LifeCycle 是一个可以感知宿主生命周期变化的组件。

常见的宿主包括 Activity/Fragment、Service 和 Application。

LifeCycle 会持有宿主的生命周期状态的信息，当宿主生命周期发生变化时，会通知监听宿主的观察者。

LifeCycle 的出现主要是为了解决系统组件的生命周期与普通组件之间的耦合性。

# 使用

该组件提供的两个接口：

- LifecycleOwner
- LifecycleObserver

被监听的系统组件需要去实现 LifecycleOwner 接口，观察者需要实现 LifecycleObserver 接口。

现在依赖基本上都已经集成到 android 源码中，所以不需要单独在build.gradle 中引入依赖。

## 1 实现观察者

观察者一般实现方式有两种

- LifecycleObserver

- LifecycleEventObserver

  前者一般需要配合注解使用，被注解的方法不能是private。
  
  后者是将事件封装成 Lifecycle.Event 事件。

```kotlin
class LifecycleListener : LifecycleObserver {

    @OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
    fun onResume() {
        HLog.i("onResume")
    }

    @OnLifecycleEvent(Lifecycle.Event.ON_PAUSE)
    fun onPause() {
        HLog.i("onPause")
    }
}
```

在观察者接口里面，使用注解对方法进行关联，当被监听的系统组件生命周期发生变化时，被标记过的方法便会被自动调用。

## 2 在Activity中引用

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        lifecycle.addObserver(LifecycleListener())
    }
}
```

如上所示，当 MainActivity#onResume 执行时，观察 LifecycleListener#onResume 方法被调用。

同理，可以被观察的组件也可以是Fragment，Service。