
## Table of Contents
1. [Scenarios Where finally Block Can Be Skipped](#1-can-finally-block-can-skip)
### 1. **Scenarios Where finally Block Can Be Skipped**
 
When the JVM Terminates Abruptly
If the Java Virtual Machine (JVM) is forcibly terminated (e.g., using System.exit()), the finally block will not execute.


```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("Try block");
            System.exit(0); // Exits the program
        } finally {
            System.out.println("Finally block");
        }
    }
}
```
### 2. **Abstract**
**Defination :** Abstraction is a process of hiding the implementation details and showing only functionality to the user.
**RULE**
A class that is declared with the abstract keyword is known as an abstract class in Java. It can have abstract and non-abstract methods (method with the body).
