一 、例子引申 


```java
class MyLocationListener {
public MyLocationListener(Context context, Callback callback) {
    // ...
}

void start() {
    // connect to system location service
}

void stop() {
    // disconnect from system location service
 } 

}

class MyActivity extends AppCompatActivity {
private MyLocationListener myLocationListener;
@Override
public void onCreate(...) {
    myLocationListener = new MyLocationListener(this, (location) -> {
        // update UI
    });
}

@Override
public void onStart() {
    super.onStart();
    myLocationListener.start();
    // manage other components that need to respond
    // to the activity lifecycle
}

@Override
public void onStop() {
    super.onStop();
    myLocationListener.stop();
    // manage other components that need to respond
    // to the activity lifecycle
}
}
```
上述弊端：

1、Activity的生命周期回调中（onCreate/onStop/onDestroy）可能需要管理很多如上组件。导致放置大量代码难以维护。

2、无法保证组件会在 Activity 或 Fragment 停止之前启动。如A跳B，B的onStart做了耗时操作。A的onStop就先结束。

3、最大的弊端，感知Activity的生命周期并不复杂，但问题在于，在一个Activity中去感知它的生命周期非常简单，

而如果要在一个非Activity的类中去感知Activity的生命周期，应该怎么办呢？我们或许要在Activity中做些逻辑处理。


lifeCycle优势：
lifeCycle就是解决上述问题的。它可以让任何一个类都能轻松感知到Activity的生命周期，同时又不需要在Activity中编写大量的逻辑处理。

二、依赖（参看4、ViewModel.md）

 1、lifeCycle 依赖

 2、lifeCycle的注解处理依赖


三、简单实用

 1、自定义生命周期监听类


```java
      class MyObserver : LifecycleObserver {
companion object {
    const val TAG = "MyObserver"
}

@OnLifecycleEvent(Lifecycle.Event.ON_CREATE)
fun activityCreate() {
    Log.i(TAG, "onCreate")
}

@OnLifecycleEvent(Lifecycle.Event.ON_START)
fun activityStart() {
    Log.i(TAG, "onStart")
}

@OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
fun activityResume() {
    Log.i(TAG, "onResume")
}

@OnLifecycleEvent(Lifecycle.Event.ON_STOP)
fun activityStop() {
    Log.i(TAG, "onStop")
}

@OnLifecycleEvent(Lifecycle.Event.ON_DESTROY)
fun activityDestroy() {
    Log.i(TAG, "onDestroy")
}
        
}
```



   2、activity中注册下监听类

```java
        lifecycle.addObserver(MyObserver())
```



四、注意点：

1、lifeCycler的state 对应的有activity的生命周期回调

2、新版本安卓project中 activity默认实现了lifecyclerOwner 接口实现了getLifecycle方法。这个实现类为ComponentActivity。

要想实现自定义生命周期监测可以自定义activity实现这个接口。那么你的activity也是一个lifecyclerOwner 的实现类。具体参看官方文档。


