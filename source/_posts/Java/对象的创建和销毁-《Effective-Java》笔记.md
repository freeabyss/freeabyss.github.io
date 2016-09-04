---
title: 对象的创建和销毁-《Effective Java》笔记
date: 2016-08-18 18:18:03
tags: [Java, Effective, note]
categories: Java
---

## 使用静态方法代替构造器
> * 静态方法有名称，便于理解
> * 静态方法可以返回已存在的对象，避免创建不必要的重复对象
> * 静态方法可以返回原返回类型的任何子类型，增加灵活性
> * 在创建参数化类型实例的时候，使代码更加简洁

## 存在多个构造器参数时考虑使用构造器
> * 易于阅读
> * 加强参数的约束条件，一旦有一个参数违反约束条件就创建不成功
> * 可以非常灵活的增加参数数量
> * Builder模式适用于有多个参数构造时使用，一般是4个或多个。
> * 通常最好一开始就使用Builder模式

以下是使用构造器的示例

```java
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        private final int servingSize;
        private final int servings;

        /**
         * 带默认值的
         */
        private int calories = 0;
        private int fat = 0;
        private int sodium = 0;
        private int carbohydrate = 0;

        public Builder(int servingSize, int servings) {
            this.servings = servings;
            this.servingSize = servingSize;
        }

        public Builder calories(int val) {
            calories=val;
            return this;
        }

        public Builder fat(int val) {
            fat = val;
            return this;
        }

        public Builder carbohydrate(int val) {
            carbohydrate = val;
            return this;
        }

        public Builder sodium(int val) {
            sodium = val;
            return this;
        }
        public  NutritionFacts build() {
            return new NutritionFacts(this);
        }

    }

    private NutritionFacts(Builder builder) {
        servings = builder.servings;
        servingSize = builder.servingSize;
        calories = builder.calories;
        fat = builder.fat;
        carbohydrate = builder.carbohydrate;
        sodium = builder.sodium;
    }
    public static void main(String[] args) {
        NutritionFacts nutritionFacts = new NutritionFacts.Builder(20, 20)
                .calories(10).carbohydrate(12).build();
    }
}
```

## 使用枚举类型实现单例模式
> 单元素的枚举类型是实现单例模式的最佳方法 ，详情可参考[设计模式之单例模式](http://blog.csdn.net/abyss521/article/details/52232409)

## 对于不想被实例化的类添加私有构造器
> 例如`java.lang.Math`这种的工具类，不希望被实例化，最好添加私有构造器避免被实例化

## 避免创建不必要的对象
> 尤其是要避免在大规模应用场景中使用字符串连接符`+`连接字符串，以及对包装类`Integer`、`Long`等类型使用运算符。 

## 避免使用finalize
> * `finalize()`不能保证被及时地执行，甚至根本不保证它们会执行
> * 在`finalize()`中创建和销毁对象对性能损耗非常大
> * 在`finalize()` 中抛出的异常会被忽略，使对象处于破坏状态
> * 假如需要释放资源，推荐使用`try-finally` 