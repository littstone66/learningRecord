# `eladmin 框架学习记录`



## `注解`

1. `@RestController = @Controller + @ResponseBody` 
2. `@RequestMapping 请求映射` 
3. `@Component 将一个类（通常是通用的类）注册为bean` 
4. `@Repository：Dao层的类注册为bean` 
5. `@Service：Service层的类注册为bean` 
6. `@Controller：Controller层的类注册为bean`
7. `@Configuration 将配置类注册为bean`
8. `@Indexed 在项目中使用了@Indexed之后，编译打包的时候会在项目中自动生成META-INT/spring.components文件当Spring应用上下文执行ComponentScan扫描时，META-INT/spring.components将会被CandidateComponentsIndexLoader读取并加载，转换为CandidateComponentsIndex对象，这样的话@ComponentScan不在扫描指定的package(包)，而是读取CandidateComponentsIndex对象，从而达到提升性能的目的。` 
9. `@Value：可以从配置文件中读取值并赋值`
10. `@Bean：产生一个bean对象，并将这个对象交给Spring管理，Spring在创建这个对象时只会调用一次`
11. `@primary：在Srping容器中使用@Bean注解，往ioc容器里面注入两个相同的bean对象，则会报错，但是如果@primary和@bean同时使用，则带有@Primary注解的bean对象会替代与之相同的bean对象，提高了优先级`
12. `@Inherited：如果该注解修饰注解，那么其子类会继承父类的注解，否则则不会继承。也就是说如果需要定义一个用于类注解的时候，需要该注解也作用于子类，则可以用@Inherited来修饰`
13. `@Mapper：作用于Dao层的接口，相当于mapper.xml文件，使用@Mapper之后不需要在Spring中配置扫描路径，等同于@Reponsitory和@MapperScan的结合，所以使用@Mapper注解可以省略@Responsitory和@MapperScan`
14. `@Reponsitory和@Mapper类似都是作用于Dao层的接口，但是这个注解不等同于mapper.xml，而且使用这个注解的话需要在Spring的启动类上配置添加@MapperScan注解`
15. `@Param：服务于SQL语句的赋值，方法(@Param("userName") String name == where user_name = #{userName}`
16. `@AliasFor：用来给指定的属性设置别名，一般是用在自定义注解上，就像@Value（name=“”） = @Value （value = “”），name和value作用都一样，都是说明这个字段的含义`
17. `@ConfigurationProperties：在SpringBoot里要将Java对象与配置文件中的数据绑定，需要用到@Value注解，@ConfigurationProperties 也可以绑定数据，与@Value 的差别是@ConfigurationProperties 一次可以绑定多个数据，@Value 只能一次绑定一个数据，但是他要求命名更加严格，要使用这个注解需要在Spring配置类或者启动类上添加@EnableConfigurationProprties注解，开启这个功能才能使用`
18. `@CreatedBy：用在实体类上，插入数据库中的一条数据会自动附加上创建人的信息`
19. `@LastModifiedBy：用在实体类上，更新记录时会自动附加上更新人的信息`
20. `@CreatedDate：同理` 
21. `@LastModifiedDate：同理，在比较规范的项目中，需要对每条数据做记录，所以基本上每条数据都有更新人，创建人，创建时间，更新时间，同上面四个注解相同`
22. `@Override：在方法上添加了这个注解，编辑器就会检查这个方法是否真的重写了父类的同名方法，可读性会得到提高，所以当子类重写了父类的方法需要使用@Override 注解`
23. `@EnableCaching：开启缓存，Spring自带的缓存注解，一般与@Cacheable一起使用，@Cacheable的作用是添加缓存，可以在查询公用的数据量大的数据时把这查询出的数据添加到缓存，当这些数据被修改时，缓存中的数据将会被删除`
24. `@Cachevict：清除缓存，也是放在方法上，执行方法则会清除指定的缓存或者全部缓存`
25. `@CacheConfig(cacheNames = "data")：在类上使用，表明该类下面所有使用缓存的方法的缓存组件都是名为data，不使用这个注解也行，只不过就需要在每个使用缓存的注解上添加名字，显得繁琐`
26. `@ConditionalOnClass：@Conditional是一个条件化注解，只有当满足指定条件Spring才会创建bean，@ConditionalOnClass的意思是只有某个类在类路径上才会创建bean。与此类似的注解还有@ConditionalOnBean：只有当上下文中不存在某个注解才会创建bean等`
27. `@SuppressWarnings("all")：用来抑制警告，有的代码在程序编译完成或者启动之后会在控制台打印警告信息，如果在编码阶段就确定这些警告不影响程序的正常执行，就可以使用这个注解来抑制警告，使对警告保持静默态度，这样有利于开发者更关心已有的报错信息`
28. `@RestControllerAdvice：是一个组合注解，由@ControllerAdvice和@ResponseBody组成，作用一般是配置全局异常处理器（ExceptionHandler），每个方法使用@ExceptionHandler注解，再添加异常类型，如果发生了指定的异常就会执行这个方法里面的异常，并打印出指定的异常信息`
29. `@NotBlank：用在字段上，被注释的字段不能为null，但是可以为empty`
30. `@NotEmpty：用在字段上，被注释的字段不能为null，但是长度必须 >0`
31. `@NotBlank：用在字段上，只能用在String类型的不能为null，但是调用trim()之后长度必须 >0，上面这仨注解必须配套@Valid使用，否则不起作用`
32. `@Transactional：作用在方法上，如果该方法发生了异常（异常类型可以指定），就会发生回滚。注意如果在该方法所在的类中调用这个添加了事务的方法，及时发生了异常，也不会回滚，在别处调用需要使用对象调用才会正常回滚`
33. `@EnableTransactionManagement：SpringBoot开启事务支持`
34. `@Async：作用在方法上，表明该方法是一个异步方法，需要在配置类或者启动类上使用@EnableAsync，这个注解开启才能有效。注意：这个注解与SpringSecurity框架一起使用可能会出现问题，异步方法获取不到当前登录的用户信息，可能会报空指针异常`
35. `@EnableGlobalMethodSecurity：开启方法执行前后的权限检查，前提是方法需要使用@PreAuthorize，类似的权限检查注解`
36. `@PreAuthorize：在方法调用前进行权限检查或者增加一些限制条件，符合这些条件才能够调用方法`



## `Lombok注解`

1. `@Data：会提供类的get、set、hashCode、canEqual、toString方法`
2. `@AllArgsConstructor：会提供类的所有参数构造器`
3. `@NoArgsConstructor：会提供类的无参构造器`
4. `@Setter：提供类的set方法`
5. `@Getter：提供类的get方法`
6. `@EqualsAndHashCode：提供类的Equals和HashCode方法`
7. `@Log4j/@Slf4j：提供日志功能，变量名为log`
7. `@RequiredArgsConstructor：主要对类中被final修饰的属性生成构造器`

## FastJson

1. `@JSONField：可以指定类字段的名字，日期格式，输出序列化的顺序、是否序列化某个字段等`





## `Mybatis-Plus注解`

1. `@TableName：作用于Dao层的实体类上，实体类对应的表名`
2. `@TableId：实体类字段与数据表中的ID相对应`



## `Swagger注解`

1. `@ApiModelProperty：用于对实体类字段的描述，说明这个字段的作用`
2. `TableField：主要解决数据表中的字段和实体类中的字段不一致、实体类中的字段在表中不存在的问题`
2. `@Api：作用在类上给类添加描述信息，一般使用tags属性，使用tags添加的描述信息，在Swagger的前端UI上也能看到`
4. `@ApiOperation：作用在方法上，给方法添加描述信息，一般使用value属性`
5. `@ApiimplicParams：作用在方法上，给方法的参数添加描述信息`



## `元注解`

1. `@Documented` 生成文档时有标记，没有什么实际作用
2. `@Retention` 被这个注解修饰的注解能在某处生效
   1. `source`
   2. `class`
   3. `runtime`
3. `@Target：用来标识这个注解可以使用的地方，方法、类、字段上`

## `AOP概念`

### `个人理解`

`AOP为面向切面编程，常规的编程方式是线性编程（实现业务逻辑之类的），面向切面编程主要是为了解耦，以实现“可插拔”的效果，使能够很轻易地添加或者删除一个功能，常用场景如：日志记录，性能统计，安全控制，事务处理`

### `注意`

`所有的增强含义翻译成大白话均为执行了某个方法`

### `注解`

1. `@Aspect：声明一个类为切面，大白话就是这个AOP要在这个类里面写`
2. `@Pointcut：切入点，切点表达式，里面写要执行方法所在的类路径`
3. `@Around：要增强方法的执行前和执行后都要增强`
4. `@AfterReturning：方法返回之后将会执行增强`
5. `@Before：方法执行前将会执行`
6. `@AfterThrowing：异常抛出之后将会增强`
7. `@After：方法执行后将会增强`





## `概念`

1. `VO、DTO、PO、Entity`
   1. `VO可以简单理解为后端返回给前端的数据保存形式`
   2. `DTO是前端传给后端的数据保存形式`
   3. `VO、DTO区别：在实际的业务中可能会在VO中对DTO中的增删一些字段或者做出一些额外的解释`
   4. `一些工具类的系统和一些业务不是很复杂的系统DTO是可以和BO合并成一个，当业务扩展的时候注意拆分就行`
   5. `VO是可以第一个优化掉的，展示业务不复杂的可以压根儿不要，直接用DTO`



# `框架`

## `SpringSecurity`

1. `自定义是否拦截某个url`
2. `自定义权限不足（未授权）异常信息`
   1. `实现某个接口，然后将该对象的注入到SpringSecurity的过滤器链条中`

# `Java常用类`

1. `LocalDateTime，获取时间类`



# `疑问`

1. `为什么要重写toString（）方法`

   `toString方法是Object的，如果不重写toString方法，那么如果直接输出一个对象，就会把一个对象的地址给输出出来，类似@15db9742这种，完全不懂是啥意思，但是如果重写了toString（）方法再输出对象，就会出现对象的详细信息，形如：Person{name = '不一样的烟火', age = 21}`





# `常用类库`

```xml
<!-- 切面依赖-->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
    <version>1.9.7</version>
</dependency>

<!-- Java图形验证码 -->
<dependency>
    <groupId>com.github.whvcse</groupId>
    <artifactId>easy-captcha</artifactId>
    <version>1.6.2</version>
</dependency>

<!-- jjwt jwt令牌 -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId> <!-- or jjwt-gson if Gson is preferred -->
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>

<!-- lombok 使代码更加的优雅、简洁--> 
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.4</version>
    <scope>provided</scope>
</dependency>
```



