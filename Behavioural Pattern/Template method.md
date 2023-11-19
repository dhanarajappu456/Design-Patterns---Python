
The Template Method Pattern is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. 
It is used to create a method that provides the outline of an algorithm and allows the steps of the algorithm to be implemented by concrete subclasses.<br><br>

The key idea behind the Template Method Pattern is to define the structure of an algorithm in a method but leave some steps of the algorithm to be implemented by subclasses.
This pattern promotes code reuse and allows for variations in the implementation of certain steps without changing the overall algorithm.

<br><br>

Consist of Abstract Class which has :<br>
1)Template method  defining the order or general outline of algo <br>
2)Hooks - These are methods with default implementation or empty implementation <br>
the sublass/concrete class can implement them leave unimplemented (and use default implemenation)<br>
3) Abstract methods - they are abstract methods - that subclass has to implement <br>


```
from abc import ABC, abstractmethod

class HotBevPrearatorTemplate(ABC):
  #template method
  def prepare_beverage(self):
    
    
    self.boil_water()
    self.brew()
    self.pour_to_cup()
    self.add_condiments()
  
  #hooks(default implementation)
  def boil_water(self):
    
    print("Boiling water...")
  #hooks(empty)
  def pour_to_cup(self):
    pass
  
  
  @abstractmethod    
  def brew(self):
    pass
  @abstractmethod
  def add_condiments(self):
    pass
  
class Tea(HotBevPrearatorTemplate):
  def pour_to_cup(self):
    print("pour to the cup in swirl")
  def brew(self):
    print("brew with tea powder...")
  def add_condiments(self):
    print("adding lemon...")
  
class Coffee(HotBevPrearatorTemplate):
  def pour_to_cup(self):
    print("pour to the cup in gently")
  def brew(self):
    print("brew with coffee powder...")
  def add_condiments(self):
    print("adding cardamom...")
    
#client
Tea().prepare_beverage()
Coffee().prepare_beverage()
    
