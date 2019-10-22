@value

```java
@Configuration
public class DruidProperties
{
    @Value("${spring.datasource.druid.initialSize}")
    private int initialSize;

    @Value("${spring.datasource.druid.minIdle}")
    private int minIdle;

    @Value("${spring.datasource.druid.maxActive}")
    private int maxActive;

    @Value("${spring.datasource.druid.maxWait}")
    private int maxWait;
 }
```

@ConfigurationProperties(prefix="person")

```java
@Configuration
@ConfigurationProperties(prefix="person")
public class DruidProperties
{
    //@Value("${spring.datasource.druid.initialSize}")
    private int initialSize;

    //@Value("${spring.datasource.druid.minIdle}")
    private int minIdle;

    //@Value("${spring.datasource.druid.maxActive}")
    private int maxActive;

    //@Value("${spring.datasource.druid.maxWait}")
    private int maxWait;
 }
```

使用场景

1，如果我们在某个业务中只是需要取一下文件中的某项值，使用@Value

2, 如果我们专门编写了一个javaBean 来和配置文件映射，我们就用@ConfigurationProperties

3, 使用PropertySource(value={"classpath:person.properties"})可以加载指定的配置文件，进行数据匹配

```java
@Configuration
@PropertySource(value={"classpath:person.properties"})
@ConfigurationProperties(prefix="person")
public class DruidProperties
{
    private int initialSize;

    private int minIdle;

    private int maxActive;

    private int maxWait;
 }
```

SpringBoot向容器中中注入bean对象的两种方法

1，在主类中添加@ImportResource(locations={"classpath:beans.xml"})

```java
@SpringBootApplication
@ImportResource(locations={"classpath:beans.xml"})
public class RuoYiApplication
{
    public static void main(String[] args)
    {
        SpringApplication.run(RuoYiApplication.class, args);
    }
}
```

在classpath下添加beans.xml文件即可

2，springBoot添加配置类@Configuration

```java
@Configuration
public class MyConfig{
  @Bean
  public HelloService helloService()
  {
    return new HelloService();
  }
}
```

配置文件占位符

```properties
application.properties

person.name = 张三${random.uuid}

person.dog.name = ${person.hello:hello}_dog  ## 注意： 如果person.hello 取不到值，则取冒号后面的hello
```

SpringBoot支持多环境配置

application-dev.properties中配置

```
server.port = 8080
```

application-pro.properties中配置

```
server.port = 80
```

application.properties中配置

```properties
server.port = 8081

## spring激活某个指定文件
spring.profiles.active = dev
```

yml 多文档块方式指定开发环境

```yaml
server:
	port : 8080
spring:
	profiles:
		active: dev
---
server:
	port : 8083
spring:
	profiles: dev
---
server:
	port : 8083
spring:
	profiles: pro
```

命令行方式指定生产环境

```shell
java -jar xxxx.jar --spring.profiles.active=dev
```

虚拟机参数指定生产环境

```shell
vm params : -Dspring.profiles.active = dev
```

