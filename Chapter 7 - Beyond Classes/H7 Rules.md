
## Interfaces

* Many modifiers are implicit, they don't have to be declared. An interface is always abstract as are the methods in it. The variables are always public static final. 
	* Not required to define any methods.
	* When a class implements an interface, the method in the interface is implicitly public, but the implemented method on the class must be declared public explicitly.
	* When an interface implements another interface, 'extends' is used.
	* Interfaces cannot have private or protected instance variables as the compiler will insert public which conflicts with that.
	* Next to abstract methods and constants, an interface can have the following members:
		* Default method (has a body and may be optionally overridden in class implementing the interface)
		* Static method
		* Private method
		* Private static method

## Default method
* You can have multiple default methods in an interface.
* Default methods can only be declared in interfaces, must have a method body and are implicitly public. It cannot be marked abstract, final or static. 
* A default method can be overridden by an implementing class.
* If a class inherits two or more default methods with the same method signature, then the class must override the method.

## Static methods
- A static method must be marked with the static keyword and include a method body. You can’t omit the body in static methods in classes either.
- A static method without an access modifier is implicitly public.
- A static method cannot be marked abstract or final.
- A static method is not inherited and cannot be accessed in a class implementing the interface without a reference to the interface name. They can be accessed without an instance of a class. A class does not inherit static methods, so you should reference them by the interface.

## Private and private static methods
- A private interface method must be marked with the private modifier and include a method body.
- A private static interface method may be called by any method within the interface definition.
- A private interface method may only be called by default and other private non-static methods within the interface.

Key points:
- Treat abstract, default, and non-static private methods as belonging to an instance of the interface.
- Treat static methods and variables as belonging to the interface class object.
- All private interface method types are only accessible within the interface declaration.****

## Enums
* Each enum value has a corresponding int value listed in the order they are declared, starting from 0. You can’t compare an int and enum value directly.
* When using enums in switch expressions, you must use the value directly as the case.
* Every enum constant is static. 
* As opposed to simple enums, you also have complex enums. 
* When complex enum, semicolon after list is required
- An enum can implement an interface as this just requires overriding the abstract methods. 
- Whether simple or complex enum, the list of values comes first.

It is a special type of class. Here’s what happens under the hood: 
- Each enum constant is effectively an instance of the Season enum type. Think of them as predefined instances of the Season class.
- These instances are created automatically when the enum type is initialized. The Java runtime ensures that each enum constant is instantiated once and only once.
- Enum constants can have fields, methods, and constructors just like regular classes. Each constant can have its own set of behaviors and properties.

**When designing an enum, the values should be immutable.**

## Sealed classes
An enum with many constructors, fields, and methods may start to resemble a full-featured class. What if we could create a class but limit the direct subclasses to a fixed set of classes? Enter sealed classes! A sealed class is a class that restricts which other classes may directly extend it.

```java
public sealed class Bear permits Kodiak, Panda {}
```

non-sealed: applied to a class or interface that extends a sealed class, indicating that it can be extended by unspecified classes.

Rules:
- A sealed class needs to be declared (and compiled) in the same package or named module as its direct subclasses.
- When you permit a class to extend a sealed class, the subclass **must** extend that class otherwise the compiler generates an error.
- **Every class that directly extends a sealed class must specify exactly one of the following three modifiers: final, sealed, or non-sealed.** 
- Final just works as with regular classes preventing other classes to extend. Using sealed again, just means the same but other classes are allowed, so there can be **indirect subclasses**. The non-sealed modifier is used to open a sealed parent class to potentially unknown subclasses. 
- You can sometimes omit the permits keyword if the classes are in the same file. It is REQUIRED if classes are in separate files. This rule also applies to nested classes. 
- When all of your subclasses are nested, we strongly recommend omitting the permits class part.

## **Encapsulating Data with Records (primarily used for transferring data)**
The compiler inserts a lot of boilerplate code into records, but there is a bonus; it provides useful implementations of the Object methods equals(), hashCode(), and toString(). The compiler does the following:
- It creates a constructor for you with the parameters in the same order in which they appear in the record declaration.
- For each field, it also creates an accessor as the field name, plus a set of parentheses. Instead of getName(), it will be name().

The println method will call the toString method automatically on any object passed to it. The default implementations of the bonus methods are:
- equals(): a method to compare two elements that returns true if each field is equal in terms of equals()
- hashCode(): A consistent hashCode() method using all of the fields
- toString(): a toString implementation that prints each field of the record in a convenient, easy-to-read format.

It is legal to have a record without any fields.
* Records don't have setters. Every field is inherently final and cannot be modified after declared in the constructor. interfaces are implicitly abstract, records are implicitly final.
* You can't extend or inherit a record.
* long constructor <> compact constructor
	* It requires no parameters. 
	* Long constructor is implicitly called at the end of compact constructor
	* Compact constructors can modify the constructor parameters, they cannot modify the fields of the record

Records actually support many of the same features as a class, for example:
- Overloaded and compact constructors
- Instance methods including overriding any provided methods (accessors, equals(), hashCode(), and toString())
- Nested classes, interfaces, annotations, enum, and records
- Static fields

## Nested classes
A nested class is a class that is defined within another class. It comes in four flavors:
- Inner class: A non-static type defined at the member level of a class
- Static nested class: A static type defined at the member level of a class
- Local class: A class defined within a method body
- Anonymous class: A special case of a local class that does not have a name

**Inner Class**
- Because they are not top-level types, they can use any of the four access levels, not just public and package access. Can be declared: public, protected, package or private
- Can extend a class and implement interfaces
- Can be marked abstract or final
- Can access members of the outer class, including private members

**Static nested class**
Unlike an inner class, a static nested class can be instantiated without an instance of the enclosing class. The tradeoff, though, is that it can’t access instance variables or methods declared in the outer class.

**Local Class**
You can only create instances of it from within the method where the local class is created. They go out of scope when the method returns. They have the following properties:
- They do not have an access modifier.
- They can be declared final or abstract.
- They have access to all fields and methods of the enclosing class (when defined in an instance method).
- They can only access final and effectively final variables.

**Anonymous Class**
An anonymous class is a specialized form of a local class that does not have a name. Anonymous class must extend an existing class or implement an existing interface. They are useful when you have a short implementation that will not be used anywhere else.

## Understanding polymorphism
A Java object may be accessed using:
- A reference with the same type as the object
- A reference that is a superclass of the object
- A reference that defines an interface the object implements or inherits

A cast is not required if the object is being reassigned to a supertype or interface of the object. Once the object has been assigned to a new reference type, only the methods and variables available to that reference type are callable on the object without an explicit cast.

In Java, all objects are accessed by reference, so as a developer you never have direct access to the object itself. Regardless of the type of the reference you have for the object in memory, the object itself doesn’t change. The following rules apply:
- The type of the object determines which properties exist within the object in memory.
- The type of the reference to the object determines which methods and variables are accessible to the Java program.

**Casting**
When casting objects, you do not need a cast operator if casting to an inherited supertype. This is referred to as an implicit cast. If you want to access a subtype of the current reference, you need to perform an explicit cast with a compatible type.

Remember, interfaces support multiple inheritance, which limits what the compiler can reason about them. While a given class may not implement an interface, it’s possible that some subclass may implement the interface.

This limitation aside, the compiler can enforce one rule around interface casting. The compiler does not allow a cast from an interface reference to an object reference if the object type cannot possibly implement the interface, such as if the class is marked final. The compiler then recognizes that there are no possible subclasses of Wolf capable of implementing the dog interface.

## Overriding methods vs method hiding
While method overriding replaces the method everywhere it is called, static method and variable hiding do not. Strictly speaking, hiding members is not a form of polymorphism since the methods and variables maintain their individual properties. Unlike method overriding, hiding members is very sensitive to the reference type and location where the member is being used.  

When hiding a static method, the result is that calling that method in either of the classes returns a different value than calling it in the other, even if the underlying object is the same. Contrast this with overriding a method, where it returns the same value for an object regardless of which class it is called in. 

Besides the location, the reference type can also determine the value you get when you are working with hidden members. 

In practice, overriding methods is the cornerstone of polymorphism and an extremely powerful feature. Don’t hide members in practice. The value of the variable or method can change depending on what reference is used, making your code very confusing, difficult to follow, and challenging for others to maintain. This is further compounded when you start modifying the value of the variable in both the parent and child methods, since it may not be clear which variable you’re updating.