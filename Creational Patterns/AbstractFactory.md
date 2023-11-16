```from abc import ABC,abstractmethod

#interface for all type of tables
class ITable:
  @abstractmethod
  def get_dimensions():
    pass
    

class SmallTable(ITable):
  
  def __init__(self):
    self.height =120
    self.width =90
  
  def get_dimensions(self):
    return ("SmallTable", "height = ", self.height,  "width = ", self.width)
  

class MediumTable(ITable):
  
  def __init__(self):
    self.height =160
    self.width =100
  
  def get_dimensions(self):
     return ("MediumTable", "height = ", self.height,  "width = " ,self.width)
    
class BigTable(ITable):
  
  def __init__(self):
    self.height =200
    self.width =180
  
  def get_dimensions(self):
    return ("BigTable", "height = ", self.height,  "width = " ,self.width)
    


#interface for all type of chairs
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
    


class ChairFactory:
  
  def get_chair(self,chair):
    
    if chair == "SmallChair":
      return SmallChair()
    elif chair =="MediumChair":
     
      return MediumChair()
    elif chair =="BigChair":
      return BigChair()
    
    return None
      
      
class TableFactory:
  
  def get_table(self,table):
    
    if table == "SmallTable":
      return SmallTable()
    elif table =="MediumTable":
     
      return MediumTable()
    elif table =="BigTable":
      return BigTable()
    
    return None  
  

class  IFurnitureFactory:
  @abstractmethod
  def get_furniture(self):
    pass 
  
  
class FurnitureFactory(IFurnitureFactory):
  #abstract factory with multiple factories
  
  
  def get_furniture(self,furniture):
    
    if furniture in ["SmallChair","MediumChair","BigChair"]:
      return ChairFactory().get_chair(furniture)
      
    elif furniture in ["SmallTable","MediumTable","BigTable"]:
      return TableFactory().get_table(furniture)
    return None



    

#client
chair  = FurnitureFactory().get_furniture("loio")
if chair ==None:
  print("Oops no such furniture...")
else:
  print(chair.get_dimensions())
```

Factory of factories , where each factory produces product of a kind
  
  
    
  
