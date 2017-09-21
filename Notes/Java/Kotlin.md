# Kotlin使用笔记

## Kotlin in Idea

Maven构建时，需要添加以下插件，否则需要手动build。

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <executions>
    <!-- Replacing default-compile as it is treated specially by maven -->
    <execution>
      <id>default-compile</id>
      <phase>none</phase>
    </execution>
    <!-- Replacing default-testCompile as it is treated specially by maven -->
    <execution>
      <id>default-testCompile</id>
      <phase>none</phase>
    </execution>
    <execution>
      <id>java-compile</id>
      <phase>compile</phase>
      <goals>
        <goal>compile</goal>
      </goals>
    </execution>
    <execution>
      <id>java-test-compile</id>
      <phase>test-compile</phase>
      <goals>
        <goal>testCompile</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

