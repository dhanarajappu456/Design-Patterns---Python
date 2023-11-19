class Momento:
  
  def __init__(self, state):
    self.state = state
  
  

class Originator:
  
  def __init__(self):
    self.state = ""
  @property
  def state(self):
    return self.state
  @state.setter
  def state(self,state):
    self.state = state
  @property
  def momento(self):
    print("From the originator , creating a momento of the state")
    return Momento(self.state)
  @momento.setter
  def momento(self,momento):
    print("restoring state from the momento, to the originator")
    self.state = momento.state
    
    

class CareTaker:
  
  def __init__(self):
    self.originator = Originator()
    self.momentos = []
    
  def create(self,momento):
    print("The caretaker creates the copy of the state as momento and added to the list")
    self.momentos.append(momento)
  def restore(self,ind):
     print(f"The caretaker restores the momento at {ind } to originator ")
    momento = self.momentos[ind]
    self.originator.state = momento.state

#client
originator  = Originator()
care_taker =CareTaker()
