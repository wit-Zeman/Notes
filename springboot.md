# 1、创建springboot项目

![image-20230320195739240](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320195739240.png)

**![image-20230320195806044](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320195806044.png)

## 可能遇到的错误

![image-20230320200716491](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320200716491.png)

## 创建一个controller

```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hell(){
        return "hello,springboot";
    }
}
```

## 启动springboot项目

![image-20230320200850545](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320200850545.png)

# 2、自定义端口号和banner

## 自定义端口

![](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320201024441.png)

![image-20230320201045423](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320201045423.png)

## 自定义banner

![image-20230320201353905](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320201353905.png)

![image-20230320201436939](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320201436939.png)

# 3、自动配置原理

- pom.xml 核心依赖在父工程中
- 启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

- 要使用什么功能，直接添加对应的启动器即可

结论: springboot所有自动配置都是在启动的时候扫描并加载:  所有的自动配置类都在这里面，但是不一定生效，要判断条件是否成立，只要导入了对应的start，就有对应的启动器了，有了启动器，我们自动装配就会生效，然后就配置成功!

1. springboot在启动的时候，从类路径下/META-INF/ spring.factories获取指定的值;
2. 将这些自动配置的类导入容器，自动配置就会生效，帮我进行自动配置!
3. 以前我们需要自动配置的东西，现在springboot帮我们做了!
4. 整合javaEE，解决方案和自动配置的东西都在spring-bootautoconfigure2.2.0.RELEASE.jar这个包下
5. 它会把所有需要导入的组件，以类名的方式返回，这些组件就会被添加到容器;
6. 容器中也会存在非常多的xxxAutoConfiguration的文件(@Bean)，就是这些类给容器中导入了这个场景的所有组件;并自动配置，@Configuration, JavaConfig !
7. 有了自动配置类，免去了我们手动编写配置文件的工作!

# 4、yaml语法详解

**YAML**（/ˈjæməl/，尾音类似*camel*骆驼）是一个可读性高，用来表达数据[序列化](https://baike.baidu.com/item/序列化?fromModule=lemma_inlink)的格式。*YAML*是"YAML Ain't a MarkuLanguage"（YAML不是一种[标记语言](https://baike.baidu.com/item/标记语言?fromModule=lemma_inlink)）的[递归缩写](https://baike.baidu.com/item/递归缩写?fromModule=lemma_inlink)。在开发的这种语言时，*YAML* 的意思其实是："Yet Another Markup Language"（仍是一种[标记语言](https://baike.baidu.com/item/标记语言?fromModule=lemma_inlink)，但为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。

# 5、给属性的几种赋值方式



- ## 通过注解实现赋值

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component  //@Component 将实体类注入为spring容器bean对象
public class Dog {
    //spring注解赋值
    @Value("旺财")
    private String name;
    @Value("3")
    private Integer age;
}
```

```java
@SpringBootTest
class SpringbootDemo01ApplicationTests {

    //spring 注解 实现自动装配
    @Autowired
    private Dog dog;

    @Test
    void contextLoads() {
        System.out.println(dog);
    }

}
```

- ## 通过yml文件赋值

  添加pom.xm   lombok依赖

  ```xml
          <!--Lombok引入-->
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
          </dependency>
  ```

  

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component  //@Component 将实体类注入为spring容器bean对象
@ConfigurationProperties(prefix = "person")
//使用yaml赋值 必须使用该注解 将yaml中的所有属性与类进行绑定
public class Person {
    private String name;
    private Integer age;
    private Date birth;
    private Map<String,Object> map;
    private List<Object> list;
    private Dog dog;
}
```

```yaml
#给实体类赋值
person:
  name: magic
  age: 22
  birth: 2023/03/20
  map: {k1: v1,k2: v2}
  list: [a,b,c]
  dog:
    name: 旺财
    age: 3
```

# 6、JSR303校验(判断输入格式是否合法)

添加pom.xml依赖

```xml
        <!--引入validation的场景启动器-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
```



![image-20230320213818785](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320213818785.png)

![image-20230320213826572](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320213826572.png)

![image-20230320214737673](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320214737673.png)

![image-20230320214949952](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230320214949952.png)

# 7、多环境配置及配置文件

![image-20230321152300353](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230321152300353.png)

# 8、springboot Web开发

## 1.使用thymeleaf模板引擎

- 引入pom依赖

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
```

- 在templates目录下创建一个HTML文件
- 注意：使用thymeleaf要添加  `<html lang="en" xmlns:th="http://www.thymeleaf.org">`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>test</title>
</head>
<body>
<div th:text="${msg}"></div>
</body>
</html>
```

- 编写一个controller并跳转到该文件

```java
@Controller
public class IndexController {
    @RequestMapping("/test")
    public String index(Model model){
        model.addAttribute("msg","hello,springboot");
        return "test";
    }
}
```

# 9、扩展springMVC

![image-20230321171945899](C:\Users\xzhan\AppData\Roaming\Typora\typora-user-images\image-20230321171945899.png)

```java
@Configuration
public class MVCConfig implements WebMvcConfigurer {
    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        WebMvcConfigurer.super.addViewControllers(registry);
    }
}
```

