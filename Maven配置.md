# maven如何配置阿里云仓库
## 方式一 ：全局配置
可以添加阿里云的镜像到maven的setting.xml配置中，这样就不需要每次在pom中，添加镜像仓库的配置，在mirrors节点下面添加子节点：  
1. 找到Maven安装路径，打开conf文件夹，找到settings.xml  
2. 在settings.xml中在mirrors节点下加入如下子节点
```xml
<mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>central</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

## 方式二：单项目配置
单项目配置时，需要修改pom文件。pom文件中，没有mirror元素。在pom文件中，通过覆盖默认的中央仓库的配置，实现中央仓库地址的变更。

1. 打开项目的pom.xml
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.test</groupId>
    <artifactId>conifg</artifactId>
    <packaging>war</packaging>
    <version>0.0.1-SNAPSHOT</version>

    <repositories>
        <repository>
            <id>central</id>
            <name>aliyun maven</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
            <layout>default</layout>
            <!-- 是否开启发布版构件下载 -->
            <releases>
                <enabled>true</enabled>
            </releases>
            <!-- 是否开启快照版构件下载 -->
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>

</project>
```
注：Maven默认中央仓库的id 为 central。id是唯一的。因此使用< id>central< /id>覆盖了默认的中央仓库。

---