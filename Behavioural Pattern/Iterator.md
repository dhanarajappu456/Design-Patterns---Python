
The Iterator will commonly contain two methods that perform the following concepts.<br>
        next: returns the next object in the aggregate (collection, object).
       has_next: returns a Boolean indicating if the Iterable is at the end of the iteration or not.<br>
The benefits of using the Iterator pattern are that the client can traverse a collection of
aggregates(objects) without needing to understand their internal representations and/or data
structures
```
from abc import ABC , abstractmethod

#interface for aggregates on which Iterator iterates
class IAggregate(ABC):
  @abstractmethod
  def method(self):
    pass

#Aggregate on which iterator iterates
class Aggregate(IAggregate):
  def method(self):
    print("method invoked")
    
    
#interface for the Iterator
class Iiterable(ABC):
  @abstractmethod
  def has_next(self):
    pass
  def next_(self):
   pass

#iterator
class Iterator(Iiterable):
  def __init__(self,aggregates):
    self.aggregates=aggregates
    self.ind  = 0
  def has_next(self):
    return self.ind<len(self.aggregates)
      
    
  def next_(self):
    if self.has_next():
     aggr  = self.aggregates[self.ind]
     self.ind+=1
     return aggr
    raise Exception("AtEndOfIteratorException" ,"End of Iteration")
   
     

aggregates = [Aggregate(),Aggregate(),Aggregate(),Aggregate()]
#creating Iterator for the aggregates
itr = Iterator(aggregates)

#iterating on the aggregates
while(itr.has_next()):
  itr.next_().method()
  
