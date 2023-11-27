
<strong>Fly</strong> in the term Flyweight means light/not heavy. 
Instead of creating thousands of objects that share common attributes, and result in a situation
where a large amount of memory or other resources are used, you can modify your classes to share
multiple instances simultaneously by using some kind of reference to the shared object instead


Objects usually have intrinsic and extrinsic data , <br>
__________________________________________________________________<br>
inorder to make use of flyweight and thus manage memory efficiently , we need to keep intrinsic data(that is data that is shared b/w the objects) while creating the flywight object<br>
based on which when the object with same , intrinsic data is needed, we can just return the object that is created before 

```
from abc import ABC , abstractmethod


class IFlyEeight:
  @abstractmethod
  def get_value(self):
    pass


class FlyWeight(IFlyEeight):
  
  def __init__(self,value):
    self.value = value
  def get_value(self):
    
    print(f"The object is {self.value}  id is {id(self)}")

#Factory is responsible for managing the creation of objects,(either gives existing object or new objects)
class FlyWeightFactory:
  
  def __init__(self):
    self.objects_dict ={}
    
  def get_objects(self,value):
    
    #suppose each object is uniquely identfied with the value attribute , 
    #then we cache the object, so that in case it is accessed again we can return the reference
    if value not in self.objects_dict:
      self.objects_dict[value] = FlyWeight(value)
    return self.objects_dict[value]

#client 

factory  = FlyWeightFactory()
#if the same objects is tried to be accessed then it return the existing object
objects_to_get =[1,2,15,13,1,200,100,13]
for val in objects_to_get:
  obj =factory.get_objects(val)
  obj.get_value()
    
    
    
