# Maven使用

## Maven Archetype Plugin

生产代码骨架

## Maven Compile Plugin

### 使用过程中的问题

#### 使用rt.jar时，提示找不到类库

sun.security.pkcs10.PKCS10

在plugin的configuration中增加如下代码：

```
<compilerArgs>
    <arg>-XDignore.symbol.file</arg>
</compilerArgs>
<fork>true</fork>
```

- 原因分析：

	javac在编译代码时，当他尝试从rt.jar中找寻对应的类文件时，

	会默认从对应的符号表文件ct.sym (同样在jre/lib/下)中查找该类是否存在，

	由于ct.sym中有意或无意的遗失了部分rt.jar中的类，包括sun.security.pkcs10.PKCS10，因此导致编译报错。

- 解决方法：

	就是通知javac编译器，在编译代码时，忽略该符号表ct.sym, 

	直接查找rt.jar，通过给javac传入对应的参数完成：-XDignore.symbol.file

	`<fork>true</fork>`
	在此例中也是必须要配置的，是因为maven-compile-plugin会默认忽视所有-XD参数，所有必须使用独立的编译器。

	关于fork的作用参考: <https://maven.apache.org/plugins/maven-compiler-plugin/compile-mojo.html#fork>

## Settings.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  <profiles>
    <profile>
      <id>wacai</id>
      <repositories>
        <repository>
          <id>wacai-public</id>
          <url>http://repo.caimi-inc.com/nexus/content/groups/public/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </repository>
        <repository>
          <id>wacai-third</id>
          <url>http://repo.caimi-inc.com/nexus/content/groups/public-third/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>wacai-public</id>
          <url>http://repo.caimi-inc.com/nexus/content/groups/public/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </pluginRepository>
        <pluginRepository>
          <id>wacai-third</id>
          <url>http://repo.caimi-inc.com/nexus/content/groups/public-third/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </pluginRepository>
      </pluginRepositories>
    </profile>
    <profile>
      <id>personal</id>
      <repositories>
        <repository>
          <id>aliyun-public</id>
          <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>aliyun-public</id>
          <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
          </snapshots>
        </pluginRepository>
      </pluginRepositories>
    </profile>
    <profile>
      <id>sonar</id>
      <properties>
        <sonar.host.url>http://sonarqube.test.wacai.info</sonar.host.url>
      </properties>
    </profile>
  </profiles>
  <activeProfiles>
    <activeProfile>personal</activeProfile>
  </activeProfiles>
</settings>
```