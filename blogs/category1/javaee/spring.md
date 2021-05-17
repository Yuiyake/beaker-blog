---
title: spring
date: 2021-05-14
categories: 
 - javaee
---
## spring
  ### 整体架构
<img :src="$withBase('/img/spring-1.jpg')" alt="foo"> 
---
  ### 核心容器
  Beans，创建和管理bean以及ioc，访问配置文件等
  * ioc：即控制反转。解释“构成应用程序主干并由springioc容器管理的对象成为bean。 bean是由springioc容器实例化，组装和管理的对象,他们是springioc容器的基础。
  * DI：即依赖注入（应用依赖于ioc容器，ioc容器把小的外部资源注入进应用依赖的某个对象。）
  * Core，核心工具类，是其它组件的基本核心，我们也可以自己使用。
  * Context，构建于core和beans模块基础之上，为spring核心提供扩展，它的关键是ApplicationContext接口，添加了bean的生命周期控制等功能。
  * Expression Language， 提供强大的表达式语言，用于在运行时查询和操纵对象。
---
### 依赖注入
- 定义 依赖注入
1. 构造方法注入
   * 优点
      - 脱离了ioc框架这个类仍然可以工作（POJO）
   * 缺点
      - 参数过多
      - 一旦是用构造函数注入，就无法是用默认构造函数（比如MVC框架的Controller类）
      - 有冗余方法并不需要依赖
   ``` java
        public class StupidStudent {
            private SmartStudent smartStudent;
            public StupidStudent(SmartStudent smartStudent) {
                this.smartStudent = smartStudent;
            }
            public doHomewrok() {
                smartStudent.doHomework();
                System.out.println("学渣抄作业");
            }
        }
        public class StudentTest {
            public static void main(String[] args) {
                SmartStudent smartStudent = new SmartStudent();
                StupidStudent stupidStudent = new StupidStudent(smartStudent);
                stupidStudent.doHomework();
            }
        } 
   ```
   
2. setter方法注入
   * 优点
      - 在对象的生命周期内，可以动态改变依赖，灵活。
   * 缺点
      - 不直观
   ```java
     public class StupidStudent {
         private SmartStudent smartStudent;
         //添加setter方法
         public void setSmartStudent(SmartStudent smartStudent) {
            this.smartStudent = smartStudent;
         }
         public doHomewrok() {
             smartStudent.doHomework();
             System.out.println("学渣抄作业");
         }
     }
    public class StudentTest {
        public static void main(String[] args) {
            SmartStudent smartStudent = new SmartStudent();
            StupidStudent stupidStudent = new StupidStudent();
            stupidStudent.setSmartStudent(smartStudent);
            stupidStudent.doHomework();
            }
    }
   ```
   
3. 接口注入
   * 优点
      - 灵活
   * 缺点
      - 参数过多
      - 新加入依赖时会破坏原有方法名
    ```java
      public class MovieRecommender {
           private MovieCatalog movieCatalog;
           private CustomerPreferenceDao customerPreferenceDao;
           @Autowired
           public void prepare(MovieCatalog movieCatalog,
           CustomerPreferenceDao customerPreferenceDao) {
               this.movieCatalog = movieCatalog;
               this.customerPreferenceDao = customerPreferenceDao;
           }
        // ...
        }
   
    ```

---
  ### 封装模块
 * jdbc，用jdbc数据访问进行封装类
 * orm，对象-关系映射api
 * oxm， 对object/xml映射实现抽象层
 * jms， messagingService制造和消费信息的特性
 * Transaction， 支持变成和声明性的事务管理
---
  ### AOP
 * aop核心，面向切面
 * aspects， 用AspectJ框架
 * instructment， 可以通过代理类在运行时修改的字节，从而改变一个类的功能，实现AOP
 * 三种织入方式
     1. 编译器织入  -- 要有特殊java编译器
     2. 类装载期织入  -- 要有特殊类装载器
     3. 动态代理织入  -- 在运行期间为目标添加通知生成子类
   tips：Spring AOP框架默认动态代理织入，而AspectJ采用编译器和类装载期织入
---
### ✨书本上的课后习题（个人觉得有意义/不会的）
1. 控制反转（IOC）和依赖注入（DI）是什么？优点？
    - ioc是一种设计思想，意味着将设计好的对象给容器控制，非直接由对象控制。
