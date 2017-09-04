# Javadoc

## Maven配置

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-javadoc-plugin</artifactId>
      <version>2.9</version>
      <configuration>
        <locale>en_US</locale>
        <doclet>org.umlgraph.doclet.UmlGraphDoc</doclet>
        <!-- <docletPath>/path/to/UmlGraph.jar</docletPath> -->
        <docletArtifact>
          <groupId>org.umlgraph</groupId>
          <artifactId>umlgraph</artifactId>
          <version>5.6.6</version>
        </docletArtifact>
        <additionalparam>-views -all -collapsible</additionalparam>
        <useStandardDocletOptions>true</useStandardDocletOptions>
      </configuration>
    </plugin>
  </plugins>
</build>
```

### 两个配置关键

1. 官方提供的umlgraph版本只到5.1，需要5.5.8-SNAPSHOT版本，该解决了`Warning, could not find a line that matches the pattern`问题，下载地址：[Link](https://oss.sonatype.org/content/repositories/snapshots/org/umlgraph/umlgraph/5.5.8-SNAPSHOT/)

   下载后，通过命令`mvn install:install-file -Dfile=umlgraph-5.5.8-20120530.182844-4.jar -DpomFile=umlgraph-5.5.8-20120530.182844-4.pom`安装到本地仓库。

   *** 补充，5.6.6已解决，并提供官方下载。

2. 一定要配置`<locale>en_US</locale>`，否则生成的javadoc中，`class`关键字会变成`类`，Interface、Enum亦如此，会导致umlgraph无法解析，同样会报`could not find a line that matches the pattern`错误。


### 参数说明

#### -collapsible

折叠，默认不显示UML图，点击`Show UML class diagram`显示。

### 源代码参考

[UMLGraph@github](https://github.com/dspinellis/UMLGraph)


## 安装graphviz

### For Mac

#### 使用brew cask

1. Press `Command+Space` and type **Terminal** and press **enter/return** key.
2. Run in Terminal app:
```shell
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null ; brew install caskroom/cask/brew-cask 2> /dev/null
```
   	and press **enter/return** key. Wait for the command to finish.
3. Run:
   `brew cask install graphviz`


#### 直接使用brew

需要编译

## 遗留问题

package说明页还无法关联，提示`Warning, could not find a line that matches the pattern '.*</[Hh]2>.*'.`，估计也和解析格式有关。

*** 5.6.6中已解决

注解类（Annotation Type）无法解析。

可生成链接，点击后显示。（在官方有说明） => collapsible参数