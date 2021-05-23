直接参考文档即可：https://developer.android.google.cn/topic/libraries/view-binding

十分简单，`kotlin-android-extensions` 的替代方案。

activity的简单配置如下,fragment 的参考文档把：

1、build.gradle 文件（安卓studio3.6以上）

```java
 android {
...
buildFeatures {
    viewBinding true
}
```
}


2、activity中 配置


```java
 class MainActivity : AppCompatActivity() {
 
private lateinit var activityMainBinding: ActivityMainBinding // 根据布局文件名自动生成 驼峰式命名+Binding 形式类名
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    // 1、设置View
    activityMainBinding = ActivityMainBinding.inflate(layoutInflater)
    val view = activityMainBinding.root
    setContentView(view)
    initData()
}

private fun initData() {
    // 2、使用
    activityMainBinding.btnOpenDataStoreActivity.setOnClickListener {
        startActivity(Intent(this@MainActivity, DataStoreActivity::class.java))
    }
}
```
}


ps：如果您希望在生成绑定类时忽略某个布局文件，请将 tools:viewBindingIgnore="true" 属性添加到相应布局文件的根视图中