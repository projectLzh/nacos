# Nacos 使用：

1. 下载 nacos-server-$version.tar.gz  下载地址：https://github.com/alibaba/nacos/releases
2. tar -xvf nacos-server-$version.tar.gz    
3. 进入到nacos/bin 并输入 sh startup.sh -m standalone 
* 注：使用单机模式启动  如果不是单机启动 会报连接Mysql的错误， 就算改了配置文件，也会报连接超时的问题

4. 创建一个SpringBoot 的Mavne的项目 添加如下配置
    
```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.5.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <dependencies>
        <!--服务发现(注册中心) -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
            <version>2.2.1.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-log4j2</artifactId>
        </dependency>
    </dependencies>
```



5. 创建application.yml 并添加如下内容：
	
```
spring:
  	application:
   	name: testNacos_No1
   	cloud:
    	nacos:
      	discovery:
        server-addr: localhost:8848
server:
    port: 9999
```

7. 创建RecruitApplication.java 启动类：

```
package com.corpvip.server;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

/**
 * @author laizhihui on 2020/6/12
 */
@SpringBootApplication
@EnableDiscoveryClient
public class RecruitApplication {
    public static void main(String[] args) {
        SpringApplication.run(RecruitApplication.class, args);
    }
}

```
8. 项目启动后 在浏览器中打开 输入 http://192.168.110.245:8848/nacos/index.html  为什么是输入这个地址
进入 nacos/logs  cat start.out  

9. 打开后输入用户名/密码 nacos/nacos
10. 进入到服务器管理/服务器列表就可以看到刚刚启动的Client服务
