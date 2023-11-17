
# . 
The Facade pattern essentially is an alternative, reduced or simplified interface to a set of other
interfaces, abstractions and implementations within a system that may be full of complexity and/or
tightly coupled.

# .
It can also be considered as a higher-level interface that shields the consumer from the
unnecessary low-level complications of integrating into many subsystems



```
class SubSystemClassA:
  
  @staticmethod
  def method():
  
    print("A")
class SubSystemClassB:
 
  @staticmethod
  def method():
   
    print("B")
class SubSystemClassC:
  
  @staticmethod
  def method():
   
    print("C")
    
class Facade:
  
  #Facade class that acts as a shield tp the comples subsystems , as a common and simplified 
  #point of access to the client
  
  def method_for_a(self):
    
    SubSystemClassA.method()
    
  def method_for_b(self):
    SubSystemClassB.method()
  
  def method_for_c(self):
    SubSystemClassC.method()


#client

Facade().method_for_a()
Facade().method_for_b()
Facade().method_for_c()
    
    
    
    
