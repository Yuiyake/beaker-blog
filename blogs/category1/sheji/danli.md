---
title: sheji
date: 2021-05-14
categories: 
 - sheji
---
## 单例模式
 - 懒汉式（调用才实例）
   1. 步骤
     - 创建单例类，声明自己静态私有对象，创建私有构造方法和以自己为实例返回值的静态公有方法，工厂方法，里面是被动创建（if自己==null， 则create）
     - 客户端 将但李磊实例化，调用
     - 线程不安全，延迟初始化
   2. 代码(这是改进过的线程安全版)
     ```java
    public class Singleton {  
        private static Singleton instance;  
        private Singleton (){}  
        public static synchronized Singleton getInstance() {  
            if (instance == null) {  
                instance = new Singleton();  
            }  
            return instance;  
        }  
    }
    ```
 - 饿汉式（声明即实例）
   1. 步骤
    - 创建单例类，声明并创建自己的静态私有对象和私有构造方法，还有自己类型返回自己的静态公有方法，静态工厂方法
    - 客户端一样
   2. 代码
    ```java
   public class Singleton {  
        private static Singleton instance = new Singleton();  
        private Singleton (){}  
        public static Singleton getInstance() {  
            return instance;  
        }  
    }
    ```
  - 优缺点
    - 优 节约系统资源，允许可变数目的实例，提供了对唯一实例的受控访问
    - 缺 单例模式扩展会十分困难，违背单依职责原则