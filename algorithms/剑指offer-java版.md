# 剑指Offer Java版 题解

[TOC]

## Singleton 单例模式

- 懒汉式

  ```java
  public class Singleton {
      private static Singleton instance;
      // 私有化构造器，防止外部调用
      private Singleton(){    
      }
      public static Singleton getInstance() {
          if (instance == null){
              instance = new Singleton();
          }
          return instance;
      }
  }
  ```
  **这种单例模式 在多线程的情况下，如果同时有多个线程判断 if(instance == null) 那就会有多个instance出现了**

- 线程安全的懒汉式

  ```java
  public class Singleton {
      private static Singleton instance;
      private Singleton(){
      }
      public static synchronized Singleton getInstance(){
          if (instance == null){
              instance = new Singleton();
          }
          return instance;
      }
  }
  ```

  **通过加锁的方式解决了多线程时出现instance的情况，但是并发很常见，所以这种方式效率很低**

- 饿汉式

  ```java
  public class Singleton {
      private static Singleton instance=new Singleton();
      private Singleton(){
      }
      public static Singleton getInstance(){
          return instance;
      }
  }
  ```

  **直接在运行这个类的时候就一次加载，然后常驻在内存中，但是这种方式没有做到lazy loading**

- 静态类内部加载

  ```java
  public class Singleton {
      private static class SingletonHolder {
          private static final Singleton INSTATCE = new Singleton();
      }
      private Singleton(){
      }
      public static final Singleton getInstance() {
          return SingletonHolder.INSTANCE;
      }
  }
  ```

  **这种方式外部是懒汉式，静态内部类是饿汉式，既解决了懒加载问题，又解决了多线程问题，但是依然可以通过反射创建多个instance**

- 枚举

  ```java
  public enum Singleton {
      INSTANCE;
      public void yourFunction(){
          //TODO: do something;
      }
  }
  ```

  使用时

  ```java
  Singleton.Instance.yourFunction();
  ```

  **《Effective Java》中的推荐写法，线程安全、提供了序列化机制、防止反射调用构造器**

通常情况下，其实用饿汉式就足够了，一般没有人加载了实例但是不调用方法闲的蛋疼的吧。