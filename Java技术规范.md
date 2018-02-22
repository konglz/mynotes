# Java技术规范

## 一、为什么需要规范

* java的优势在于生态，而java生态的基础是规范，不遵从规范就难以利用java生态

* 只遵从一套规范的一部分规则，而不遵从所有规则，就容易踩到坑里

* 遵从java的规范，可以让我们站上巨人的肩膀

## 二、有哪些规范

### 1. 编码规范

* [编码规范](https://github.com/alibaba/p3c/blob/master/%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4Java%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%EF%BC%88%E7%BA%AA%E5%BF%B5%E7%89%88%EF%BC%89.pdf)

### 2. Java Bean规范

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

* 关于取方法，布尔型变量最好**不要用isXxx、setXxx、getXxx**，比如：isDeleted最好改成deleted，否则可能会导致一些框架get属性出错

* 接收请求参数的bean、接收数据库数据的bean，属性最好不要用基本类型，要用封装类型，比如：private boolean deleted最好改成private Boolean deleted

### 3. spring注解使用规范

#### 声明Bean的注解：

* @Component：组件，没有明确的角色。

* @Service：在业务逻辑层（Service层）使用。

* @Repository：在数据访问层（dao层）使用。

* @Controller：在展现层（MVC→Spring MVC）使用

* @Configurable 声明当前类是一个配置类

* @ComponentScan("com.reachauto.cxn.book.test")  设置自动扫描包下面所有的 @Service @Component @Repository @Controller 一般在全局启动配置中配，慎用，勿滥用

* @EnableScheduling 注解开启对计划任务的支持，一般在全局启动配置中配，慎用，勿滥用

#### 注入Bean的注解，一般情况下通用：

* @Autowired：Spring提供的注解。

* @Inject：JSR-330提供的注解。

* @Resource：JSR-250提供的注解。

* @Value("xxxx") 注入普通字符串，常量

*  @Value("${xxx.xxx}") 注入配置文件中字符串

*  @PostConstruct 标注在方法上，在构造函数执行完毕后执行

* @PreDestroy Bean 标注在方法上，销毁前执行，比如释放资源（关闭线程池等）

* @Async 异步方法表明，若是在class上则全是

* @Scheduled 声明方法是计划任务

* @Conditional() 条件注解，当满足某条件时

* @Autowired、@Inject、@Resource可注解在set方法上或属性上，但建议注解在属性上，优点是代码更少、层次更清晰。

* @Autowired、@Inject、@Resource注解在属性上时，不需要存方法也能注进来，它是根据反射设值的，所以，在此时最好不要定义存方法

#### SpringMvc相关

* @RequestMapping 用于映射Web请求 返回体，编码格式都可以在此处设置 produces = {} 设置返回值json/xml charset 等

* @RestController 这是个组合注解，组合了@Controller和@ResponseBody

* @ResponseBody 支持返回体放入response体中，而不是直接返回一个页面，此注解可以放在返回值或者方法体上

* @RequestBody 允许参数在request体里，而不是在地址栏后面

* @PathVariable 用来接收路径参数，api/{id}

### 4. 数据规范

#### 创建表相关

* 尽量满足3NF 所有字段值都是不可分解的原子值;也就是说在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中; 每一列数据都和主键直接相关，而不能间接相关.

* 按照微服务分库/实例，一个服务尽量只访问自身的表；如果要访问其他服务的表，则应当调接口，而不应该直接查对方的库

#### sql相关

* 不要写过于复杂的sql，join不应该超过3层，不要企图用一条语句搞定所有事情；遇到复杂查询，可以想办法在多次查询并在应用层拼接数据；因为应用程序容易扩展，数据库不易扩展，应当适当减轻数据库的计算负担
