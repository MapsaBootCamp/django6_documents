# Descriptors
* when we using getter setter and deleter, if we have so many variable for initiolize we will have so many problem for fixing that Descriptors had created


+ __get__
- __set__
* __delet__
- __set_name__

"""
"""
Descriptors are for contrilling variables
they are __get__, __set__, __set_name__,  __delet__
"""
class One:

    def __set_name__(self, owner, name):
        self.name = name     
    """
    this method get class variables names for using in class One methods
    """

    def __get__(self, instance, owner):
        return instance.__dict__[self.name]
    """
The object is taken by Get and variables can be accessed from inside the object and the 
property method is also executed
    """
    def __set__(self, instance, value):
        if not isinstance(value, str):
            raise ValueError("you must enter string! ")
        instance.__dict__[self.name] = value

    """
the object is taken bt set and variables can be cheacked and set 
    """        

    def __delete__(self, instance):
        instance.__dict__[self.name] = None

class Person:
    name = One()
    car = One()

    def __init__(self, name, car):
        self.name = name
        self.car = car    
    

p = Person('amir', 'benz')
p.name = 'parsa'
p.car = 'hunda'
print(p.name)












"""