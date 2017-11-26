# 开发环境相关

## 工程

esignpro-exception-collector需要和esignpro-service放在同一级目录，存在引用关系

### PKCS10 Missing In Jdk8

Java8中，PKCS10所在package移到了`sun.security.pkcs10`

### Sonar

是一个集成了CheckStyle、PMD、Findbugs的代码校验规则，重复代码发现，代码测试覆盖率，代码注释率，及所有的检测率变化追踪的完美代码质量检查工具。

目前公司使用Java7，Sonar最后支持Java7的是5.5版本，对应的sonar-maven-plugin版本2.7.1

```
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>sonar-maven-plugin</artifactId>
    <version>2.7.1</version>
</plugin>
```

龙辉本有意使用Findbugs，但是没人使用，一定要结合CI才可以。

Sonar的客户端工具：SonarLint

## 环境配置

### 数据库

#### 开发测试环境

121.41.110.33:3306
developer
Dev#timevale123