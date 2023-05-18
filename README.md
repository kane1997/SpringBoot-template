# SpringBoot Project Initial Template

This is a project starter template based on Java SpringBoot, integrating commonly used frameworks and sample codes for mainstream business scenarios.

You can set up the backend of a content website in just 1 minute!!! Plus, you can quickly develop your own projects based on this template.


## Features of the Template

### Mainstream Frameworks & Features

- Spring Boot 2.7.x (super new)
- Spring MVC
- MyBatis + MyBatis Plus for data access (with pagination)
- Spring Boot debugging tools and project processors
- Spring AOP for aspect-oriented programming
- Spring Scheduler for scheduled tasks
- Spring Transaction Annotations

### Data Storage

- MySQL database
- Redis in-memory database
- Elasticsearch search engine
- Tencent Cloud COS object storage

### Utility Classes

- Easy Excel for spreadsheet handling
- Hutool utility library
- Gson parsing library
- Apache Commons Lang3 utility class
- Lombok Annotations

### Business Features

- Spring Session Redis for distributed login
- Global request/response interceptor (for logging)
- Global exception handler
- Custom error codes
- Encapsulation of a common response class
- Swagger + Knife4j for API documentation
- Custom permission annotations + global validation
- Global CORS handling
- Solution for loss of precision with long integers
- Multi-environment configuration


## Business Functions

- Provides example SQL (user, post, post likes, post collection table)
- User login, registration, logout, update, retrieval, permission management
- Post creation, deletion, editing, updating, database retrieval, ES flexible retrieval
- Post likes, cancel likes
- Post collection, cancel collection, retrieval of collected posts
- Post full sync ES, incremental sync ES scheduled tasks
- Supports login via WeChat Open Platform
- Supports WeChat Official Account subscription, message sending/receiving, menu setting
- Supports file upload for different businesses

### Unit Tests

- JUnit5 unit tests
- Example unit test classes

### Architectural Design

- Rational layering


## Quick Start

> All places that need to be modified are marked with `todo`, making it easy for everyone to find the modification points~

### MySQL Database

1) Modify the database configuration in `application.yml` to your own:

```yml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/my_db
    username: root
    password: 123456
 ```

2）Execute the database statements in sql/create_table.sql to automatically create the database and tables

3）Start the project, access http://localhost:8101/api/doc.html to open the API documentation, you can test the API online without writing a front end~

![](doc/swagger.png)

### Redis Distributed Login

1) Modify the Redis configuration in `application.yml` to your own:

```yml
spring:
  redis:
    database: 1
    host: localhost
    port: 6379
    timeout: 5000
    password: 123456
```

2) Modify the session storage method in `application.yml`:

```yml
spring:
  session:
    store-type: redis
```

3) Remove the exclude parameter in the `@SpringBootApplication` annotation at the start of the `MainApplication` class:

Before modification:

```java
@SpringBootApplication(exclude = {RedisAutoConfiguration.class})
```

After modification:

```java
@SpringBootApplication
```

### Elasticsearch Search Engine

1) Modify the Elasticsearch configuration in `application.yml` to your own:

```yml
spring:
  elasticsearch:
    uris: http://localhost:9200
    username: root
    password: 123456
```

2) Copy the contents of the `sql/post_es_mapping.json` file and create an index through Elasticsearch's API or Kibana Dev Tools (equivalent to creating a database table):

```
PUT post_v1
{
 Parameters are in the sql/post_es_mapping.json file
}
```

If you are not familiar with this step, you need to supplement your knowledge of Elasticsearch or search it up on your own~

3) Enable the synchronization task to sync the posts in the database to Elasticsearch

Find the `FullSyncPostToEs` and `IncSyncPostToEs` files in the job directory, remove the comment on the `@Component` annotation, and run the program again to trigger synchronization:

```java
// todo Uncomment to enable the task
//@Component
```
