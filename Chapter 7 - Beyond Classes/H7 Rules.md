
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