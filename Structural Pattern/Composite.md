```
from abc import ABC, abstractmethod
#leaf and the compostite(which include many leafs and other composite as the child or component)
#leaf and compoiste are components , hence it has common interface 

class IComponent(ABC):
  
  ref_to_parent = None
  name  = None
  @abstractmethod
  def info(self):
    pass
  @abstractmethod
  def detach(self):
    pass

#leaf node 
class Leaf(IComponent):
  
  def __init__(self,name):
    self.name = name
  #prints this leaf info(id) and its parent node's (which is a composite ) id 
  def info(self):
    print(f" Leaf name : {self.name}  Leaf id :{id(self)}  Parent id :{self.ref_to_parent}")
  #detach this object from parent
  def detach(self):
    if self.ref_to_parent != None: 
      self.ref_to_parent.delete(self)
      self.ref_to_parent = None
  
#composite consist of many component as child
class Composite(IComponent):
  def __init__(self,name):
    self.name = name
    #list of all the components attached to this composite object 
    self.components =[]
  
  
  def info(self):
    print(f"Composite name : {self.name}  Composite id :{id(self)}  Parent id :{self.ref_to_parent}")
    print(f"Composite length : {len(self.components)}")
    #recursively print the components
    for component in self.components:
      component.info()
      
  #detach this object from parent
  def detach(self):
    if self.ref_to_parent != None: 
      self.ref_to_parent.delete(self)
      self.ref_to_parent = None
  #attach the passed component to this Composite object
  def attach(self,component):
    #remove the prev parent reference to which the component was attached , when reattaching to other composite
    component.detach()
    component.ref_to_parent = self
    self.components.append(component)
    
  def delete(self,component):
    self.components.remove(component)
    
  
#client
leaf1 = Leaf("leaf1")
leaf2 = Leaf("leaf2")
leaf3 = Leaf("leaf3")


composite1  = Composite("comp1")
composite2 = Composite("comp2")

#composite1 has leaf1 and leaf2 has child
composite1.attach(leaf1)
composite1.attach(leaf2)
#composite contain the whole composite1 as child
composite2.attach(composite1)

#now composite2 logs its info it childs info and their childs info and so on recursively
composite2.info()
```
To maintain the heirarchical relation , we use composite design pattern 
  

  


