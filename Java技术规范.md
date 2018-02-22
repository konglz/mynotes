# Java技术规范

## 一、为什么需要规范

* java的优势在于生态，而java生态的基础是规范，不遵从规范就难以利用java生态

* 只遵从一套规范的一部分规则，而不遵从所有规则，就容易踩到坑里

## 二、有哪些规范

### 1. 编码规范

* [编码规范](https://github.com/waylau/java-code-conventions/blob/master/README.md)

### 2. 命名规范

### 3. Java Bean规范

#### 要求

* JavaBean 类必须是一个公共类，并将类的访问属性设置为 public  ，如： public class user{......}

* JavaBean 类必须有一个空的构造函数：类中必须有一个不带参数的公用构造器

* 一个javaBean类不应有公共实例变量，类变量都为private  ，如： private int id;

* 属性应该通过一组存取方法（getXxx 和 setXxx）来访问，一般是IDE(Eclipse、JBuilder) 为属性生成getter/setter 方法

* 存方法的返回值必须为void，即不返回任何值

#### 禁止

* 必须通过java bean的存方法存值、取方法取值，不应该直接调用属性，尤其是通过反射访问属性更不应该（写框架例外）

* 关于存方法，**禁止用builder模式**（链式调用）的存方法，否则可能会导致一些框架set属性出错

* 存方法应当仅仅用于设置**1个属性**的值，不应得设置多个属性的值，除了设值之外，也**不要写其他逻辑**

* 关于取方法，布尔型变量最好**不要用isXxx**，比如：isDeleted最好改成deleted，否则可能会导致一些框架get属性出错

* 接收请求参数的bean、接收数据库数据的bean，属性最好不要用基本类型，要用封装类型，比如：private boolean deleted最好改成private Boolean deleted

