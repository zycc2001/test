```java
byte b1 = 10;
byte b2 = 20;

byte b3 = b1 + b2; // 该行报错，因为byte类型参与算术运算会自动提示为int，int赋值给byte可能损失精度

int i3 = b1 + b2; // 应该使用int接收
byte b3 = (byte) (b1 + b2); // 或者将结果强制转换为byte类型

```

**1）向上转型，即子类转父类**

- 父类引用指向子类对象就是向上转型
- 格式
- ```
  父类型 对象名 = new 子类型对象（）;
  父类引用调用方法是被重写过的
  ```

**2）向下转型，即父类转子类**

- 可以调用子类的特有成员
- 子类引用指向父类强转成子类的对象。
- 格式
- ```
  子类型 对象名 = (子类型)父类引用;
  ```

### 抽象类的特点

- 抽象类和抽象方法必须使用 abstract 关键字修饰

```java
//抽象类的定义
public abstract class 类名 {
    //抽象方法的定义
    public abstract void eat();
}
```

- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类

- 抽象类的子类

- 要么重写抽象类中的所有抽象方法

- 要么是它也是一个抽象类

  

  `一个*.java文件中可以包含多少个public类？A.最多1个

### 无参构造函数里调用有参构造函数

```java
    Cylinder(int radius,int height) {//有参
        this.height=height;
        this.radius=radius;
        System.out.println("Constructor with para");
    }
    Cylinder() {//无参
        this(2,1);//无参里调用有参
        System.out.println("Constructor no para");
    }
```

```java
Person pp[] = new Person[2];//对象数组的声明
         pp[0]=new Person();//对象的声明？？？？？？？？？？
         pp[1]=new Person(name);
```

### 抛出异常

### 动态数组

`ArrayList<Main> ss=new ArrayList<>(n);`

### 匿名内部类

An anonymous(匿名) inner class can access final variables in any enclosing scope.





````java
 class B{
    int x=100,y=200;
    public void setX(int x){ x=x; }//相当于把x赋给自己 并不能改变对象的x的值
    public void setY(int y){ this.y=y; } 
    public int getXYSum(){ return x+y; } 
 } 
 public class A { 
    public static void main(String args[]){
        B b=newB(); 
        b.setX(-100); 
        b.setY(-200); 
        System.out.println("sum="+b.getXYSum()); 
    } 
 } 
//运行结果为 sum=-100
````

### 四种权限修饰符

注意事项: `(default)`并不是关键是`default`而是什么也不写

|                    | public | protected | (default) | private |
| ------------------ | ------ | --------- | --------- | ------- |
| 同一个类           | 1      | 1         | 1         | 1       |
| 同一个包           | 1      | 1         | 1         | 0       |
| 不同包子类(需继承) | 1      | 1         | 0         | 0       |
| 不同包非子类       | 1      | 0         | 0         | 0       |

### 内部类

1.成员内部类

2.局部内部类(包含匿名内部类)

#### 成员内部类的格式：

```java
修饰符 class 外部类名称Outer{
	修饰符 class 内部类名称Inner{
	}
}
//注意:内用外，随意访问，反之，借助内部类对象
// Outer&Inner.class //内部类的文件形式
 
```

成员内部类的方法的调用

1. 1.间接调用：在外部类的方法中，使用内部类，在`main`中调用外部类的方法间接的使用内部类的方法
2. 2.直接调用: 外部类名称`.`内部类名称 = `new` 外部类名称()`.`内部类名称

内部类同名的访问方法

1. 1.内部类访问外部类的重名变量 `Outer.this.v`//outer表示外部类，内部外部类都有`v`变量

#### 局部内部类：

此类是定义在一个方法体内部的，出了方法体便失去了意义

