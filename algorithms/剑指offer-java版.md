# 剑指Offer Java版 题解

[面试题2-Singleton单例模式](https://github.com/zeelam/blog/blob/master/algorithms/%E5%89%91%E6%8C%87offer-java%E7%89%88.md#%E9%9D%A2%E8%AF%95%E9%A2%982-singleton-%E5%8D%95%E4%BE%8B%E6%A8%A1%E5%BC%8F)

[面试题3-数组中重复的数字](https://github.com/zeelam/blog/blob/master/algorithms/%E5%89%91%E6%8C%87offer-java%E7%89%88.md#%E9%9D%A2%E8%AF%95%E9%A2%983-%E6%95%B0%E7%BB%84%E4%B8%AD%E9%87%8D%E5%A4%8D%E7%9A%84%E6%95%B0%E5%AD%97)

## 面试题2-Singleton 单例模式

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



## 面试题3-数组中重复的数字

> 题目一：找出数组中重复的数字
>
> 在一个长度为n的数组里的所有数字都在0~n-1的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中**任意一个**重复的数字。例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是重复的数字2或者3

```java
public class Solution {
    
    public boolean duplicate(int[] nums,int duplication){
        // 判断数组不为空，并且长度 > 1
        if(nums == null || nums.length <= 1){
            return false;
        }
        // 从数组下标为0遍历到下标为n-1,将当前i下标的数字放到该数字为下标的位置上，如果出现重复，则该数为重复的数，并且为该数组中有重复的数，返回true，如果便利到最后没有，则返回false
        for (int i = 0, i < nums.length; i++){
            while(nums[i] != i){
                if (nums[i] == nums[nums[i]]){
                    duplication = nums[i];
                    return true;
                }
                swap(nums, i, nums[i]);
            }
        }
        return false;
    }
    
    /**
    * 交换
    */
    private void swap(int[] nums, int i, int j){
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
    
}
```

