
Objects communicate through the Mediator rather than directly with each other.
As a system evolves and becomes larger and supports more complex functionality and business
rules, the problem of communicating between these components becomes more complicated to
understand and manage. It may be beneficial to refactor your system to centralize some or all of its
functionality via some kind of mediation process<b>

The mediator pattern is similar to creating a Facade pattern between your classes and processes.
Except the Mediator is expected to transact data both ways between two or more other classes or
processes that would normally interact directly with each other

```

'''
this is is similar to facade, where a central  point of truth is responsible for managing other objects
but unlike facade, where a client request subsystem methods(which is one way)

the mediator is a broad 2 way of communication b/w the objects (collegues ) not directly, but via mediator
'''

from abc import ABC, abstractmethod 

#interface for both mediator and colleagues, 
#the colleagues can only method releveant to it  and  leave the other methods un implemented

class IMediator:
  @abstractmethod
  def method_a(self):
    pass
  def method_b(self):
    pass
  

#colleague implement methods of it
class ColleagueA(IMediator):
  def method_a(self):
    print("Colleague A method")
  
  def method_b(self):
    pass


#colleague implement method releveant to it  
class ColleagueB(IMediator):
  def method_a(self):
    pass
  def method_b(self):
    print("Colleague B method")
    
    
#mediator act
class Mediator(IMediator):
  
  def __init__(self,colleague_a,colleague_b):
    self.colleague_a = colleague_a
    self.colleague_b  = colleague_b
  
  def method_a(self):
    self.colleague_a.method_a()
  
  def method_b(self):
    self.colleague_b.method_b()
    

coll_a  = ColleagueA()
coll_b  = ColleagueB()


med =Mediator(coll_a, coll_b)

#ColleagueB may want to communicate or request ColleagueA info
med.method_a()
#ColleagueA may want to communicate or request ColleagueB info
med.method_b()
    
