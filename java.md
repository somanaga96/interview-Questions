
## Table of Contents
1. [Scenarios Where finally Block Can Be Skipped](#1-can-finally-block-can-skip)
2. [Class and Object](#2-class-and-object)
3. [Abstract](#3-abstract)
4. [DOwnCast and UpCast](#4-Downcast-UpCast)
5. [Encapsulation](#5-encapsulation)
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
### 2. **Class and Object**
1. A class is like a blueprint for a house.
2. An object is like an actual house built using that blueprint

   
### 3. **Abstract**
**Defination :** Abstraction is a process of hiding the implementation details and showing only functionality to the user.
**Eg " : In ATM showing option as Account balance check, money withdraw to end user. But **NOT**  showing the method implementation to end user.

**RULE**

1. A class that is declared with the abstract keyword is known as an abstract class in Java.
2. It can have abstract and non-abstract methods (method with the body).

**Ways to achieve Abstraction**

 There are two ways to achieve abstraction in Java:
1. Using Abstract Class (0 to 100%)
2. Using Interface (100%

Example :
```java
abstract class Bike{  
  abstract void run();  
}  
class Honda4 extends Bike{  
void run(){System.out.println("running safely");}  
public static void main(String args[]){  
 Bike obj = new Honda4();  
 obj.run();  
}  
}
```

### 4. **DownCast and UpCast**
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal animal = new Dog();  // Upcasting

        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;  // Safe downcasting
            dog.sound();  // Output: Dog barks
        } else {
            System.out.println("Not a Dog");
        }
    }
}
```
### 5. **Encapsulation**
Key Points of Encapsulation in Java:


**Private Fields:** Fields (variables) of a class are made private so that they cannot be accessed directly from outside the class.
**Public Getter and Setter Methods:** Public methods (getters and setters) are provided to access and update the values of the private fields in a controlled way.
**Control:** Encapsulation allows you to enforce rules and constraints on how data is set or retrieved. For example, a setter method could ensure that only valid values are assigned to an object's fields.
