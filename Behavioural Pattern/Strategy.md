

The Strategy Pattern is similar to the State Pattern, except that the client passes in the algorithm
that the context should run and the execution of the algorithm does not affect the state of the context.<br>

The algorithm should be contained within a class that implements the particular strategies interface.<br>

An application that sorts data is a good example of where you can incorporate the Strategy pattern.
There are many methods of sorting a set of data. E.g., Quicksort, Mergesort, Introsort, Heapsort,


```
from abc import ABC, abstractmethod 
#useful when client choose type of algorithm- represented by a Strategy
# eg: say the client choose a type of sorting algo (like quick, merge etc...) 
# , then excute algo represented by a strategy 

#interface for strategies
class IStrategy(ABC):
  @abstractmethod
  def strategy_method(self):
    pass


class StrategyA(IStrategy):
  
  def strategy_method(self):
    print ("Strategy A executed...")
  
  
class StrategyB(IStrategy):
  
  def strategy_method(self):
   print ("Strategy B executed...")
    
class StrategyC(IStrategy):
  
  def strategy_method(self):
   print ("Strategy C executed...")

#context encapsulate or receive the strategy to execute
class Context:

  def execute(self,strategy):
    strategy().strategy_method()
    
#client
context = Context()
context.execute(StrategyA)
context.execute(StrategyB)
context.execute(StrategyC)

    
      
  
