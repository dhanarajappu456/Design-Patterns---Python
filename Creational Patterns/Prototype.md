
The Prototype Pattern is used when you want to create new objects by copying an existing object, known as the prototype. Instead of creating a new instance of a class using a constructor, the prototype pattern involves creating new objects by copying an existing object, known as the prototype.

This is useful to save time consuming object creation say if object is created with info from some database reads, so performing this reads, for each object would be time consuming and cost heavy 
in such scenarios , you can use this pattern where it clones the first object that read the database so that  further object can be created from this , rather than reading the database directly 

Here are some scenarios where the Prototype Pattern is commonly used:

Creating Objects with Costly Initialization:
If creating an object is an expensive operation in terms of time or resources, and you need multiple similar instances, the Prototype Pattern allows you to create new objects by copying an existing one, potentially saving on the cost of initialization.


```

from abc import ABC,abstractmethod

import copy
class Iprototype: 
  @abstractmethod
  def clone(self):
    pass
  
class MyClass(Iprototype):
  
  def __init__(self,value,arr):
    self.value = value
    self.arr = arr
  #deepcopy 
  #you can also use shallow copy if needed
  def clone(self):
    return copy.deepcopy(self)
  
  
obj1 =MyClass(19,[1,2,3])
print(f"id, object,  first element of the array = ,{id(obj1),obj1, obj1.arr[0]}")

obj2 =obj1.clone()
print(id(obj2),obj2,obj2.arr[0])

print("changing first element of array of obj2\n")
obj2.arr[0]=10
#obj1 has still 1 as the first element and obj2 has first element changed = 10
#which means deep copy has worked correctly
print(f"after change first element of array in obj1 and obj2 are ={ obj1.arr[0], obj2.arr[0 ]}") #1,10





    
