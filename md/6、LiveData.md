一 、简介

 1、类似于Rxjava 是一种响应式编程组件，可观察任何数据类型的数据，并在数据发生变化时通知给观察者。

 2、普通的观察者也可以观察数据，数据变化时通知观察者。LiveData有啥优势呢？LiveData的优势就是可以

感知安卓应用组件（四大组件）的生命周期。这样可确保LiveData只把更新的数据传给生命周期活跃（组件未被销毁）的组件。



 3、大部分情况都是LiveData结合ViewModel使用


二、简单练习 LiveData 观察ViewModel数据变化

1、ViewModel：


```java
class MainViewModel : ViewModel() {
var count = MutableLiveData<Int>()// 构造可传参默认值

fun plusOne() {
    val cou = count.value ?: 0
    count.value = cou + 1
}

fun clean() {
    count.value = 0
}
         }
```
2、MainActivity中


```java
   private fun initData() {
    val mainViewModel = ViewModelProvider(this).get(MainViewModel::class.java)
    Log.i(TAG, "mainViewModel.count:${mainViewModel.count}")

    binding.btnPlus.setOnClickListener {
        mainViewModel.plusOne()
    }
    binding.btnClean.setOnClickListener{
        mainViewModel.clean()
    }

    mainViewModel.count.observe(this@MainActivity, Observer {
        Log.i(TAG, "观察到数据变化:${it.toString()} ")
    })

}
```

总结：activity界面相关的数据处理逻辑可以放到VIewModel中处理，LiveData 可以结合ViewModel进行回调。这样Activity只负责界面的触发工作（如点击事件）然后通过LiveData回调数据更新显示即可。