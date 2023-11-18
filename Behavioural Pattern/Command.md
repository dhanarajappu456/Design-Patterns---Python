
The Command pattern is a behavioral design pattern, in which an abstraction exists between an
object that invokes a command, and the object that performs it.
<br>
E.g., a button will call the Invoker, that will call a pre-registered Command, that the Receiver will
perform.
<br>
A Concrete Class will delegate a request to a command object, instead of implementing the request
directly.
<br>
Using a command design pattern allows you to separate concerns and to solve problems of the
concerns independently of each other.
<br>
E.g., logging the execution of a command and its outcome
<br>
The command pattern is a good solution for implementing UNDO/REDO functionality into your
application.

<br>
#There are:

a)Invoker - like switch that trigger command <br>
b)Command object <br>
c)Receiver - on which the command is executed <br>


```
from abc import ABC , abstractmethod


#inteface for all the commands
class Icommand:

  @abstractmethod
  def execute(self):
    pass

#commnad object which is created with the asscoiated receiver 
#it should notify with the appropriate command 
class Command1(Icommand):
  
  def __init__(self,receiver):
    self.receiver  = receiver
  def execute(self):
    self.receiver.execute_1()
    

class Command2(Icommand):
  
  def __init__(self,receiver):
    self.receiver  = receiver
  def execute(self):
    self.receiver.execute_2()
    
    
#reciver receives the command and execute it
class Receiver:
  
  def execute_1(self):
    print("Executing command 1")
    
  def execute_2(self):
    print("Executing command 2")
    
#invoker execute/ trigger the command
class Invoker:
  
  def __init__(self):
    
    self.commands ={}
  def register(self,command_name, command):
    
    self.commands[command_name] = command
  
  def execute(self,command_name):
    if command_name not in self.commands:
      print("No such commands")
      return 
    self.commands[command_name].execute()
    
    
    
#client
receiver = Receiver()

#Create commands with the receiver associated with it, here just one receiver
command1 = Command1(receiver)
command2 = Command2(receiver)

#invoker need to have info on the available commands- which is stored in a lookup and executed on demand
invoker = Invoker()
invoker.register("command1",command1)
invoker.register("command2", command2)

#executing the commmands
invoker.execute("command1") # prints Executing command 1
invoker.execute("command2") # prints Executing command 2
invoker.execute("command3") # prints no such command 
    
    
