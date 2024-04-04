Interfaces
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