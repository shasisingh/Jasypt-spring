# Spring Boot Password Encryption using Jasypt


Jasypt is a Java library which helps developers with basic encryption in configurations without much effort or in-depth knowledge of encryption implementation. Please go through http://www.jasypt.org/ for detailed information.

><plugin>
>    <groupId>com.github.ulisesbocchio</groupId>
>    <artifactId>jasypt-maven-plugin</artifactId>
>    <version>3.0.3</version>
></plugin>

><dependency>
>    <groupId>com.github.ulisesbocchio</groupId>
>    <artifactId>jasypt-spring-boot-starter</artifactId>
>    <version>3.0.3</version>
></dependency>
>

## Installation
then run the below specify the path of the file(application.yml) in the command like this:

```sh
mvn jasypt:encrypt -Djasypt.encryptor.password=acdc123 -Djasypt.plugin.path="file:src/main/resources/application.yml"
```

For application.properties [ default]

```sh
mvn jasypt:encrypt -Djasypt.encryptor.password=acdc123
```
To decrypt- default
```sh
mvn jasypt:decrypt -Djasypt.encryptor.password=acdc123 
```

To decrypt- application.yml
```sh
mvn jasypt:decrypt -Djasypt.encryptor.password=acdc123 -Djasypt.plugin.path="file:src/main/resources/application.yml"
```

Suppose that you want to encrypt username and password of a Spring data source in the following application.properties file:
```sh
spring.datasource.username = root
spring.datasource.password = Password
```
STEP 01:

First, wrap the values password inside DEC() as shown below:
```sh
spring.datasource.username = root
spring.datasource.password = DEC(Password)
```
Here, DEC() is a placeholder that tells Jasypt what to encrypt, and the remaining values are untouched.

STEP 02:
```sh
mvn jasypt:encrypt -Djasypt.encryptor.password=acdc123 -Djasypt.plugin.path="file:src/main/resources/application.yml" -Djasypt.encryptor.algorithm=PBEWITHHMACSHA512ANDAES_256 -Djasypt.encryptor.iv-generator-classname=org.jasypt.iv.RandomIvGenerator

```

Then it will replace the DEC() placeholders in the application.properties file with the encrypted value:

```sh
spring.datasource.password = ENC(llo8Tfwc2cBLNAzjkksTk9dBj8tIwT3ZUHDQoFQm88D85qJTTY9doPcmQiN/Emtd)
```
STEP 03:

If you want to see original value

```sh
mvn jasypt:decrypt -Djasypt.encryptor.password=acdc123 -Djasypt.plugin.path="file:src/main/resources/application.yml" -Djasypt.encryptor.algorithm=PBEWITHHMACSHA512ANDAES_256 -Djasypt.encryptor.iv-generator-classname=org.jasypt.iv.RandomIvGenerator
```
Now to run the Spring Boot application in any IDE, you need to pass VM argument as below

> Note: -Djasypt.encryptor.password=acdc123

