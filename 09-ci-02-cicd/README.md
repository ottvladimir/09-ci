# Домашнее задание к занятию "09.02 CI\CD"

## Знакомоство с SonarQube

image


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

### Подготовка к выполнению

1. Скачиваем дистрибутив с [maven](https://maven.apache.org/download.cgi)
2. Разархивируем, делаем так, чтобы binary был доступен через вызов в shell (или меняем переменную PATH или любой другой удобный вам способ)
3. Проверяем `mvn --version`
4. Забираем директорию [mvn](./mvn) с pom

### Основная часть

1. Меняем в `pom.xml` блок с зависимостями под наш артефакт из первого пункта задания для Nexus (java с версией 8_282)
2. Запускаем команду `mvn package` в директории с `pom.xml`, ожидаем успешного окончания
3. Проверяем директорию `~/.m2/repository/`, находим наш артефакт
4. В ответе присылаем исправленный файл `pom.xml`

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
