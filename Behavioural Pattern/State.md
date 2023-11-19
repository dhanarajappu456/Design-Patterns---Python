
The State Design Pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes.<br>
The pattern involves representing the possible states of an object as separate classes and delegating the state-specific behavior to these classes. <br>
The object, referred to as the "context," has a reference to an instance of the current state class. When the state changes, the context switches its reference to a different state class, effectively changing its behavior.



```
from abc import ABC, abstractmethod 
import random

#interface for states
class IState(ABC):
  @abstractmethod
  def __str__(self):
    pass


class StateA(IState):
  
  def __str__(self):
    return "state A"
  
  
class StateB(IState):
  
  def __str__(self):
    return "state B"
    
class StateC(IState):
  
  def __str__(self):
    return "state C"

#context is the object , which might changes the state when its behaviour changes
#this pbject has reference to different state object, denoting different states
class Context:
  
  def __init__(self):
    self.handles = [StateA(),StateB(),StateC()]
  
  def request(self):
    ind  = random.randint(0,2)
    return self.handles[ind]
    
#client
context = Context()
print(context.request())
print(context.request())
print(context.request())
    
      
  
