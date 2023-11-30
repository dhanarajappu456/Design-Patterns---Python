
builder pattern used to create complex objects at runtime, 
it is useful when u need to include only some component(attributes) in creating the final product 


# builder pattern solves the telescopic problem , where u need to have multiple and huge number of constructor for a product to be overloaded based on the attribute that you would need to use to create the product


# it is also useful when you need to invoke mtehods  on object in a particular order than return the object 

for example conside house object, the house object is completeed when 
we  call
a)make_plot 
b)make_wall
c)put_window, 
d)put_door
e)make_ceiling 

and so on.. 
finally house is returned

```
from abc import ABC,abstractmethod

#house is the product that is built
class House:
  
  def __init__(self):
    self.walls = 0
    self.doors = 0
    self.house_type = None
    
  def specification(self):
    print(f"{self.house_type} with spec : walls ={self.walls}, doors ={self.doors}")



#Interface for the builder
class IHosueBuilder:
  @abstractmethod
  def set_type(self):
    pass
  def set_walls(self):
    pass
  def set_doors(self):
    pass
    


#Builder has the product(house) object , which it builds
class HosueBuilder(IHosueBuilder):
  
  def __init__(self):
    self.house = House()
    
  def set_type(self,house_type):
    self.house.house_type = house_type
    return self
    
  def set_walls(self,walls):
    self.house.walls = walls
    return self
    
  def set_doors(self,doors):
    self.house.doors = doors
    return self
  def build(self):
    return self.house 
    



#director has builder object , based on different director , the same builder class is instantiated differntly, 
#which in turn create the product differntly
class IglooDirector:
  @staticmethod
  def construct():
    return HosueBuilder().set_type("Igloo").set_doors(1).set_walls(0).build()

class CastleDirector:
  @staticmethod
  def construct():
    return HosueBuilder().set_type("Castle").set_doors(10).set_walls(10).build()
    
class MansionDirector:
  @staticmethod
  def construct():
    return HosueBuilder().set_type("Mansion").set_doors(20).set_walls(20).build()



#client
igloo = IglooDirector.construct()
igloo.specification()

castle  = CastleDirector.construct()
castle.specification()

mansion = MansionDirector.construct()
mansion.specification()
```
