#actual abstraction(The Shapes  -Circle and Square ) is seperated from the implementation(
#The implementations- CircleImplentation and SquareImplementation). The Abstracion make use of the composed 
#object of the implementation.

#thus both of them (Abstracion and Implementation)can be developed independently , 
#Similar to Adapter, but unlike Adapter, Bride pattern is more of refactoring the existing code, 
#whereas , the Adapter pattern is wrapper around existinglibrary or legacy code, that you can't alter

```
from abc import ABC , abstractmethod


#interface for the abstraction layer
class IShape(ABC):
  @abstractmethod
  def draw(self):
    pass
    


class Circle(IShape):
  
  def __init__(self,implementer):
    self.implementer = implementer
  
  def draw(self):
    
    self.implementer.draw_implemention()
    
   
class Square(IShape):
  def __init__(self,implementer):
    self.implementer = implementer
  
  def draw(self):
    self.implementer.draw_implemention()
  
#interface for implementer  

class IShapeImplementer(ABC):
  @abstractmethod
  def draw_implemention(self):
    pass
  


class CircleImplentation(IShapeImplementer):
  def draw_implemention(self):
    print("Circle is drawn...")
    
class SquareImplementation(IShapeImplementer):
  def draw_implemention(self):
    print("Square is drawn...")
     

#client  

#the Implementation is bridged to the Abstracion
circle  =Circle(CircleImplentation())
square = Square(SquareImplementation())

circle.draw()
square.draw()    


```
You can see the implemnetation is independent of the abstraction , Shape , you can add new implmenation  without adding a shape <br>
You can add new shape without adding new implementation , and make use of existing implementation and also change b/w implementation

