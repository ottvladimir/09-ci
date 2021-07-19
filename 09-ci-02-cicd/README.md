# Домашнее задание к занятию "09.02 CI\CD"

## Знакомоство с SonarQube

![SonarQubeimage](IMG_20210719_150451_452.jpg)


## Знакомство с Nexus

### Подготовка к выполнению

```xml 
   <metadata modelVersion="1.1.0">
      <groupId>netology</groupId>
      <artifactId>java</artifactId>
      <versioning>
         <latest>8_282</latest>
         <release>8_282</release>
         <versions>
            <version>8_102</version>
            <version>8_282</version>
         </versions>
         <lastUpdated>20210719042450</lastUpdated>
      </versioning>
   </metadata>
```

### Знакомство с Maven

```xml
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-insta
     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
     <modelVersion>4.0.0</modelVersion>

     <groupId>com.netology.app</groupId>
     <artifactId>simple-app</artifactId>
     <version>1.0-SNAPSHOT</version>
      <repositories>
       <repository>
         <id>my-repo</id>
         <name>maven-public</name>
         <url>http://localhost:8081/repository/maven-public/</url>
       </repository>
     </repositories>
     <dependencies>
        <dependency>
         <groupId>netology</groupId>
         <artifactId>java</artifactId>
         <version>8_282</version>
         <classifier>distrib</classifier>
         <type>tar.gz</type>
       </dependency>
     </dependencies>
   </project>
```
