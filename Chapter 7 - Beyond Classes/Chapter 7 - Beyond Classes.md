# **Interface**

An **Interface in Java** programming language is defined as an abstract type used to specify the behavior of a class. An interface in Java is a blueprint of a behavior. A Java interface contains static constants and abstract methods. It is used to achieve abstraction and multiple inheritances in Java using Interface.

```java
public abstract interface CanBurrow {

    public abstract Float getSpeed(int age); 

    public static final int MINIMUM_DEPTH = 2;
}
```

Interfaces are not part of instance initialization. 

The following rules are applicable:
* Most of the modifiers in the code above are implicit, they don’t have to be declared. An interface is always abstract as are the methods in it. The variables are always public static final.
* Interfaces are not required to define any methods.
* When a class implements an interface, the method in the interface is implicitly public, but the implemented method on the class **must** be declared public explicitly.
* The implements keyword is used with interfaces, but when an interface implements another interface, 'extends' is used.
* If an abstract class implements an interface, it is not required to implement any of the abstract methods it inherits, but the concrete class extending the abstract class is required to do so.
* Interfaces cannot have private or protected instance variables as the compiler will insert public which conflicts with that.

Java supports inheriting two abstract methods that have compatible method declarations. By compatible, we mean a method can be written that properly overrides both inherited methods, e.g. by using covariant return types.

Next to abstract methods and constants, an interface can have the following members:
- Default method (has a body and may be optionally overridden in class implementing the interface)
- Static method
- Private method
- Private static method
## Default method
* You can have multiple default methods. It cannot be marked abstract, final or static.
* If a class inherits two or more default methods with the same method signature, then the class must override the method.

## Static methods
* A static method must be marked with the static keyword and include a method body. You can’t omit the body in static methods in classes either.
* A static method without an access modifier is implicitly public.
* A static method cannot be marked abstract or final.
* A static method is not inherited and cannot be accessed in a class implementing the interface without a reference to the interface name.

They can be accessed without an instance of a class. A class does not inherit static methods, so you should reference them by the interface.

```java
public class Bunny implements Hop {

public void printDetails() {
	getJumpHeight(); // does not compile as not inherited
	Hop.getJumpHeight(); // CORRECT
}

}```

## Private and private static methods
They were added primarily to reduce code duplication. They can only be used in the interface in which they are declared. The benefits are:

- Hiding implementation details from classes that implement the interface achieving encapsulation
- Less duplication and more re-usable code added to interfaces for methods with similar functionality.