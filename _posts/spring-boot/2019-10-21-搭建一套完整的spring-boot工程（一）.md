## 1, 搭建基本的启动工程(支持jar包启动和tomcat部署启动方式两种)

### 1.1 搭建一个支持jar包启动的spring-boot工程

#### 1.1.1 配置springboot启动所需要的maven坐标

##### 1.1.1.1 加入父pom依赖

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.1.RELEASE</version>
    <relativePath/>
</parent>
```

##### 1.1.1.2 添加依赖基本属性

```xml
 <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <java.version>1.8</java.version>
  </properties>
```

##### 1.1.1.3 添加启动坐标

```xml
<dependencies>
    <!-- SpringBoot 核心包 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
    </dependency>

    <!-- SpringBoot 测试 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
    </dependency>

    <!-- SpringBoot Web容器 -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- spring-boot-devtools -->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <optional>true</optional> <!-- 表示依赖不会传递 -->
    </dependency>
  </dependencies> 
```

##### 1.1.1.4 添加maven编译插件

```xml
<build>
    <finalName>${project.artifactId}</finalName>
    <plugins>
      <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <configuration>
          <fork>true</fork> <!-- 如果没有该配置，devtools不会生效 -->
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>${java.version}</source>
          <target>${java.version}</target>
          <encoding>${project.build.sourceEncoding}</encoding>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

1.1.1.5 添加仓库

```xml
<repositories>
    <repository>
      <id>public</id>
      <name>aliyun nexus</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <releases>
        <enabled>true</enabled>
      </releases>
    </repository>
  </repositories>
```

1.1.1.6 添加插件仓库管理

```html
<pluginRepositories>
    <pluginRepository>
      <id>public</id>
      <name>aliyun nexus</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <releases>
        <enabled>true</enabled>
      </releases>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </pluginRepository>
  </pluginRepositories>
```

#### 1.1.2 添加启动类

```java
@SpringBootApplication
public class App 
{
    public static void main( String[] args )
    {
        SpringApplication.run(App.class,args);
    }
}
```

1.1.3 添加一个控制层controller类

```java
@RestController
public class TestController {

    @GetMapping("/hello")
    public String hello ()
    {
        return "hello world";
    }
}
```

#### 1.1.4 启动主启动类，

浏览器器测试，发现返回数据hello，表明基本工程搭建完成

#### 1.1.5 maven 编译成jar包

使用idea对工程打包，修改名字为boot-vue.jar

拓展（maven）

#### 1.1.6 jar包测试

cmd 进入打好的jar包目录，使用命令

java -jar boot-vue.jar

浏览器测试 发现正常返回hello数据，jar包方式构建完成

### 1.2  搭建一个支持tomcat部署启动的工程

#### 1.2.1 在原有jar工程中添加web启动容器即可

```java
public class SustarServletInitializer extends SpringBootServletInitializer{
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
        return builder.sources(Sustar.class);
    }
}
```

