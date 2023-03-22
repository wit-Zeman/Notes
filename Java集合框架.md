# 1、为什么要学习Java中的集合框架？

## 集合概念：存放多个元素内容

## 框架：底层封装好 提供简单 a pi  给开发人员使用

##  集合提供一种存储空间可动态存放数据  

# ![image-20230223141025610](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230223141025610.png)

## 单列------一行就只有一列元素

## 多列------一行就两列元素  key  value 

![image-20230223142504911](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230223142504911.png)

# 2、Array List集合与常用方法

```java
public static void main(String[] args) {
        /**
         * new ArrayList<泛型> 必须 引用类型
         * 在集合中 使用<泛型> 必须使用 引用类型  若要使用基本数据类型 则使用它的包装类
         */
        List<String> arrayList = new ArrayList<String>();
        //add()方法 向arrayList中添加数据元素
        arrayList.add("student1");
        arrayList.add("student2");
        arrayList.add("student3");
        arrayList.add("student4");
        arrayList.add("student5");
        //arrayList.size()查看当前集合容量空间
        System.out.println("集合空间大小为：" + arrayList.size());
        //修改元素
        String before = arrayList.set(0, "teacher");//arrayList.set() 返回修改之前的元素值
        System.out.println("修改之前的元素为：" + before);
        //删除元素  同数组删除
        String old = arrayList.remove(0);//返回删除的元素
        System.out.println("删除的元素为：" + old);
        //按index查找arrayList.get(i)
        for (int i = 0; i < arrayList.size(); i++) {
            System.out.println("集合中第" + (i + 1) + "个元素是" + arrayList.get(i));
        }
    }
```

# 3、使用Array List集合存入学生对象（静态）

```java
    public static void main(String[] args) {
        List<Student> students = new ArrayList<Student>();
        students.add(new Student("magic01",11));
        students.add(new Student("magic02",12));
        students.add(new Student("magic03",13));
        students.add(new Student("magic04",14));
        students.add(new Student("magic05",15));
        System.out.println("添加学生对象成功!");
        System.out.println("开始输出学生对象：");
        for (int i = 0;i<students.size();i++){
            System.out.println(students.get(i));
        }
    }
```

![image-20230223151926259](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230223151926259.png)

#  4、使用Array List集合存入学生对象（动态）

```java
public static void main(String[] args) {

    List<Student> students = new ArrayList<Student>();
    //动态录入5位学生信息
    for (int i = 1; i <= 5; i++) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入第" + i + "位学生的名称：");
        String name = sc.nextLine();
        System.out.println("请输入" + i + "位学生的年龄：");
        int age = sc.nextInt();
        students.add(new Student(name, age));
        System.out.println("-----------------");
    }
    System.out.println("录入成功，开始查询");
    for (int j = 0; j < students.size(); j++) {
        Student student = students.get(j);
        System.out.println("姓名:" + student.getName() + "年龄:" + student.getAge());
    }
}
```

# 5、迭代器iterator

```java
public static void main(String[] args) {
    List<String> arrayList = new ArrayList<String>();
    arrayList.add("magic01");
    arrayList.add("magic02");
    arrayList.add("magic03");
    //获取迭代器对象
    Iterator<String> iterator = arrayList.iterator();
    //调用iterator.next()方法 输出元素 每调用一次 next() 就会输出集合中的第一个元素
    System.out.println(iterator.next());
    System.out.println(iterator.next());
    System.out.println(iterator.next());
}
```

# 6、has next（）方法

```java
public static void main(String[] args) {
    List<String> arrayList = new ArrayList<String>();
    arrayList.add("magic01");
    arrayList.add("magic02");
    arrayList.add("magic03");
    Iterator<String> iterator = arrayList.iterator();
    //当数据量很大时 可采用while循环 + iterator.hasNext()返回Boolean类型 判断
    while (iterator.hasNext()) {
        System.out.println(iterator.next());
    }
}
```

# 7、List集合中独有的 方法

  ![image-20230224133337706](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224133337706.png)

![image-20230224133534114](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224133534114.png)

# 8、增强for循环

基本语法	

​	for （元素类型 元素名（自己取的变量名）：集合名或数组名）{

​			使用变量名称访问集合

}

```java
public static void main(String[] args) {
    int[] arrInt = {10, 20, 30};
    System.out.println("使用增强for循环遍历数组");
    for (int arr : arrInt) {
        System.out.println(arr);
    }

    List<String> arrayList = new ArrayList<>();
    arrayList.add("magic01");
    arrayList.add("magic02");
    arrayList.add("magic03");
    System.out.println("使用增强for循环便利集合");
    for (String list : arrayList) {
        System.out.println(list);
    }

    Iterator<String> iterator = arrayList.iterator();
    System.out.println("使用迭代器遍历集合");
    while (iterator.hasNext()){
        System.out.println(iterator.next());
    }
}
```

# 9、泛型

 ![image-20230224142710031](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224142710031.png)

![image-20230224153534098](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224153534098.png)

```java
public class FanXing<T> {
    //定义泛型
    private T t;
    //定义泛型方法
    public<T> T show(T t){
        return t;
    }
}

    public static void main(String[] args) {
        FanXing<String> fanXing = new FanXing<>();
        String s = fanXing.show("magic");
        System.out.println(s);
        FanXing<Integer> integerFanXing = new FanXing<>();
        Integer integer = integerFanXing.show(69);
        System.out.println(integer);
    }
```

![image-20230224161536445](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224161536445.png)

# 10、Map集合

![image-20230224192502641](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224192502641.png)

![image-20230224193111615](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224193111615.png)

![image-20230224193837346](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230224193837346.png)

```java
public static void main(String[] args) {
    Map<String, String> map = new HashMap<>();
    map.put("001","magic01");
    map.put("002","magic02");
    map.put("003","magic03");
    System.out.println("before");
    System.out.println(map);

    String s = map.get("002");
    System.out.println(s);

    map.remove("003");
    System.out.println("after");
    System.out.println(map);

    System.out.println(map.isEmpty());

    System.out.println("clear-after");
    map.clear();
    System.out.println(map);
}
```

# 11、hash Set

```java
public static void main(String[] args) {
    //set接口 底层基于hashmap 单列 随机存储 不可重复(采用hashmap key 存储)
    Set<String> set = new HashSet<>();
    set.add("magic01");
    set.add("magic02");
    set.add("magic03");

    Iterator<String> iterator = set.iterator();
    while (iterator.hasNext()) {
        System.out.println(iterator.next());
    }
}
```

# 12、hash Set不重复存储

## 要想实现不重复存储 则要在存储的类中 重写 equals方法和hash Code方法

```java
public static void main(String[] args) {
    //采用hashSet存储学生对象 保证不重复
    /**
     * ((k = p.key) == key || (key != null && key.equals(k)))) 当未重写Students中的equals方法时
     * (k = p.key) == key比较内存地址 s1==s2  false s1.equals(s2)也比较内存地址false
     * 认为两个对象内存地址不一样 这时存入就会导致重复
     * */
    HashSet<Student> students = new HashSet<>();
    Student s1 = new Student("001", "magic");
    Student s2 = new Student("001", "magic");
    students.add(s1);
    students.add(s2);
    System.out.println(students);
}
```

```java
@Override
public boolean equals(Object o) {
    /**
 	1.先比较二者内存地址是否一样 若一样 表明二者相同				compare内存地址      
    2.当二者内存地址不一样时 就比较二者类型是否一致				compare类型
    3.当1 2 符合时 最后比较属性是否一致 						  compare属性
    */
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Student student = (Student) o;
    return Objects.equals(number, student.number) &&
            Objects.equals(name, student.name);
}

@Override
public int hashCode() {
    return Objects.hash(number, name);
}
```

# 13、![image-20230225170105022](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230225170105022.png)

```java
public static void main(String[] args) {
    HashMap<String, String> map = new HashMap<>();
    map.put("key1","value1");
    map.put("key2","value2");
    map.put("key3","value3");
    System.out.println(map);

    //1.map.get()根据key 获取value
    String key1 = map.get("key1");
    System.out.println(key1);
    //2.获取所有key的集合(返回set集合  为什么是set集合呢? 由于key是唯一的且set也保证了唯一存储)
    Set<String> keys = map.keySet();
    Iterator<String> iterator = keys.iterator();
    while (iterator.hasNext()){
        System.out.println(iterator.next());
    }
    //3.获取所有value的集合
    Collection<String> values = map.values();
    for (String value:values
    ) {
        System.out.println(value);
    }
    //4.获取所有键值对的的集合
    //hashMap键值对底层如何封装? 通过Map接口中的entry对象
    Set<Map.Entry<String, String>> entries = map.entrySet();
    for (Map.Entry<String, String> entry:entries
         ) {
        System.out.println(entry);
    }
    //5.获取存在相应key对应的value
    String orDefault = map.getOrDefault("key1", "default");
    System.out.println(orDefault);

    String orDefault4 = map.getOrDefault("key4", "default");
    System.out.println(orDefault4);
}
```

# 14、如何手写hash Map集合

![image-20230225174414528](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230225174414528.png)

```java
//定义泛型
public class MyHashMap<K, V> {

    //利用ArrayList实现手写hashMap
    List<Entry<K, V>> arrayListHashMap = new ArrayList<Entry<K, V>>();//注意小括号别丢

    //创建Entry容器 封装hashmap的键值对
    class Entry<K, V> {

        K k;
        V v;

        public Entry(K k, V v) {
            this.k = k;
            this.v = v;
        }
    }

    public void put(K k, V v) {
        //hashMap put方法 调用ArrayList add方法 传入新的entry对象
        arrayListHashMap.add(new Entry<K, V>(k, v));
    }

    public V get(K k) {
        //循环遍历ArrayList中的集合元素，集合中元素的k 与 传进来的参数k 相等 就返回对应的 v 若不存在k 则返回null
        for (Entry<K, V> entry : arrayListHashMap
        ) {
            if (entry.k.equals(k)) {
                return entry.v;
            }
        }
        return null;
    }
}
```



```java
public static void main(String[] args) {
    //泛型类 new的时候 不加<>
    MyHashMap myHashMap = new MyHashMap();
    myHashMap.put("key", "Value");
    System.out.println(myHashMap.get("key"));
}
```

# 15、Hash Map 常见的面试题（hash Map集合底层实现原       理）

1. ## Hash Map key 是否可以是为	我们自定义对象？ 肯定可以

2. ## Hash Map存储数据 有序还是无序？ 无序 ———底层采用散列存储

3. ## Hash Map key 是否可以是为 null       可以  存放在数组中的index[0]

4. ## Hash Map 中的键值对是如何封装的呢？ 通过entry对象  



![image-20230225212746490](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230225212746490.png)

# 16、![image-20230225215034198](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230225215034198.png)

![image-20230225224018039](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230225224018039.png)

# 17、

- ##  Hash Map  （无序） 

- ## Linked Hash Map （有序）  对Hash Map   改进

- ## Hash Set（无序） 底层基于 Hash Map   

- ## Linked Hash Set  （有序）底层基于 Linked Hash Map  



# 18、Hash Map和Hash table的区别

1. Hash Map是非线程安全的，Hash table是线程安全的
2. Hash Map允许null作为键或值，Hash table不允许,运行时会报NullPointerException
3. Hash Map添加元素使用的是自定义hash算法，Hash table使用的是key的hash Code
4. Hash Map在数组+链表的结构中引入了红黑树，Hash table没有
5. Hash Map初始容量为16，Hash table初始容量为11     -----> 初始容量不同