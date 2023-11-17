
# .
Use the decorator when you want to add responsibilities to objects dynamically without
affecting the inner object

# .
You want the option to later remove the decorator from an object in case you no longer need it

# .
It is an alternative method to creating multiple combinations of subclasses. I.e., Instead of
creating a subclass with all combinations of objects A, B, C in any order, and including/
excluding objects, you could create 3 objects that can decorate each other in any order you
want.


# .
A decorator supports recursive composition. E.g., halve(halve(number)

```
from abc import ABC , abstractmethod

#interface both the decorator and component implement
class IComponent(ABC):
  cost = 0 
  @abstractmethod
  def get_cost(self):
      pass

class ComponentA(IComponent):
  
  def __init__(self):
    self.cost = 10
  def get_cost(self):
    return self.cost 
    
class ComponentB (IComponent):
    
  def __init__(self):
    self.cost = 20
  def get_cost(self):
    return self.cost 




#decorator that decorates the component or another decorator that has decorated another  component 
class Decorator1(IComponent):
  
  def __init__(self,component):
    self.component = component
    self.cost = 100
  def get_cost(self):
    return self.cost   + self.component.get_cost()
      

class Decorator2(IComponent):
  def __init__(self):
    self.component = component
    self.cost = 200
  def get_cost(self):
    
    return self.cost   + self.component.get_cost()
  
#Client code

comp1 = ComponentA()
tot_cost  = Decorator1(Decorator1(comp1)).get_cost()
print(tot_cost)#prints 210


