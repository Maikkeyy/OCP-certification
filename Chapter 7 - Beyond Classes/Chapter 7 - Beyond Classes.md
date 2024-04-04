
# Chapter 7 - Beyond Classes
## **Interface**

An Interface in Java programming language is defined as an abstract type used to specify the behavior of a class. An interface in Java is a blueprint of a behavior. A Java interface contains static constants and abstract methods. It is used to achieve abstraction and multiple inheritances in Java using Interface.

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

Het is gewoon handig, want stel je wilt in meerdere default methods hetzelfde stukje code uitvoeren, dan kun je daar nu gewoon een private methode voor aanmaken waarin dat stukje code centraal staat. Just handy! 

Rules: 
- A private interface method must be marked with the private modifier and include a method body.
- A private static interface method may be called by any method within the interface definition.
- A private interface method may only be called by default and other private non-static methods within the interface.

Private method is alleen beschikbaar voor non-static methods en private static is voor elke methode soort beschikbaar.

Key points:
- Treat abstract, default, and non-static private methods as belonging to an instance of the interface.
- Treat static methods and variables as belonging to the interface class object.
- All private interface method types are only accessible within the interface declaration.

## **Enums (special kind of class)**

Fixed set of constants. Using an enum is much better than using a bunch of constants because it provides type-safe checking. With numeric or String constants, you can pass an invalid value and not find out until runtime. With enums it is impossible to create an invalid enum value without introducing a compiler error.

For example, considering the months, if we have constants as int (static final int JANUARY = 1) then a variable or method parameter must be declared as int and would accept any integer value, valid or not(e.g. setMonth(123) or setMonth(0)).

If we have an enum, then the variables or method parameters can only accept its values - errors (wrong constants) can be detected at compile time (exception: null which can also be assigned/passed instead of an enum, like any reference type).

Each enum value has a corresponding int value listed in the order they are declared, starting from 0. You can’t compare an int and enum value directly:

```If (Season.SUMMER == 2) {} // DOES NOT COMPILE```

When using enums in switch expressions, you must use the value directly as the case:

Case WINTER
Case Season.WINTER // DOES NOT COMPILE

While a simple enum is composed of just a list of values, we can define a complex enumeration with additional elements. In the code below, the values are enum constants, not strings (which you probably assumed). 

enum Season {
    WINTER,
    SPRING,
    SUMMER,
    FALL
}

Every enum constant is static.

