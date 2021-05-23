ֱ�Ӳο��ĵ����ɣ�https://developer.android.google.cn/topic/libraries/view-binding

ʮ�ּ򵥣�`kotlin-android-extensions` �����������

activity�ļ���������,fragment �Ĳο��ĵ��ѣ�

1��build.gradle �ļ�����׿studio3.6���ϣ�

```java
 android {
...
buildFeatures {
    viewBinding true
}
```
}


2��activity�� ����


```java
 class MainActivity : AppCompatActivity() {
 
private lateinit var activityMainBinding: ActivityMainBinding // ���ݲ����ļ����Զ����� �շ�ʽ����+Binding ��ʽ����
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    // 1������View
    activityMainBinding = ActivityMainBinding.inflate(layoutInflater)
    val view = activityMainBinding.root
    setContentView(view)
    initData()
}

private fun initData() {
    // 2��ʹ��
    activityMainBinding.btnOpenDataStoreActivity.setOnClickListener {
        startActivity(Intent(this@MainActivity, DataStoreActivity::class.java))
    }
}
```
}


ps�������ϣ�������ɰ���ʱ����ĳ�������ļ����뽫 tools:viewBindingIgnore="true" ������ӵ���Ӧ�����ļ��ĸ���ͼ��