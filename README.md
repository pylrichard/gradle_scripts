# Gradle构建通用脚本

## 概述

从Maven的流行来看，构建过程95%以上的情况不需要自行扩展，如果这么做了，只会让构建变得难以理解

Gradle给了足够的自由，约定优于配置，但Gradle太灵活，可能会造成不可控

为了减少重复开发，降低维护成本

1 将build.gradle中构建通用逻辑拆分到多个文件中

2 修改后的build.gradle变得极其简洁，只需要关心基本信息及依赖即可

3 构建通用逻辑存储在git仓库，方便维护，从而使Gradle的使用更加规范，更加简单

## init.gradle的加载顺序

Gradle会依次对相关目录进行检测，按照优先级加载对应目录下的文件

如果一个目录下有多个文件被找到，则按照英文字母的顺序依次加载

加载优先级如下:

1 通过`--I`或者`–init-script`参数在构建开始时指定路径，如

```
gradle --init-script init.gradle clean

gradle --I init.gradle assembleDebug
```

2 加载USER_HOME/.gradle/init.gradle文件

3 加载USER_HOME/.gradle/init.d下的以.gradle结尾的文件

4 加载GRADLE_HOME/init.d下的以.gradle结尾的文件

Gradle可以通过`apply from`命令加载外部gradle文件，可以加载远程http服务器的gradle文件

## Gradle缓存位置

下载的文件存储在~/.gradle/caches

使用`find / -name "*.gradle"`进行查找

## 官方文档

[Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/html/)

[Java Plugin](https://docs.gradle.org/current/userguide/java_plugin.html)