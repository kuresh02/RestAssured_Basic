
### RestAssured Basic README File Description

The README file for a basic RestAssured project should provide a comprehensive guide to understand, set up, and run the project. Here's a detailed template for such a README file:

---

# RestAssured Basic Project
It is a Project regarding RestAssured_Basic Testing
## Overview

This project demonstrates the basics of API testing using RestAssured. RestAssured is a Java library for testing REST APIs, making it easy to validate and interact with RESTful services.

## Prerequisites

Before you begin, ensure you have the following installed:
- Java JDK (version 8 or higher)
- Maven
- An IDE (e.g., IntelliJ IDEA, Eclipse)

## Project Structure

The project follows a standard Maven project structure:

```
RestAssured_Basic/
├── src/
│   ├── main/
│   │   └── java/
│   └── test/
│       └── java/
│           └── com/
│               └── example/
│                   └── api/
│                       ├── tests/
│                       │   └── BasicApiTest.java
│                       └── utils/
│                           └── ApiUtils.java
├── pom.xml
└── README.md
```

- **src/main/java**: Contains the main application code (if any).
- **src/test/java**: Contains the test code.
  - **tests**: Contains test classes.
  - **utils**: Contains utility classes for API testing.
- **pom.xml**: Maven configuration file.

## Getting Started

### Clone the Repository

```sh
git clone https://github.com/your-username/RestAssured_Basic.git
cd RestAssured_Basic
```

### Import the Project

1. Open your IDE (e.g., IntelliJ IDEA, Eclipse).
2. Import the project as a Maven project.

### Maven Dependencies

The `pom.xml` file includes the necessary dependencies for RestAssured:

```xml
<dependencies>
    <!-- RestAssured -->
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>rest-assured</artifactId>
        <version>4.4.0</version>
        <scope>test</scope>
    </dependency>

    <!-- TestNG -->
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.4.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JSON Path -->
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>json-path</artifactId>
        <version>4.4.0</version>
        <scope>test</scope>
    </dependency>

    <!-- XML Path -->
    <dependency>
        <groupId>io.rest-assured</groupId>
        <artifactId>xml-path</artifactId>
        <version>4.4.0</version>
        <scope>test</scope>
    </dependency>

    <!-- Maven Surefire Plugin -->
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.22.2</version>
    </plugin>
</dependencies>
```

### Running the Tests

You can run the tests using Maven:

```sh
mvn test
```

Or directly from your IDE by right-clicking on the test class and selecting "Run".

## Writing Tests with RestAssured

### Basic Example

Here is an example of a simple test class (`BasicApiTest.java`) that demonstrates how to use RestAssured:

```java
package com.example.api.tests;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.testng.annotations.Test;

import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class BasicApiTest {

    @Test
    public void testGetEndpoint() {
        given().
            baseUri("https://jsonplaceholder.typicode.com").
        when().
            get("/posts/1").
        then().
            statusCode(200).
            body("userId", equalTo(1)).
            body("id", equalTo(1)).
            body("title", notNullValue());
    }

    @Test
    public void testPostEndpoint() {
        given().
            baseUri("https://jsonplaceholder.typicode.com").
            header("Content-Type", "application/json").
            body("{ \"title\": \"foo\", \"body\": \"bar\", \"userId\": 1 }").
        when().
            post("/posts").
        then().
            statusCode(201).
            body("title", equalTo("foo")).
            body("body", equalTo("bar")).
            body("userId", equalTo(1));
    }
}
```

### Utility Class

An example of a utility class (`ApiUtils.java`) that provides helper methods for API tests:

```java
package com.example.api.utils;

import io.restassured.RestAssured;
import io.restassured.response.Response;

public class ApiUtils {

    public static Response get(String baseUri, String endpoint) {
        return RestAssured.given()
                .baseUri(baseUri)
                .when()
                .get(endpoint);
    }

    public static Response post(String baseUri, String endpoint, String body) {
        return RestAssured.given()
                .baseUri(baseUri)
                .header("Content-Type", "application/json")
                .body(body)
                .when()
                .post(endpoint);
    }
}
```

## Best Practices

- Use utility classes to avoid code duplication.
- Parameterize test data to make tests reusable.
- Use assertions to validate API responses.
- Organize tests in a logical structure.

## Conclusion

This project provides a basic setup for API testing using RestAssured. It covers the essentials to get started with writing and running tests. For more advanced features and configurations, refer to the official RestAssured documentation.

---

This README template should help you set up a RestAssured project, understand its structure, and provide clear instructions on how to write and run API tests.
