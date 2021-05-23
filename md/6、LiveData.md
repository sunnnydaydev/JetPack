һ �����

 1��������Rxjava ��һ����Ӧʽ���������ɹ۲��κ��������͵����ݣ��������ݷ����仯ʱ֪ͨ���۲��ߡ�

 2����ͨ�Ĺ۲���Ҳ���Թ۲����ݣ����ݱ仯ʱ֪ͨ�۲��ߡ�LiveData��ɶ�����أ�LiveData�����ƾ��ǿ���

��֪��׿Ӧ��������Ĵ���������������ڡ�������ȷ��LiveDataֻ�Ѹ��µ����ݴ����������ڻ�Ծ�����δ�����٣��������



 3���󲿷��������LiveData���ViewModelʹ��


��������ϰ LiveData �۲�ViewModel���ݱ仯

1��ViewModel��


```java
class MainViewModel : ViewModel() {
var count = MutableLiveData<Int>()// ����ɴ���Ĭ��ֵ

fun plusOne() {
    val cou = count.value ?: 0
    count.value = cou + 1
}

fun clean() {
    count.value = 0
}
         }
```
2��MainActivity��


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
        Log.i(TAG, "�۲쵽���ݱ仯:${it.toString()} ")
    })

}
```

�ܽ᣺activity������ص����ݴ����߼����Էŵ�VIewModel�д���LiveData ���Խ��ViewModel���лص�������Activityֻ�������Ĵ��������������¼���Ȼ��ͨ��LiveData�ص����ݸ�����ʾ���ɡ�