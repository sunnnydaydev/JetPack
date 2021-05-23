

һ�����

ORM�������ϵӳ�䣨Object Relational Mapping��

ORM������������ʹ�õı��������������������ԣ�ʹ�õ����ݿ��ǹ�ϵ�����ݿ⡣�������������Ժ������ϵ�͵����ݿ�֮�佨��ӳ���ϵ�������ORM��

����Room�ļܹ�

����Ҫ��Entity��Dao��Database��3������ɣ�ÿ�����ֶ�����ȷ��ְ��

1��Entity������ʵ���࣬ÿ��ʵ���඼�������ݿ�����һ�Ŷ�Ӧ�ı����ұ��е����Ǹ���ʵ�����е��ֶ��Զ����ɵġ�

```java
          @Entity
           data class User(var name: String, var sex: String, var age: Int) {

                @PrimaryKey(autoGenerate = true)
                 var id = 0L
           }

          ����ʾ����
          ��1��ʹ��Entity����ʵ����
          ��2�������������

 

 
```





   2��Dao�����ݷ��ʶ������˼������������ݿ�ĸ���������з�װ����ʵ�ʱ�̵�ʱ���߼���Ͳ���Ҫ�͵ײ����ݿ�򽻵��ˣ�ֱ�Ӻ�Dao����н������ɡ�

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

              @Query("select * from User where age > :age ") // ע�������:age �������ݿ��ѯ��������age
              fun queryUserOlderThan(age:Int):List<User>
        }
```

   3�� Database�����ڶ������ݿ��еĹؼ���Ϣ���������ݿ�İ汾�š�������Щʵ�����Լ��ṩDao��ķ���ʵ����

```java
       @Database(version = 1,entities = [User::class]) // ���ݿ�汾�������ı�
       abstract class AppDataBase : RoomDatabase() {

             abstract fun userDao(): UserDao // �ṩUser���ݿ�ķ��ʽӿڶ��������������Ҳ�������ⶨ��

             companion object { // ע�����ݿ����Ҫ�����ڵ���
                      private var instance: AppDataBase? = null

                     fun getDataBase(context:Context): AppDataBase {
                                   instance?.let {
                                   return it
                       }

                  return Room.databaseBuilder(context, AppDataBase::class.java,"app_database").build().apply { // apply ���÷�
                        instance = this
                       }
                 }
             }

         }
```



����ʹ��


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
https://developer.android.google.cn/training/data-storage/room �ο��ĵ�