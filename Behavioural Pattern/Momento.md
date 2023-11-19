
Throughout the lifecycle of an application, an objects state may change. You might want to store a
copy of the current state in case of later retrieval. E.g., when writing a document, you may want to
auto save the current state every 10 minutes. Or you have a game, and you want to save the current
position of your player in the level, with its score and current inventory.<br>

You can use the Memento pattern for saving a copy of state and for later retrieval if necessary. 
The Memento pattern, like the Command pattern, is also commonly used for implementing UNDO/
REDO functionality within your application.<br>
The difference between the Command and the Memento patterns for UNDO/REDO, is that in the
Command pattern, you re-execute commands in the same order that changed attributes of a state,
and with the Memento, you completely replace the state by retrieving from a cache/store.

#this is object respresnting a stored state
class Momento:
  
  def __init__(self, state):
    self._state = state
  
#this is the object which changes state often and whose state is being stored by care taker
class Originator:
  
  def __init__(self):
    self._state = ""
  @property
  def state(self):
    return self._state
  @state.setter
  def state(self,state):
    self._state = state
  @property
  def momento(self):
    print("From the originator , creating a momento of the state\n")
    return Momento(self._state)
  @momento.setter
  def momento(self,momento):
    print("restoring state from the momento, to the originator\n")
    self._state = momento._state
    
    
#care taker responsible for creating the state backup and restore as required
class CareTaker:
  
  def __init__(self,originator):
    #keep info of originator whose,  state to be stored as momento, and to  be restored ,
    self.originator = originator
    #keeps momentos as backup in a list , and restored as needed
    self.momentos = []
    
  def create(self):
    print("The caretaker creates the copy of the state as momento and added to the list")
    self.momentos.append(originator.momento)
  def restore(self,ind):
    print(f"The caretaker restores the momento at { ind } to originator")
    momento = self.momentos[ind]
    self.originator.state = momento._state
  

#client


originator  = Originator()
care_taker =CareTaker(originator)
#originator may change state often 
originator.state  = "state1"
originator.state =  "state2"
#caretaker takes backup of any state 
care_taker.create()


originator.state = "state3"
originator.state = "state4"
#caretaker takes backup of another state 
care_taker.create()

print(f"Total created momentos till now =  {len(care_taker.momentos)}\n")

#care_taker restore state of originator as needed 
care_taker.restore(0)
print(f"The originator state is {originator.state}")


