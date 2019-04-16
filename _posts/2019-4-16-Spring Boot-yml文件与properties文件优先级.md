---
layout: post
title: "yml与properties的优先级"
date: 2019-04-16
categories: Java SpringBoot
tags: Java SpringBoot Maven Tomcat Idea
---

* content
{:toc}
今天在学习SpringBoot的时候，发现项目中同时存在application.yml和application.properties时会存在优先级问题。



```properties
#application.properties中配置端口
server.port=8080
```

```yaml
#application.yml中配置端口
server:
  port: 8081
#spring:
#  profiles:
#    active: dev
---
server:
  port: 8082
spring:
  profiles: dev
---
```

此时运行，会发现端口号为==8080==



```yaml
#application.yml中配置端口
server:
  port: 8081
spring:
  profiles:
    active: dev
---
server:
  port: 8082
spring:
  profiles: dev
---
```

那么还是会先执行这里的yml激活的8082端口. 

