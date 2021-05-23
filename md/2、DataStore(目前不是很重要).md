

DataStore 提供两种不同的实现：

   Preferences DataStore:存基本数据类型

  Proto DataStore：可存自定义数据类型。


Preferences DataStore 使用键存储和访问数据。此实现不需要预定义的架构，也不确保类型安全。

Proto DataStore 将数据作为自定义数据类型的实例进行存储。此实现要求您使用协议缓冲区来定义架构，但可以确保类型安全。



依赖库：


    implementation "androidx.datastore:datastore-core:1.0.0-alpha08"//DataStore:Proto DataStore
    implementation "androidx.datastore:datastore-preferences-core:1.0.0-alpha08"//DataStore:preferences DataStore


参考：https://segmentfault.com/a/1190000038902771