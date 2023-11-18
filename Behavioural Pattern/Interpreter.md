The Interpreter pattern helps to convert information from one language into another. <br>

The language can be anything such as words in a sentence, numerical formulas or even software
code.<br>

The process is to convert the source information, into an Abstract Syntax Tree (AST) of Terminal
and Non-Terminal expressions that all implement an interpret() method.<br>

A Non-Terminal expression is a combination of other Non-Terminal and/or Terminal expressions.
Terminal means terminated, i.e., there is no further processing involved.<br>

An AST root starts with a Non-Terminal expression and then resolves down each branch until all
expressions terminate.<br>

An example expression is A + B .<br>

The A and B are Terminal expressions and the + is Non-Terminal because it depends on the
two other Terminal expressions

```
from abc import ABC , abstractmethod
#common intreface for the terminal and non terminal expression
class IExpression:
  @abstractmethod
  def evaluate(self):
    pass

#terminal expression
class Number(IExpression):
  def __init__(self,value):
   
    self.value = int(value)
  def evaluate(self):
    return self.value
  def __repr__(self):
    #repr always expect to return , string format
    return str(self.value)

#non terminal expression 
class Add(IExpression):
  def __init__(self,left,right):
    self.left =left
    self.right = right
  def evaluate(self):
    ans  =self.left.evaluate()  + self.right.evaluate()
    return ans
    
  def __repr__(self):
    return f"({self.left} Add {self.right})"

#non terminal expression     
class Sub(IExpression):
  
  def __init__(self,left,right):
    self.left =left
    self.right = right
  def evaluate(self):
    
    ans  =self.left.evaluate()  - self.right.evaluate()
   
    return ans
  def __repr__(self):
    return f"({self.left} Sub {self.right})"
    
#client
#expression to be interpreted
expression = "10 + 3 + 9 - 1 - 3 + 4"

#converting to token for connstructing abstract expression 
tokens = expression.split(" ")
AST =[]
AST.append(Add(    Number(tokens[0]) ,Number(tokens[2])   )   )
AST.append(Add(    AST[0] ,Number(tokens[4])   )   )
AST.append(Sub(    AST[1] ,Number(tokens[6])   )   )
AST.append(Sub(    AST[2] ,Number(tokens[8])   )   )
AST.append(Add(    AST[3] ,Number(tokens[10])   )   )

#the top/ root level abstract expression is at the end of the list , which 
#we evaluate

#calls evaluate recursively
print(AST[-1].evaluate())
#prints the expresion recursively
#calls the repr recursively
print(AST[-1])
    
