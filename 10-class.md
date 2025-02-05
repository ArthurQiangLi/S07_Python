# Using 'Class' in python

## Quick example

```py
car.py

class Car(): ##[1]
    def __init__(self, make, model, year):
        self.make=make
        self.model=model
        self.year=year
        self.odo=0 ##[4]

    def read_odo(self):
        return self.odo
    def set_odo(self, val):
        self.odo = val
    def fill_gas(self):
        ...

class Battery():
    def __init__(self, battery_size=70):
        self.battery_size=battery_size

class ElectricCar(Car): ##[5]
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        self.battery = Battery() ##[7] instance a class inside a class

    def charge(self, amount):
        self.battery += amount
    def fill_gas(self): ##[6]
        print('there is no gas tank in a ev.')

```

```py
my_car.py

from car imort Car, ElectricCar
my_new_car = Car('audi', 'a4', 2016)  ##[2] the __init__() is called when instancing a class.
my_old_car = Car('bmw', '325', 2001)

my_new_car.odo = 10 ##[3]
my_new_car.set_odo(11)

bob_ev = ElectricCar('tesla', 'model S', 2015)
```

Code explained here refering to each `##[N]` in the code above:

1. Define a class
2. Create a class instance
3. Using the class instance, with '.'
4. Set default value for variables in a class
5. **Inherit** from a father class
6. Ignore the father class same-name method.
7. Use a class in a class

## What are the notes for using classes?

### 1. 'AaaaBbbb' naming convention

use Camel style as `class Dog():` and `class ElectricCar():`

### 2. when importing whole module

you add `car.` explicitly, this can effectively avoid naming conflict. my_car.py :

```py
import car
my_new_car = car.Car('audi', 'a4', 2016)
bob_ev = car.ElectricCar('tesla', 'model S', 2015)
```

### 3. when inheriting a class

The **son class** automatically gets AL the variables and methods from the **father class**.
