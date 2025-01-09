
## Table of Contents
1. [Select Option Without Select Class](#1-Scenarios Where finally Block Can Be Skipped)
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
}```
