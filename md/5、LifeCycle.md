һ ���������� 


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
�����׶ˣ�

1��Activity���������ڻص��У�onCreate/onStop/onDestroy��������Ҫ����ܶ�������������·��ô�����������ά����

2���޷���֤������� Activity �� Fragment ֹ֮ͣǰ��������A��B��B��onStart���˺�ʱ������A��onStop���Ƚ�����

3�����ı׶ˣ���֪Activity���������ڲ������ӣ����������ڣ���һ��Activity��ȥ��֪�����������ڷǳ��򵥣�

�����Ҫ��һ����Activity������ȥ��֪Activity���������ڣ�Ӧ����ô���أ����ǻ���Ҫ��Activity����Щ�߼�����


lifeCycle���ƣ�
lifeCycle���ǽ����������ġ����������κ�һ���඼�����ɸ�֪��Activity���������ڣ�ͬʱ�ֲ���Ҫ��Activity�б�д�������߼�����

�����������ο�4��ViewModel.md��

 1��lifeCycle ����

 2��lifeCycle��ע�⴦������


������ʵ��

 1���Զ����������ڼ�����


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



   2��activity��ע���¼�����

```java
        lifecycle.addObserver(MyObserver())
```



�ġ�ע��㣺

1��lifeCycler��state ��Ӧ����activity���������ڻص�

2���°汾��׿project�� activityĬ��ʵ����lifecyclerOwner �ӿ�ʵ����getLifecycle���������ʵ����ΪComponentActivity��

Ҫ��ʵ���Զ����������ڼ������Զ���activityʵ������ӿڡ���ô���activityҲ��һ��lifecyclerOwner ��ʵ���ࡣ����ο��ٷ��ĵ���


