Example Spring Boot Application
==========

## Environment Setup

Reference:

[Develop your Spring Boot application with Visual Studio Code](https://careers.edicomgroup.com/develop-your-spring-boot/)

### Prerequisites

1. Java
    
    ```bash
    $ java -version
    java version "1.8.0_271"
    Java(TM) SE Runtime Environment (build 1.8.0_271-b09)
    Java HotSpot(TM) 64-Bit Server VM (build 25.271-b09, mixed mode)
    ```
    
2. Maven
    
    ```bash
    choco install maven
    ```
    
3. Visual Studio Code

### Extensions

1. [Language Support for Java(TM) by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.java)
    
    Need couple of minutes to install, please wait patiently.
    
2. [Debugger for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)
3. [Spring Boot Tools](https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-spring-boot)
4. [Spring Boot Dashboard](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard)
5. [Spring Initializr Java Support](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr) (to add dependencies)

**Errors**

- Gradle error → Delete folder `C:\…\.gradle\wrapper\dists\gradle-7.5.1-bin`
    
    ```bash
    Could not install Gradle distribution from 'https://services.gradle.org/distributions/gradle-7.5.1-bin.zip'  
    Timeout of 120000 reached waiting for exclusive access to file "C:\…\.gradle\wrapper\dists\gradle-7.5.1-bin"
    ```
    
- Install failure for 3 & 4 → Download VSIX from Marketplace and install via VSIX

## Project Setup

### Initialize Spring Boot Project

1. Go to [Spring Initializr](https://start.spring.io/)
    - Configuration (Example): *Gradle, Java, 2.7.5 (latest stable), Jar, Java 17*
        ![picture 1](https://i.imgur.com/6TnM1H8.png) 
2. Add dependencies 
    - Spring Web
    - Spring Data JPA
    - MySQL Driver
    - Lombok
3. Generate and Download `.zip`
4. Open with VS Code

### Run

- Use Run and Debug to Debug the application
- After making some changes, click restart to see the changes

### Add API for root `"/"`

Add `@RestController` and API for `"/"`

```java
@RestController
@SpringBootApplication
public class DemoApplication {
	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
	@RequestMapping(value="/", method=RequestMethod.GET)
	public String helloWorld() {
		return "Hello World";
	}	
}
```

## Database Setup

### Extensions

- JPA
- hibernate-validator (for JPA)
- Lombok: Reduce getter & setter boilerplate code with `@Getter @Setter`
    - [Java - 五分鐘學會 Lombok 用法](https://kucw.github.io/blog/2020/3/java-lombok/)
    

### Setup Database MySQL

- Prerequisite: Have SQL installed.
    - For example, with XAMPP.

```sql
# Log in to mysql
mysql -u root -p

# Creates the new database
mysql> create database springboot_db;

# Creates the user
mysql> create user 'springuser'@'%' identified by 'ThePassword';

# Gives all privileges to the new user on the newly created database
mysql> grant all on springboot_db.* to 'springuser'@'%';
```

### Connect Springboot with Database

Add `[application.properties](http://application.properties)` or `application.yaml` to `src/main/resources`

```yaml
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/springboot_db
spring.datasource.username=springuser
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
#spring.jpa.show-sql: true
```
