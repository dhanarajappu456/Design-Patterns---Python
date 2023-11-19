
Your object structure inside an application may be complicated and varied. A good example is what
could be created using the Composite structure.<br>
The objects that make up the hierarchy of objects, can be anything and most likely complicated to
modify as your application grows.<br>
Instead, when designing the objects in your application that may be structured in a hierarchical
fashion, you can allow them to implement a Visitor interface. <br>

 Visitor design pattern is a behavioral pattern that allows you to define a new operation without changing the classes of the elements on which it operates.<br>
 It is useful when you have a set of classes with a common interface, and you want to perform operations on these classes that are not part of their common interface.<br>

The Visitor pattern involves defining a visitor class that implements the operations to be performed on the elements, and then each element class accepts a visitor,<br>
allowing it to perform the operation on the element.
