一、ViewModel的作用：
1、可以帮助Activity分担一部分工作，用于存放与界面相关的数据的，只要是界面上能看得到的数据，它的相关变量都应该存放在ViewModel中，而不是Activity中，这样可以在一定程度上减少Activity中的逻辑。


2、可以保证在手机屏幕发生旋转的时候不会被重新创建，只有当Activity退出的时候才会跟着Activity一起销毁。这样即使旋转手机屏幕，界面上显示的数据也不会丢失。



二、基本使用

1、依赖库  


```java
     def lifecycle_version = "2.3.1"
 // ViewModel 库
implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycle_version"
// LiveData  库
implementation "androidx.lifecycle:lifecycle-livedata-ktx:$lifecycle_version"
// Lifecycles only (without ViewModel or LiveData)
implementation "androidx.lifecycle:lifecycle-runtime-ktx:$lifecycle_version"
// Saved state module for ViewModel
implementation "androidx.lifecycle:lifecycle-viewmodel-savedstate:$lifecycle_version"
// alternately - if using Java8, use the following instead of lifecycle-compiler
implementation "androidx.lifecycle:lifecycle-common-java8:$lifecycle_version" // 注解处理
```

2、ViewModel类定义


```java
     class MainViewModel : ViewModel() {
       var count = 1 
      }
```

3、Activity 中获取

```java
     val mainViewModel = ViewModelProvider(this).get(MainViewModel::class.java)
        Log.i(TAG, "mainViewModel.count:${mainViewModel.count}")
```





三、小结：

这里先接触下库的引入、简单定义书写。其实没啥卵用。熟悉下。后续结合livedata 来练习。