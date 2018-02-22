# Java技术规范

## 1. 命名规范

## 2. Java Bean规范

### 要求

* JavaBean 类必须是一个公共类，并将类的访问属性设置为 public  ，如： public class user{......}

* JavaBean 类必须有一个空的构造函数：类中必须有一个不带参数的公用构造器

* 一个javaBean类不应有公共实例变量，类变量都为private  ，如： private int id;

* 属性应该通过一组存取方法（getXxx 和 setXxx）来访问，一般是IDE(Eclipse、JBuilder) 为属性生成getter/setter 方法

### 禁止

* 关于存方法，禁止用builder模式（链式调用），否则可能会导致一些框架set属性出错

* 关于取方法，布尔型变量最好不用用isXxx，比如：isDeleted最好改成deleted，否则可能会导致一些框架get属性出错

* 接收请求参数的bean、接收数据库数据的bean，属性最好不要用基本类型，要用封装类型，比如：private boolean deleted最好改成private Boolean deleted
