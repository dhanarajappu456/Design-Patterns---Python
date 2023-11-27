
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


Visitor pattern also have <Strong><i> double dispatching concept</i> </Strong> , that is the method invoked depend on the 2 types of object in  first is the
1)the visitor object on which the visit called depend on the concrete implemention of visitor passed as argument to the accept method of element <br> 
2) and also the visitable object on which the actual visit method get called depend on the concerete implementation of visitable intrtface that is passed to visit method of visitor
```

from abc import ABC, abstractmethod

#interface for all the Elements that the visitor can visit, and there by perform the operation on each element 

class IVisitable(ABC):
  
  @abstractmethod
  def accept(self,visitor):
    pass

#the element (node in the heirarchy)
class Element(IVisitable):
  
  def __init__(self,name,parent=None):
    self.name  = name
    #keeps a collection of descendants
    self.elements = set()
    if parent:
      parent.elements.add(self)
  
  #recursively allows to visit all the descendant
  def accept(self,visitor):
    
    for element in self.elements:
      
      element.accept(visitor)
    
    visitor.visit(self)
  
    

#interface for the visitor(which contain the operation to perform  - here visit operation, which 
#print the name of each element )
class IVisitor(ABC):
  
  def visit(self,element):
    pass

class PrintNameVisitor(IVisitor):
  #the operation that visitor perform on each element
  def visit(self,element):
    
    print(f"element {element.name}")

#client 
#create the elements in the heirarchy 
element_a =Element("A")
element_b =Element("B",element_a)
element_c =Element("C",element_a)
element_d =Element("D",element_b)

#create the visitor
visitor = PrintNameVisitor()

#visiting each element or element accepting the visitor to execute the operation on it 
element_a.accept(visitor)

'''
prints 

element D
element B
element C
element A
'''


    
  
    
    
