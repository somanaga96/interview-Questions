 ## Table of Contents
1. [Status code and body validatio](#1-status-code-body)
2. [Common Selenium Exceptions](#2-common-selenium-exceptions)

### 1 **Status code and body validation**

Ans : 
```java
RestAssured.given()
                .baseUri("https://catfact.ninja")
                .get("/fact")
                .then()
                .statusCode(200)
                .body("length", equalTo(11));
```
