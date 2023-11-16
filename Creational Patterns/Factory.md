```from abc import ABC,abstractmethod


class IChair:
  @abstractmethod
  def get_dimensions():
    pass
    

class SmallChair(IChair):
  
  def __init__(self):
    self.height =120
    self.width =90
  
  def get_dimensions(self):
    return ("SmallChair", "height = ", self.height,  "width = ", self.width)
  

class MediumChair(IChair):
  
  def __init__(self):
    self.height =160
    self.width =100
  
  def get_dimensions(self):
     return ("MediumChair", "height = ", self.height,  "width = " ,self.width)
    
class BigChair(IChair):
  
  def __init__(self):
    self.height =200
    self.width =180
  
  def get_dimensions(self):
    return ("BigChair", "height = ", self.height,  "width = " ,self.width)
    

#Factory creates the object at runtime , based on the events/ condition
#factory pattern also provides the abstraction b/w where object created and is used

class Factory:
  
  
  def get__chair(self,chair):
    if chair == "small":
      return SmallChair()
    elif chair =="medium":
     
      return MediumChair()
    elif chair =="big":
      return BigChair()
    
    return None
```
#client
chair  = Factory().get__chair("medium")<br>
print(chair.get_dimensions())
  
  
    
  
