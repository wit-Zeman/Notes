#   JavaSE之常见API

## 1、什么是API

API:应用程序编程接口，复杂的类简单调用；jdk中提供的各种Java类，这些类将底层的实现封装起来，我们无需关心是如何实现的，只需要简单拿来使用;

### 例：new  Scanner();	new Random();

## 2、Scanner

```java
        //键盘录入Scanner
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个字符串：");
        String k = sc.next();
        System.out.println("您输入的字符串是：" + k);
```

## 3、Object类

<u>**Object类中有哪些方法呢？**</u>

1. 无参构造方法；
2. clone()；克隆方法，复制对象
3. equals()；比较两个对象是否相等
4. finalize();jvm垃圾回收
5. getclass()；获取该对象的class
6. hashCode()；hash地址
7. 多线程 notiy()；
8. tostring()；返回对象的字符串表达式

## 4、toString()方法      输出对象所有值

```java
public class Test02 {
    public static void main(String[] args) {
        Student st = new Student();
        st.setName("magic");
        st.setAge(18);
        System.out.println(st);
        System.out.println(st.getClass().getName()+"@"+Integer.toHexString(st.hashCode()));
        /*  输出结果 com.magic.days01.Student@4554617c 底层如何实现toString()?
        *   1.String s = String.valueOf(x);
        *   2.return (obj == null) ? "null" : obj.toString();
        *   3.return getClass().getName() + "@" + Integer.toHexString(hashCode());
        *
        * */

    }
}
```

## 5、String底层实现

```java
public class Test03 {
    public static void main(String[] args) {
        String str = "magic";
        System.out.println(str);

        char[] arr ={'m','a','g','i','c'};
        System.out.println(arr);
      
    }
}
```

## 6、登录验证（equals方法）

```java
public class Test04 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String name = scanner.next();
        System.out.println("请输入密码：");
        String password = scanner.next();
        System.out.println(login(name, password) ? "您输入的账号和密码正确" : "您输入的账号和密码不正确")；
    }

    static boolean login(String name, String pwd) {
        String userName = "admin";
        String userPwd = "123";
        return userName.equals(name) && userPwd.equals(pwd);
    }

}



```

## 7、登陆验证（三次机会）

```java
public class Test05 {
    //check login; three chances
    public static void main(String[] args) {
        int loginCount = 3;
        for (int i = 1; i <= 3; i++) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("请输入用户名：");
            String name = scanner.next();
            System.out.println("请输入密码：");
            String password = scanner.next();
            if (login(name, password)) {
                System.out.println("恭喜您，登陆成功！");
                return;
            } else {
                if (i == 3) {
                    System.out.println("对不起，您输入的账号和密码错误，账号被冻结！");
                    return;//return 退出循环
                }
                System.out.println("对不起，您输入的账号和密码错误，您还剩于" + (loginCount - i) + "次机会");
            }
        }

    }

    static boolean login(String name, String pwd) {
        String userName = "admin";
        String userPwd = "123";
        return userName.equals(name) && userPwd.equals(pwd);
    }


}
```

## 8、Object类中的equals（）方法

```java
    public static void main(String[] args) {
        Person p1 = new Person("magic",18);
        Person p2 = new Person("magic",18);
        System.out.println(p1==p2);//== 比较二者的内存地址 false
        System.out.println(p1.equals(p2));// 此时Person类中的equals方法未重写 比较的仍是二者的内存地址 false
    }
```

##  		9、重写object类equals（）

```java
    @Override
    public boolean equals(Object o) {
        //1.比较对象的内存地址是否相同
        if (this == o) return true;
        //2.传进来的参数是否为null 或者 对象的类型是否相同
        if (o == null || getClass() != o.getClass()) return false;
        //3.当二者内存地址不同但对象类型一致 则比较二者的属性是否相同
        Person person = (Person) o;
        return age == person.age && name == person.name;
    }


        Person p1 = new Person("magic",18);
        Person p2 = new Person("magic",18);
        System.out.println(p1==p2);//== 比较二者的内存地址 false
        /*
        * System.out.println(p1.equals(p2));
        * 此时Person类中的equals方法未重写 比较的仍是二者的内存地址 false
        * */
        //重写之后 true
        System.out.println(p1.equals(p2));
```

## 10、instanceof 判断对象是否可以强转

## jdk9

![image-20230216162621762](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230216162621762.png)

## jdk1.7之前

![image-20230216162659610](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230216162659610.png)

## jdk1.7开始

![image-20230216162915146](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230216162915146.png)

## 11、Math类

![image-20230216164103088](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230216164103088.png)

```java
public static void main(String[] args) {
        //Math类方法

        //返回绝对值
        System.out.println(Math.abs(-12));
        System.out.println("---------------");
        //返回一个大于或等于本身的整数 double类型
        System.out.println(Math.ceil(12.66));
        System.out.println(Math.ceil(12.00));
        System.out.println("---------------");
        //返回一个小于或等于本身的整数 double类型
        System.out.println(Math.floor(12.66));
        System.out.println(Math.ceil(12.00));
        System.out.println("---------------");
        //四舍五入
        System.out.println(Math.round(7.99));//8
        System.out.println(Math.round(7.49));//7
        System.out.println(Math.round(-6.33));//-6
        System.out.println("---------------");
        //max min
        System.out.println(Math.max(1,12));
        System.out.println(Math.min(1,-1));
        System.out.println("---------------");
        //a的b次幂
        System.out.println((int) (Math.pow(2,3)));
        System.out.println("---------------");
        //随机数 0.0~1.0
        System.out.println(Math.random());

    }
```



## 12、System类

![image-20230216165748540](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230216165748540.png)

```java3
        long start = System.currentTimeMillis();
        for (int i=1;i<=1000000;i++){
            System.out.println("Time");
        }
        long end = System.currentTimeMillis();
        System.out.println("花费时间为:"+(end-start)+"ms");
```

# 13、工具类的设计（思想）

1. 构造器私有化，无法new

2. 工具类方法 public static 直接通过类名访问

   # 14、基本数据类型

   - 整数类型 int byte short long

   - 浮点类型 float double

   - 字符类型 char

   - 布尔类型 boolean

     ### Integer类型   包装Int类型

     ![image-20230222185427555](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230222185427555.png)

   # 15、String类中的valueOf方法

   ```java
   public class Test02 {
       public static void main(String[] args) {
           //将int类型转换成string类型 String.valueOf(i)
           int i =30;
           String j = String.valueOf(i);
           System.out.println(j);
       }
   }
   ```

```java
    public static void main(String[] args) {
        //string类型转换成int类型
        String str ="1234";
        Integer.parseInt(str);
        System.out.println(str);
    }
```

# 16、Int与Integer区别

![image-20230222194636306](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230222194636306.png)

# 17、异常处理

## 1.try catch 用法          可叠加多个catch使用    有使用顺序

```java
public class Test05 {
    public static void main(String[] args) {
        //ArrayIndexOutOfBoundsException
        System.out.println("start");
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[3]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("数组下表越界！");
            e.printStackTrace();
        }
        System.out.println("end");
    }
}
```







## 2. EXception异常            	throw用法

![image-20230222205249298](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230222205249298.png)

```java
public static void main(String[] args) {
    System.out.println("start");
    try {
        test();
    }catch (ArrayIndexOutOfBoundsException e ){
        System.out.println("数组越界错误");
    }catch (Exception e){
        e.printStackTrace();
    }
    System.out.println("end");
}

public static void test() {
    int[] arr = {1, 2, 3};
    System.out.println(arr[2]);
    //NumberFormatException
    String str = "123fff";
    Integer.parseInt(str);

}
```

## 3、自定义异常（只需要继承Exception）

```java
public static void main(String[] args) throws loginException {
    Scanner sc = new Scanner(System.in);
    System.out.println("请输入用户名");
    String name = sc.next();
    System.out.println("请输入密码");
    String pwd = sc.next();
    login(name,pwd);
}

public static void login(String userName,String passWord) throws loginException {
    if (!("admin".equals(userName)&&"123".equals(passWord))){
        throw new loginException("用户名和密码错误！");
    }
    System.out.println("用户名和密码正确！");
}
```

```java
public class loginException extends Exception {
    //自定义异常 继承Exception 构造方法 super(message)
    public loginException(String message) {
        super(message);
    }
}
```
