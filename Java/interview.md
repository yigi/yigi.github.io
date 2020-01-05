encapsulation, abstraction, inheritance, and polymorphism

### What is method overloading in OOP or Java?
When we have multiple methods with the same name but different functionality then it's called method overloading. For example. System.out.println()

### What is method overriding in OOP or Java?
In order for method overriding, we need Inheritance and Polymorphism, as we need a method with the same signature in both superclass and subclass.

### The difference between method overloading and overriding?
Several differences but the most important one is that method overloading is resolved at compile time and method overriding is resolved at runtime.

### Can we override static method in Java?
No, you cannot override a static method because it's not bounded to an object. Instead, static methods belong to a class and resolved at compile time using the type of reference variable. But, Yes, you can declare the same static method in a subclass, that will result in method hiding i.e. if you use reference variable of type subclass then new method will be called, but if you use reference variable of superclass than old method will be called. --> you can mark the method private or static, those cannot be overridden.

### What is covariant method overriding in Java?

```java
//without covariant overriding, cast at client side needed 
Date d = new Date(); 
Date clone = (Date) d.clone(); 

//casting required //with covariant method overriding, no client side cast 
Duck duck = new Duck(0xFFFFFF);
Duck copy = duck.clone(); //no casting

```
___________________________________________________________________________________________________________

### What is an abstract class in Java?
An abstract class is a class which is incomplete. You cannot create an instance of an abstract class in Java. They are provided to define default behavior and ensured that client of that class should adore to those contract which is defined inside the abstract class. In order to use it, you must extend and implement their abstract methods. BTW, in Java, a class can be abstract without specifying any abstract method.

```java
abstract class Fruit {
    private Color color;
    private boolean seasonal;

    public Fruit(Color color, boolean seasonal) {
        this.color = color;
        this.seasonal = seasonal;
    }

   /*
    * This is an abstract method, see it doesn't have method body, only declaration
    */
    public abstract void prepare();

    public Color getColor() {
        return color;
    }

    public boolean isSeasonal() {
        return seasonal;
    }
}


/*
 * A concrete class to extend Fruit, since Mango IS-A Fruit
 * extending Fruit is justified. it got all properties of
 * fruit, and it defines how to prepare mango for eating.
 */
class Mango extends Fruit {

    public Mango(Color color, boolean seasonal) {
        super(color, seasonal);
    }

    @Override
    public void prepare() {
        System.out.println("Cut the Mango");
    }
}

```
### What is an interface in Java?

Like a class, an interface can have methods and variables, but the methods declared in an interface are by default abstract (only method signature, no body).  

- Interfaces specify what a class must do and not how. It is the blueprint of the class.

- An Interface is about capabilities like a Player may be an interface and any class implementing Player must be able to (or must implement) move(). So it specifies a set of methods that the class has to implement.

- If a class implements an interface and does not provide method bodies for all functions specified in the interface, then the class must be declared abstract.Since java does not support multiple inheritance in case of class, but by using interface it can achieve multiple inheritance .

- Since java does not support multiple inheritance in case of class, but by using interface it can achieve multiple inheritance .

- The question arises why use interfaces when we have abstract classes?
The reason is, abstract classes may contain non-final variables, whereas variables in interface are final, public and static.

<img align="center" width="670" height="700" src="https://miro.medium.com/max/661/1*vmQhGSTGAeIIsCX0jEPUqg.jpeg">

###  Can we create non static variables in an interface? 

No.We can not create non static variables in an interface. If we try to create non static variables compile time error comes.  Every variable in interface are implicitly public, static, and final.

###  What will happen if we do not initialize variables in Java interface. 

Compile time error will come because by default members will be treated as public static final variables so it expects some value to be initialized. 

### Default Methods

Unlike other abstract methods these are the methods can have a default implementation. If you have default method in an interface, it is not mandatory to override (provide body) it in the classes that are already implementing this interface.

In short, you can access the default methods of an interface using the objects of the implementing classes.

```java
Example
interface MyInterface{
   public static int num = 100;
   public default void display() {
      System.out.println("display method of MyInterface");
   }
}
public class InterfaceExample implements MyInterface{
   public static void main(String args[]) {
      InterfaceExample obj = new InterfaceExample();
      obj.display();
   }
}
```

https://www.journaldev.com/2752/java-8-interface-changes-static-method-default-method

## class Cat extends Animal implements Climb

