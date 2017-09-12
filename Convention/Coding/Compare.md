# 一些比较示例

#### 1.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd" >
<generatorConfiguration>
	<classPathEntry location="D://maven//repos//mysql//mysql-connector-java//5.1.33//mysql-connector-java-5.1.33.jar" />
	<context id="context" >
        <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://10.1.1.62:3306/cif" userId="admin" password="westos" />
        <javaModelGenerator targetPackage="com.qjdchina.cif.model" targetProject="cif.model" />
        <sqlMapGenerator targetPackage="com.qjdchina.cif.dao.mapper" targetProject="cif.dao/src/main/resources/" />
        <javaClientGenerator targetPackage="com.qjdchina.cif.dao.mapper"  targetProject="cif.dao" type="XMLMAPPER" />
 		<table tableName="cif_rel_c_s" enableCountByExample="false" domainObjectName="RelationBCS" enableDeleteByExample="false" enableSelectByExample="false" enableUpdateByExample="false" />
	</context>

</generatorConfiguration>
```

vs

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>

    <classPathEntry
            location="/Users/qjdchina/.m2/repository/mysql/mysql-connector-java/5.1.43/mysql-connector-java-5.1.43.jar"/>

    <context id="demo" targetRuntime="MyBatis3">

        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/clms?useSSL=false"
                        userId="clms"
                        password="clms_1">
        </jdbcConnection>

        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>

        <javaModelGenerator targetPackage="io.ushi.springboot.model" targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="true"/>
        </javaModelGenerator>

        <sqlMapGenerator targetPackage="io.ushi.springboot.dao.mapper" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>

        <javaClientGenerator type="XMLMAPPER" targetPackage="io.ushi.springboot.dao.mapper"
                             targetProject="src/main/java">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>

        <table schema="clms" tableName="Document" domainObjectName="Document" enableSelectByExample="false"
               enableDeleteByExample="false" enableCountByExample="false" enableUpdateByExample="false">
        </table>

    </context>

</generatorConfiguration>
```

