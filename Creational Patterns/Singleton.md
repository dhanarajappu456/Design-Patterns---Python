```
class Singleton:
    # private var
    _instance = None
    
    def  __new__(cls):
        #creates the object for the first time 
        if cls._instance ==None:
          cls._instance = super().__new__(cls)
        return cls._instance
    
    def __init__(self):
      
      if not hasattr(self,"initialised"):
        #this gets printed, only very first time
        print("initialised")
        self.initialised = True
```
# Example usage:
a = Singleton()  # This initializes the singleton <br\>
b = Singleton()  # This returns the existing instance, doesn't reinitialize
