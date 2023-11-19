1. Pull-Based Observer:
___________________________
In the pull-based Observer pattern, observers explicitly request the information they need from the subject when they are notified of a change.
The subject typically provides a method that observers can call to retrieve the updated information.

here the observer and subject is more coupled, since observer need to know methods of subject it can call, so changes in subject affect the observer

When to Use Push-Based Observer:

-------------------------------
Observers Need Different Information:
If different observers are interested in different aspects of the subject's state, a pull-based approach allows each observer to request the specific information it requires.<br><br>


2. Push-Based Observer:
___________________________
In the push-based Observer pattern, the subject sends the observers detailed information about the change without waiting for them to request it.
  
 The subject typically provides a method that allows observers to be directly notified of the change.

When to Use Push-Based Observer:

---------------------------------
Observers Need the Same Information:
If all observers are interested in the same information, a push-based approach can simplify the code, as observers don't need to explicitly request the information.

it is fast- realtime- as soon as there is an update in subject, it notifies the observers and more decoupled

```
from abc import ABC, abstractmethod



#subject/publisher interface
class ISubject(ABC):
  
  @abstractmethod
  def notify (self):
    pass
  
#subject/publisher 
class Subject(ISubject):
  
  def __init__(self,name):
    self.name = name
    self.observers  =set()
  def notify(self,msg):
    for observer in self.observers:
      observer.notify(self,msg)
  
  def subscribe(self,observer):
    self.observers.add(observer)
    
  def unsubscribe(self):
    self.observers.remove(observer)

#interface for observer
class IObserver(ABC):
  @abstractmethod
  def notify(self,subject,msg):
    pass
#observer
class Observer(IObserver):
  def __init__(self,name):
    self.name =name
    
  def notify(self, subject,msg):
    
    print(f"observer {self.name} is notified by {subject.name} with msg \'{msg}\' ")
  
#client

subject = Subject("Subject1")

observer1 = Observer("observer1")
observer2 = Observer("observer2") 
observer3 = Observer("observer3")

#observers subsribing to the subject
subject.subscribe(observer1)
subject.subscribe(observer2)
subject.subscribe(observer3)
#subject notifying the subsribed observers
subject.notify("New video uploaded")
    
    
