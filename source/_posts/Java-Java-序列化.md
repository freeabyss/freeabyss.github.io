---
title: Java 浅析序列化
date: 2017-03-18 14:44:26
tags: [Java,IO]
categories: [Java]
---
## 前言
本篇文章从以下几个方面，讲述Java序列化相关的内容： 
> * 什么是序列化？
> * 如何实现序列化？
> * 修改默认的序列化机制
> * 多个对象共享一个引用时，序列化和反序列化会有什么结果？
> * 如何解决兼容问题？
> * 序列化应用时需要注意的问题
> * 父类的序列化问题
> * 安全问题

## 什么是序列化
__序列化__是指将对象表示为一个字节序列的过程，该字节序列包含对象所存储的数据、数据的类型以及对象的类型信息。 __反序列化__是将字节序列转化为对象的过程。 
序列化是对对象的持久化，将对象序列化后可以存入文件中，也可以通过网络传递到远程服务器中。         
    
## 实现序列化
在实现序列化的过程中，需要用到三个类`ObjectInputStream`、`ObjectOutputStream`和`Serializable`。首先，让需要序列化的对象所属类实现`Serializable`接口，该接口不需要实现任何方法，是典型的标记接口。 然后使用`ObjectInputStream`、`ObjectOutputStream`进行读写。   

{% gist 3d8ae4af25273ee8fec1c10c5c0002a2 %}

当存储一个对象时，这个对象所属的类也必须存储，这个类的描述包含 

* 类名。
* 序列化的版本唯一的ID，它是通过对类、超类、接口、域类型和方法签名按照规范方式排序，然后应用SHA算法获得，并且只取前8位。它相当于一个类的指纹，假如类中存在`serialVersionUID`字段，则用它作为类的指纹。     
* 描述序列化方法的标志集。
* 对数据域的描述。  

     
静态变量和被`transient`修饰的变量将不会被序列化。除非超类也实现了`Serializable`接口，否则超类的数据域不会被序列化。   

## 修改默认的序列化机制
Java提供了三种方式，用以修改默认的序列化机制。   
考虑以下这种情况，某些数据域，例如只对本地方法有意义的存储文件句柄，这种信息在重新加载或传送到其他机器上时都是没有用处的，甚至会引起程序崩溃。因此为了防止这种情况，使用`transient`修饰符，被该修饰符修饰后的数据域将被序列化机制跳过。       
      
另外一种情况是，类中的某些数据域没有实现`Serializable`接口，却又要将其序列化，这时就需要先将其标记为`transient`避免抛出`NotSerializableException`，然后通过重写`readObject`和`writeObject`方法，自定义序列化。这种两个方法是私有的，并且只能被序列化机制调用。   

下面是一个典型示例，在`java.awt.geom`包中有大量的类都是不可序列化的，例如`Point2D.Double`，现在要序列化一个包含该类型字段的类，

```java
public class LabeledPoint implements Serializable {
	private String label;
	private transient Point2D.Double point;

    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException{
        in.defaultReadObject();
       	double x = in.readDouble();
       	double y = in.readDouble();
       	point = new Point2D.Double(x, y);
    }

    private void writeObject(ObjectOutputStream out) throws IOException {
        out.defaultWriteObject();
        out.writeDouble(point.getX());
        out.writeDouble(point.getY());
    }
}
```
`defaultWriteObject`和`defaultReadObject`是特殊的方法，只能在序列化类的`writeObject`和`readObject`方法中被调用。`defaultWriteObject`表示使用默认的序列化机制，`defaultReadObject`反之。这两个方法也可以不调用，这样就跟下面讲的`Externalizable`接口差不多。      
       
除了重写`readObject`和`writeObject`方法修改默认的序列化机制外，还可使用`Externalizable`接口，自定义序列化机制。     

```java
public class Director implements Externalizable {
    private String title;
    private String bonus;

    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(title);
        out.writeUTF(bonus);
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        title = in.readUTF();
        bonus = in.readUTF();
    }
}
```
### `Externalizable`和`Serializable`的不同
`Externalizable`和`Serializable`最大的不同就是，`Externalizable`会调用类的无参构造函数来创建对象，`Serializable`则不然。  另外就是`readObject`和`writeObject`只能被序列化机制调用，而`readExternal`和`writeExternal`方法是公共的。   
      
## 序列化中遇到的问题
在序列化中，有一个重要的情况需要考虑：当一个对象被多个对象共享，作为它们各种状态的一部分时，会发生什么情况？ 

```java
public class Manager extends Employee {
    private Employee secretary;

    public static void main(String[] args) {
        Employee tony = new Employee();
        tony.setName("Tony");
        tony.setSalary(10000);
        tony.setHireDay(new Date());

        Manager harry = new Manager();
        harry.setSalary(1000);
        harry.setName("Harry");
        harry.setSecretary(tony);

        Manager carl = new Manager();
        carl.setName("Carl");
        carl.setSalary(10000);
        carl.setSecretary(tony);

        ByteArrayOutputStream byteArr = new ByteArrayOutputStream();
        try (ObjectOutputStream out = new ObjectOutputStream(byteArr)) {
            out.writeObject(harry);
            out.writeObject(carl);
        } catch (IOException e) {
            e.printStackTrace();
        }

        try (ByteArrayInputStream input = new ByteArrayInputStream(byteArr.toByteArray());
             ObjectInputStream objInput = new ObjectInputStream(input)) {
            Manager harry1 = (Manager) objInput.readObject();
            Manager carl1 = (Manager) objInput.readObject();
            // out true
            System.out.println(harry1.getSecretary() == carl1.getSecretary());
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```
经过序列化后，两个对象依然共享同一对象。造成这种现象的原因是：每个对象都是用一个序列号（serial number，即前面提到的「指纹」）保存的，这也是这种机制之所以被称为对象序列化的原因。 下面是其算法：    

* 对你遇到的每一个对象引用都关联一个序列号。    
* 对于每个对象，当第一次遇到时，保存其对象数据到流中。    
* 如果某个对象之前已经被保存过，那么只写出「与之前保存过的序列号为$x$的对象相同」。 在读回对象时，整个过程是反过来的。   
* 当遇到「与之前保存过的序列号为$x$的对象相同」标记时，获取与这个顺序号相关联的对象引用。   

> 因为保存原生的内存地址毫无意义，因此序列化用序列号代替了内存地址。   

## 如何解决兼容问题
如果使用序列化保存对象，就需要考虑版本问题，修改后的类能否读入旧文件？或者反之旧版本能否读入新版本产生的文件。      
     
这时候就体现到`serialVersionUID`字段的重要性来了。假设将SHA指纹作为序列化版本的唯一ID的话，无论类的定义产生了什么样的变化，它的SHA指纹也会跟着变化，而我们都知道对象流将拒绝读入具有不同指纹的对象。为了保持兼容性，我们必须使用`serialVersionUID`常量作为序列化版本的唯一ID。      

如果这个类只有方法发生了变化，那么在读入新对象数据时是不会有任何问题的。但是，如果数据域产生了变化，那么就有可能会有问题，不过对象流将尽力将流对象转化成这个类的当前版本。   
    
对象流会将这个类当前版本的数据域与流中版本的数据域进行比较，当然，对象流只会考虑非静态和非`transient`的数据域。    

* 如果名字匹配而类型不匹配，那么对象流不会尝试将一种类型转换成另一种类型，因为这两个对象不兼容。   
* 如果流中对象具有在当前版本中所没有的数据域，那么对象流会忽略这些额外的数据。    
* 如果当前版本具有在流中对象所没有的数据域，那么这些新添加的域将被设置成它们的默认值。   
    
这种丢弃数据域或者将数据域设置为`null`有可能会产生bug，建议设计者重写`readObject`方法来修订版本不兼容问题。   

## 序列化应用时需要注意的问题
### 序列化单例和类型安全的枚举 
如果你使用Java语言的`enum`结构，那么不用担心序列化，它能够正常工作。但考虑以下风格的代码：    

```java
public class Orientation {
    public static final Orientation HORIZONTAL = new Orientation(1);
    public static final Orientation VERTICAL = new Orientation(2);

    private int value;

    private Orientation(int value) {
        this.value = value;
    }
}
```
    
这种风格的代码在`enum`之前很常见，这个类的构造器是私有的，你不可能创建除`HORIZONTAL`和`VERTICAL`之外的对象，因此你可以使用`==`操作符来测试对象的等同性。      

```java
if (orientation == Orientation.HORIZONTAL) ...
```
   
当我们序列化这样的类时，既是构造器是私有的，序列化机制也可以创建新的对象（序列化机制不通过构造器创建对象），因此上述代码就会产生bug。    
   
为了解决这个问题，我们需要定义另外一种称为`readResolve`的特殊序列化方法。该方法会在对象被序列化之后被调用。它必须返回一个对象，而该对象之后会成为`readObject`的返回值。因此我们可以这么做：    

```java
    private Object readResolve() throws ObjectStreamException {
        if (value == 1) return HORIZONTAL;
        if (value == 2) return VERTICAL;
        return null;
    }
```
    
请记住向遗留代码中所有类型安全的枚举以及向所有支持单例设计模式的类中添加`readResolve`方法。 
    
### 使用序列化clone对象
序列化机制有一种很有趣的用法，即提供了一种`clone`对象的简便途径，只需要将对象序列化到输出流中，并且将其读回。这种方式虽然方便，但性能比显式地构建新对象的方式慢的多。  

## 父类的序列化问题
一个子类实现了`Serializable`接口，而它的父类没有实现`Serializable`接口，那么序列化时父类所属的数据域并不会被序列化。__要想父类也序列化，就需要让父类也实现`Serializable`接口__。     
     
有一点非常重要，如果父类没有实现`Serializable`接口的话，就__需要有默认的无参的构造函数__。这是因为在父类没有实现`Serializable`接口时，虚拟机不会序列化父对象，而一个Java对象的构造必须先有父对象，才有子对象，反序列化也不列外。  

## 安全问题
序列化后的字节序列并没有加密，若被黑客窃取了这部分数据，很容易的解析出数据域里的内容。 一个解决方案就是重写`writeObject`方法，对敏感内容加密后写入对象流，然后在`readObject`中解密。   