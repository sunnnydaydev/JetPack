

一、简介

ORM：对象关系映射（Object Relational Mapping）

ORM的由来：我们使用的编程语言是面向对象编程语言，使用的数据库是关系型数据库。将面向对象的语言和面向关系型的数据库之间建立映射关系，这就是ORM。

二、Room的架构

它主要由Entity、Dao和Database这3部分组成，每个部分都有明确的职责。

1、Entity：定义实体类，每个实体类都会在数据库中有一张对应的表，并且表中的列是根据实体类中的字段自动生成的。

```java
          @Entity
           data class User(var name: String, var sex: String, var age: Int) {

                @PrimaryKey(autoGenerate = true)
                 var id = 0L
           }

          如上示例：
          （1）使用Entity标明实体类
          （2）添加自增主键

 

 
```





   2、Dao：数据访问对象的意思。在这里对数据库的各项操作进行封装，在实际编程的时候，逻辑层就不需要和底层数据库打交道了，直接和Dao层进行交互即可。

```java
       @Dao
          interface UserDao {

               @Insert
                fun insertUser(user: User): Long

               @Update
               fun updateUser(newUser: User)

               @Query("select * from User")
               fun queryAllUsers():List<User>

               @Delete
               fun deleteAllUser(user: User)

              @Query("select * from User where age > :age ") // 注意这里的:age 代表数据库查询结果对象的age
              fun queryUserOlderThan(age:Int):List<User>
        }
```

   3、 Database：用于定义数据库中的关键信息，包括数据库的版本号、包含哪些实体类以及提供Dao层的访问实例。

```java
       @Database(version = 1,entities = [User::class]) // 数据库版本、包含的表
       abstract class AppDataBase : RoomDatabase() {

             abstract fun userDao(): UserDao // 提供User数据库的访问接口对象，如果有其他表也可以在这定义

             companion object { // 注意数据库对象要进程内单例
                      private var instance: AppDataBase? = null

                     fun getDataBase(context:Context): AppDataBase {
                                   instance?.let {
                                   return it
                       }

                  return Room.databaseBuilder(context, AppDataBase::class.java,"app_database").build().apply { // apply 的用法
                        instance = this
                       }
                 }
             }

         }
```



三、使用


```java
class RoomActivity : AppCompatActivity() {

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_room)

    Thread{
        val user = User("Tom","boy",18)
        val userDao = AppDataBase.getDataBase(applicationContext).userDao()
        userDao.insertUser(user)

        val userList = userDao.queryAllUsers()

        for (u:User in userList){
            println("userName:${u.name}")
            println("userSex:${u.sex}")
            println("userAge:${u.age}")
        }
    }.start()

}
  }

log:

//2021-04-27 15:54:33.662 4563-4652/com.example.jetpackcomponent I/System.out: userName:Tom

//2021-04-27 15:54:33.663 4563-4652/com.example.jetpackcomponent I/System.out: userSex:boy

//2021-04-27 15:54:33.663 4563-4652/com.example.jetpackcomponent I/System.out: userAge:18


```
https://developer.android.google.cn/training/data-storage/room 参考文档