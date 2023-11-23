# used in ATM  for getting correct denominations , where each denomination handled by each successor class in the chain 
# used in vendin machine
# used in logger where each successor handle a type of log message like error, debug etc...

# .
In this pattern, an object is passed to a Successor, and depending on some kind of logic, will or
won't be passed onto another successor and processed. There can be any number of different
successors and successors can be re-processed recursively.
# . 
This process of passing objects through multiple successors is called a chain.
# .
The object that is passed between each successor does not know about which successor will
handle it. It is an independent object that may or may not be processed by a particular successor
before being passed onto the next

```
from abc import ABC , abstractmethod
import random

#inteface for all the successors
class IHandler:
  @abstractmethod
  def handle(self):
    pass



class Successor1(IHandler):
  def handle(self,payload):
    
    payload +=1 
    #the next successor is usually determined at dynamically
    test= random.randint(1,3)
    print(f"Successor1 payload {payload}")
    if test ==1:
      
      Successor1().handle(payload)
    if test ==2:
     
      Successor2().handle(payload)
    return payload
    
    
    
class Successor2(IHandler):
  def handle(self,payload):
    
    payload -=1
    #the next successor is usually determined at dynamically
    test= random.randint(1,3)
    print(f"Successor2 payload {payload}")
    if test ==1:
      
      Successor2().handle(payload)
    if test ==2:
     
      Successor1().handle(payload)
    return payload
    
class Chain:
  @staticmethod
  def handle(payload):
    Successor1().handle(payload)

#client
Chain.handle(10)
    
    
    
