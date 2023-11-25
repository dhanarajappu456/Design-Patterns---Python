from abc import ABC, abstractmethod 


## 1)Without adapater - client had to check for the type of instance , to call the appropriate 
#method, since method signature or interface of the object is different 

```


class IA(ABC):
  @abstractmethod
  def method_a(self):
    pass
  
class A(IA):
  
  def method_a(self):
    print(f"method a is called...")
    


class IB(ABC):
  @abstractmethod
  def method_b(self):
    pass

class B(IB):
  
  def method_b(self):
    print(f"method b is called...")
#client  


objects  =[A(), B()]

for obj  in objects:
  
  if isinstance(obj,A):
    obj.method_a()
  if isinstance(obj,B):
    obj.method_b()
    
# Output:

# method a is called...
# method b is called...
```


# ----------------------------------------------------------------------------------------------------------------------------------------------------
## 2)With adapter  - the method of object b is made to adapt to the method signature of A, so that client can call just method_a on any object



```

class IA(ABC):
  @abstractmethod
  def method_a(self):
    pass
  
class A(IA):
  
  def method_a(self):
    print(f"method a is called...")
    


class IB(ABC):
  @abstractmethod
  def method_b(self):
    pass

class B(IB):
  
  def method_b(self):
    print(f"method b is called...")
#Making existing interface/implementation(B- called as adpatee) to adapt to the requirement of client(that is client know #only A types and its methods)     
class ClassBAdapter(IA):
  def method_a(self):
    #calling the method of B object inside the adapter, so that clinet can call this method still 
    #with signatutre of A, since adapter is implementing interface A
    obj  = B()
    obj.method_b()
#client  


objects  =[A(), ClassBAdapter()]

for obj  in objects:
  obj.method_a()
  
# Output:

# method a is called...
# method b is called...
  
 
