
# .
Proxy forwards requests onto the Real Subject when applicable, depending on the kind of
proxy.

# .
virtual proxy can cache elements of a real subject before loading the full object into memory.

# .
Protection proxy can provide an authentication layer. For example, an NGINX proxy can add
Basic Authentication restriction to a HTTP request.
# .
It is also very similar to the Facade, except you can add extra responsibilities, just like the 
Decorator. The Decorator however can be used recursivel
# .
The intent of the Proxy is to provide a stand in for when it is inconvenient to access a real
subject directly
# . 
The Proxy design pattern may also be called the Surrogate design pattern

# proxy design used in providing caching, access restriction , preprocessing before a request and post processing the request

```

#eg of caching proxy -which cache request here
from abc import ABC, abstractmethod 

#interface of both proxy and real subject , as both need to perform same tasks (here respond to request with 
#result)
class ISubject:
  def request(self): 
    pass
  
#the real subject
class Subject(ISubject):
  def request(self):
    #this is enoromous data
    return [1,3,5,6]
    
#proxy to real subject
class Proxy(ISubject):
  def __init__(self):
    self.real_subject = Subject()
    self.enoromous_data =None
  def request(self):
    if self.enoromous_data == None:
      print("Pulling the data from Real Subject")
      self.enoromous_data = self.real_subject.request()
    else:
      print("Pulling cached data from the proxy")
    return self.enoromous_data
    
#client
proxy = Proxy()
#proxy pulls data from the real subject and cached by proxy 
res= proxy.request()
print(res)
#proxy returns the cached data 
proxy.request()
print(res)
    
  
