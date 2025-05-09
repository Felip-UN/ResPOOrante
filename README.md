# Reto 3 "Clases"
## Retos que lo componen
1. Create a repo with the class exercise
2. Restaurant scenario: You want to design a program to calculate the bill for a customer's order in a restaurant.
- Define a base class MenuItem: This class should have attributes like name, price, and a method to calculate the total price.
- Create subclasses for different types of menu items: Inherit from MenuItem and define properties specific to each type (e.g., Beverage, Appetizer, MainCourse).
- Define an Order class: This class should have a list of MenuItem objects and methods to add items, calculate the total bill amount, and potentially apply specific discounts based on the order composition.

Create a class diagram with all classes and their relationships. The menu should have at least 10 items. The code should follow PEP8 rules.

## 1. Ejercicio de clase
Clase de la que se tomara inforamcion
```python
import math
class Point:
  definition: str = "Entidad geometrica abstracta que representa una ubicación en un espacio."
  def __init__(self, x=0, y=0):
    self.x = x
    self.y = y
  def move(self, new_x, new_y):
    self.x = new_x
    self.y = new_y
  def reset(self):
    self.x = 0
    self.y = 0
```

Clase creada para definir la linea
```python
class Line:
  def __init__(self, punto1:"Point", punto2:"Point"):
    self.punto1 = punto1 #Punto tendra 2 atributos (x, y)
    self.punto2 = punto2
  def compute_length(self):
    calculo1=((self.punto2.x-self.punto1.x)**2 + (self.punto2.y-self.punto1.y)**2)**(1/2) # Metodo con formula
    calculo2=math.dist((self.punto1.x, self.punto1.y), (self.punto2.x, self.punto2.y)) # Metodo con math sacado de chat y verificado con w3schools
    return f"La longitud entre los puntos con mformula es: {calculo1} y con metodo de math: {calculo2}"
  def compute_slope(self):
      dx = self.punto2.x - self.punto1.x
      dy = self.punto2.y - self.punto1.y
      if dx == 0:
          return float('inf')  # Pendiente infinita (recta vertical)
      return dy / dx
  def compute_horizontal_cross(self): # Este método calcula el cruce con el eje Y (ordenada al origen, b)
    m = self.compute_slope() # Pendiente se saca de un metodo anterior
    if m == float('inf'):
            return None  # Recta vertical no cruza el eje Y
    b= self.punto1.y - m*self.punto1.x # Corte en "y" se define como b = y-m*x 
    return b
  def compute_vertical_cross(self): # Este método calcula el cruce con el eje X (cuando y = 0)
        m = self.compute_slope()
        if m == 0: # Recta horizontal no cruza el eje X
            return None
        b = self.compute_horizontal_cross() # b se saca de un metodo anterior
        return -b / m
```

Main
```python
p1 = Point(0, 2)
p2 = Point(4, 6)
linea = Line(p1, p2)
pendiente=linea.compute_slope()
corte_horizontal= linea.compute_horizontal_cross()
corte_vertical= linea.compute_vertical_cross()
```
Codigo para visualizar salidas
```python
print(linea.compute_length())
print(f"La pendiente de la linea es: {pendiente}")
print(f"La linea corta con el eje vertical en Y={corte_horizontal}")
print(f"La linea corta con el eje horizontal en X={corte_vertical}")
```

**Consola**

La longitud entre los puntos con formula es: 5.656854249492381 y con metodo de math: 5.656854249492381

La pendiente de la linea es: 1.0

La linea corta con el eje vertical en Y=2.0

La linea corta con el eje horizontal en X=-2.0
