һ��ViewModel�����ã�
1�����԰���Activity�ֵ�һ���ֹ��������ڴ���������ص����ݵģ�ֻҪ�ǽ������ܿ��õ������ݣ�������ر�����Ӧ�ô����ViewModel�У�������Activity�У�����������һ���̶��ϼ���Activity�е��߼���


2�����Ա�֤���ֻ���Ļ������ת��ʱ�򲻻ᱻ���´�����ֻ�е�Activity�˳���ʱ��Ż����Activityһ�����١�������ʹ��ת�ֻ���Ļ����������ʾ������Ҳ���ᶪʧ��



��������ʹ��

1��������  


```java
     def lifecycle_version = "2.3.1"
 // ViewModel ��
implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$lifecycle_version"
// LiveData  ��
implementation "androidx.lifecycle:lifecycle-livedata-ktx:$lifecycle_version"
// Lifecycles only (without ViewModel or LiveData)
implementation "androidx.lifecycle:lifecycle-runtime-ktx:$lifecycle_version"
// Saved state module for ViewModel
implementation "androidx.lifecycle:lifecycle-viewmodel-savedstate:$lifecycle_version"
// alternately - if using Java8, use the following instead of lifecycle-compiler
implementation "androidx.lifecycle:lifecycle-common-java8:$lifecycle_version" // ע�⴦��
```

2��ViewModel�ඨ��


```java
     class MainViewModel : ViewModel() {
       var count = 1 
      }
```

3��Activity �л�ȡ

```java
     val mainViewModel = ViewModelProvider(this).get(MainViewModel::class.java)
        Log.i(TAG, "mainViewModel.count:${mainViewModel.count}")
```





����С�᣺

�����ȽӴ��¿�����롢�򵥶�����д����ʵûɶ���á���Ϥ�¡��������livedata ����ϰ��