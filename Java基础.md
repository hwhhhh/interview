# Java基础

## 基础概念

### 什么是字节码

.class文件就是字节码，java程序从源代码到运行的过程如下图：

![Java程序转变为机器代码的过程](assets/java-code-to-machine-code.png)

一开始，JVM加载字节码文件通过解释器逐行解释执行，后面引入JIT，**JIT（just-in-time）属于运行时编译**，完成第一次编译后会保存字节码对应的机器码。

![编译型语言和解释型语言](assets/compiled-and-interpreted-languages.png)

## 面向对象基础

### 面向对象三大特征

**封装、继承、多态**

- **封装**：将一个对象的状态信息（就是属性）封装在对象内部，不允许外部对象直接访问对象内部信息，但可以提供一些方法。

- **继承**：描述类和类之间的关系，使用已有类作为新类的基础，新类可以拓展，也可以使用父类功能。提高代码重用，增加可维护性。

  特别的：

  1. 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。

  2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。

  3. 子类可以用自己的方式实现父类的方法。

- **多态**：表示一个对象具有多种的状态，简单的说就是“一个函数，多种实现”，或是“一个接口，多种方法”。多态性表现在程序运行时根据传入的对象调用不同的函数。实现多态有两种方式：重写（覆盖），重载。

### 重载和重写

**重载**：方法名一样，参数不一样。

**重写**：子类重写父类方法。

### 深拷贝、浅拷贝和引用拷贝

浅拷贝：**会在堆上建立一个新的对象（区别于引用拷贝）**，如果原对象内部属性是**引用类型**的话，浅拷贝会直接复制内部对象的引用地址，就是说拷贝对象和原对象共用一个内部对象。

深拷贝：会完全复制整个对象，包括这个对象所包含的内部对象。

引用拷贝：**两个不同的引用指向同一个对象。**

![浅拷贝、深拷贝、引用拷贝示意图](assets/shallow&deep-copy.png)

### 接口和抽象类

**共同点**

1.都不能被实例化 2.都可以包含抽象方法 3.可以有默认实现的方法

**区别**

1. 接口是对类行为的进行约束，实现接口就有对应的行为；抽象类主要用于代码复用，强调从属关系。

2. 一个类只能继承一个类，可以实现多个接口
3. 接口中的成员只能是`public static final`类型的，**不能被修改且必须有初始值**，抽象类可以在子类被重新定义和赋值。

## 泛型

### 什么是泛型？

泛型，即“参数化类型”，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。

### 为什么说java是伪泛型？

泛型擦除：Java 语言中的泛型，它只在程序源码中存在，在编译后的字节码文件中，就已经替换为原来的原生类型（Raw Type，也称为裸类 型），并且在相应的地方插入了强制转型代码。对于运行期的 Java 语言来说，ArrayList＜int＞与 ArrayList＜String＞就是同一个类。泛型技术实际上是 Java 语言的一颗语法糖，**Java 语言中的泛型实现方法称为类型擦除，基于这种方法实现的泛型称为伪泛型。**

### 泛型的好处？

1. 类型安全：泛型可以帮助我们在编译时就发现类型不匹配的错误，避免了等到运行时才发现的尴尬。

2. 可读性：使用泛型可以让程序的代码更加简洁明了，减少了类型转换的代码，使程序更容易阅读和维护。

3. 代码复用：泛型可以使我们的代码更具有通用性，可以使一个类或方法具有更广泛的适用性，从而减少了冗余代码的编写。

4. 性能提高：泛型可以消除许多强制类型转换，从而在性能上获得提升。

5. 兼容性：泛型可以让我们的代码更加兼容不同的数据类型和版本。

### 基本数据类型可以作为泛型吗？

不可以。泛型通过类型擦除来实现，基本数据类型在擦除后无法转换成对象类型。可以用对应的包装类实现。

## 反射

### 什么是反射？

Java的反射（reflection）机制是指在程序的运行状态中，我们亦可以分析类以及执行类中方法。

### 反射的应用场景？

**各种框架如Spring/SpringBoot、MyBatis**等，大量使用了反射机制。这些框架大量使用了**动态代理**，动态代理的实现依赖于反射。另外，Java中**注解**的实现也用到了反射。基于反射分析类，然后获取到类/属性/方法/方法的参数上的注解。获取到注解之后，就可以做进一步的处理。

### 反射的优缺点

优点：让代码更加灵活，为各种框架提供开箱即用的功能提供便利。

缺点：增加了安全问题，如可以无视泛型参数的安全检查。

### 反射实战

**获取类对象的四种方式**

```Java
Class alunbarClass = TargetObject.class;// 知道具体类
Class alunbarClass1 = Class.forName("com.hwhhhh.TargetObject");//通过传入类的全路径
Class alunbarClass2 = o.getClass();// 通过对象实例o获取
Class alunbarClass3 = ClassLoader.getSystemClassLoader().loadClass("com.hwhhhh.TargetObject");//传入类路径
```

**操作方法和参数**

```java
package cn.javaguide;

import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException, NoSuchFieldException {
        /**
         * 获取 TargetObject 类的 Class 对象并且创建 TargetObject 类实例
         */
        Class<?> targetClass = Class.forName("com.hwhhhh.TargetObject");
        TargetObject targetObject = (TargetObject) targetClass.newInstance();
        /**
         * 获取 TargetObject 类中定义的所有方法
         */
        Method[] methods = targetClass.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method.getName());
        }

        /**
         * 获取指定方法并调用
         */
        Method publicMethod = targetClass.getDeclaredMethod("publicMethod",
                String.class);

        publicMethod.invoke(targetObject, "JavaGuide");

        /**
         * 获取指定参数并对参数进行修改
         */
        Field field = targetClass.getDeclaredField("value");
        //为了对类中的参数进行修改我们取消安全检查
        field.setAccessible(true);
        field.set(targetObject, "JavaGuide");

        /**
         * 调用 private 方法
         */
        Method privateMethod = targetClass.getDeclaredMethod("privateMethod");
        //为了调用private方法我们取消安全检查
        privateMethod.setAccessible(true);
        privateMethod.invoke(targetObject);
    }
}
```

## 代理模式

简单来说就是**使用代理对象来代替对真实对象(real object)的访问，这样就可以在不修改原目标对象的前提下，提供额外的功能操作，扩展目标对象的功能。**

代理模式的主要作用是**扩展目标对象的功能，比如说在目标对象的某个方法执行前后可以增加一些自定义的操作。**