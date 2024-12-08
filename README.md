# xd
```
from math import atan,degrees
import os 

def limpiar_pantalla():
    """Limpia la consola."""
    os.system("cls" if os.name == "nt" else "clear")

def continuar():
        """Pausa la ejecución hasta que el usuario presione Enter."""
        input("\nPresiona Enter para continuar...")
        Calculadora.limpiar_pantalla()


class Point:
    def __init__(self, x: float=0, y: float=0):
        self.x = x
        self.y = y
    def move(self, new_x: float, new_y: float):
        self.x = new_x
        self.y = new_y
    def reset(self):
        self.x = 0
        self.y = 0
    def compute_distance(self, point)-> float:
        distance = ((self.x - point.x)**2+(self.y - point.y)**2)**(0.5)
        return distance

class Line:
    def __init__(self, start: Point, end: Point):
        self.start = start
        self.end = end
    
    def compute_length(self):
        return self.start.compute_distance(self.end)

    def compute_slope(self):
        x_displacement = self.end.x - self.start.x
        y_displacement = self.end.y - self.start.y
        if x_displacement == 0:
            return "Pendiente Indefinida"  # Pendiente indefinida en caso de ser una línea vertical
        else:
            return degrees(atan(y_displacement / x_displacement))

    def compute_horizontal_cross(self):
        if self.start.y > 0 and self.end.y > 0:
            return False
        if self.start.y < 0 and self.end.y < 0:
            return False
        else: return True

    def compute_vertical_cross(self):
        if self.start.x > 0 and self.end.x > 0:
            return False
        if self.start.x < 0 and self.end.x < 0:
            return False
        else: return True

class Rectangle:
    def __init__(self, width:float, height:float, center_point:float):
        self.width = width
        self.height = height
        self.center_point = center_point
    
    def compute_area(self):
        area = (self.width * self.height)
        return area
    
    def compute_perimeter(self):
        perimeter = (2*self.width + 2*self.height)
        return perimeter
    
    def compute_interference_point(self, Point):
        if Point.x < self.width and Point.y < self.height:
            return True
        else:
            return False


class Square(Rectangle):
    def __init__(self, edge, center_point):
        super().__init__(width = edge, height = edge, center_point = center_point)


while True:
    limpiar_pantalla()
    consulta = int(input("""
   
1. Usando Vertice inferior izquierdo(Point), ancho y altura
2. Usando Center(Point), ancho y altura
3. Usando dos vertices opuestos (Points)
4. Usando 4 lineas (Lines)
                         
Ingrese el número del método deseado: """))
    
    if consulta == 1:
        width = float(input("\nIngrese el ancho: "))
        height = float(input("\nIngrese la altura: "))

        bottom_left_corner_x = float(input("\nIngrese componente x del vertice inferior izquierdo: "))
        bottom_left_corner_y = float(input("\nIngrese componente y del vertice inferior izquierdo: "))
        bottom_left_corner_point = Point(bottom_left_corner_x , bottom_left_corner_y)
        
        center_point= Point(bottom_left_corner_x+(width/2),bottom_left_corner_y+(height/2))


    elif consulta == 2:
        width = float(input("Ingrese el ancho: "))
        height = float(input("Ingrese la altura: "))

        center_point_x = float(input("\nIngrese componente x del punto central: "))
        center_point_y = float(input("\nIngrese componente y del punto central: "))
        center_point = Point(center_point_x,center_point_y)
      

    elif consulta == 3:

        corner1_x = float(input("\nIngrese componente x del vertice de la izquierda: "))
        corner1_y = float(input("\nIngrese componente y del mismo vertice: "))

        opposite_corner_x = float(input("\nIngrese componente x del vertice opuesto: "))
        opposite_corner_y = float(input("\nIngrese componente y del vertice opuesto: "))

        width = abs(corner1_x-opposite_corner_x)
        height = abs(opposite_corner_y-corner1_y)

        center_point_x = height - (width/2)
        center_point_y = width - (height/2)
        center_point = Point(corner1_x+(width/2),corner1_y+(height/2))
    


    elif consulta == 4:
        start_x_width = float(input("Ingrese la coordenada x inicial del ancho: "))
        end_x_width = float(input("Ingrese la coordenada x final del ancho: "))
        start_y_width = float(input("Ingrese la coordenada y de inicio para el ancho: "))
        end_y_width = float(input("Ingrese la coordenada y de final para el ancho: "))

        start_x_height = float(input("Ingrese la coordenada x de inicio para el largo: "))
        end_x_height = float(input("Ingrese la coordenada x de final para el largo: "))
        start_y_height = float(input("Ingrese la coordenada y de inicio para el largo: "))
        end_y_height = float(input("Ingrese la coordenada y de final para el largo: "))

        horizontal_line = Line((Point(start_x_width, start_y_width)),(Point(end_x_width, end_y_width)))
        vertical_line = Line((Point(start_x_height, start_y_height)),(Point(end_x_height, end_y_height)))

       
        width = horizontal_line.compute_length()
        height = vertical_line.compute_length()

        center_point_x = (start_x_width + end_x_width) / 2
        center_point_y = (start_y_width + end_y_width) / 2
        
        center_point = Point(center_point_x,center_point_y)


    else:
        print("Error, intente de nuevo")
        continuar()
        continue
    break

Rctngl = Rectangle(width, height, center_point)
print("El área del rectángulo es ", Rctngl.compute_area(), "y el perímetro del rectángulo es", Rctngl.compute_perimeter())

Sqr = Square(edge = width or height, center_point = Point(center_point_x, center_point_y))
print("El área del cuadrado es ", Sqr.compute_area(), "y el perímetro es", Sqr.compute_perimeter())

horizontal_coord = int(input("Ingrese coordenada x de un punto: "))
vertical_coord = int(input("Ingrese coordenada y: "))
point = Point(horizontal_coord, vertical_coord)
contenencia = Rectangle.compute_interference_point(point)

if contenencia:
    print(f"El punto de coordenadas {horizontal_coord},{vertical_coord} está dentro del rectángulo")
else:
    print(f"El punto de coordenadas {horizontal_coord},{vertical_coord} NO está dentro del rectángulo")
```

```python
from math import sqrt, acos, degrees

class Point:
    """Clase que representa un punto en un plano bidimensional."""
    def __init__(self, x: float = 0, y: float = 0):
        self._x = x
        self._y = y

    def get_x(self):
        return self._x

    def set_x(self, value):
        self._x = value

    def get_y(self):
        return self._y

    def set_y(self, value):
        self._y = value

    def compute_distance(self, other_point):
        return sqrt((self.get_x() - other_point.get_x())**2 + (self.get_y() - other_point.get_y())**2)


class Line:
    """Clase que representa una línea en un plano bidimensional."""
    def __init__(self, start_point: Point, end_point: Point):
        self._start_point = start_point
        self._end_point = end_point
        self._length = self.compute_length()

    def get_start_point(self):
        return self._start_point

    def set_start_point(self, value):
        self._start_point = value
        self._length = self.compute_length()

    def get_end_point(self):
        return self._end_point

    def set_end_point(self, value):
        self._end_point = value
        self._length = self.compute_length()

    def get_length(self):
        return self._length

    def compute_length(self):
        return self.get_start_point().compute_distance(self.get_end_point())


class Shape:
    """Superclase que representa una figura geométrica."""
    def __init__(self, vertices: list[Point], edges: list[Line]):
        self.vertices = vertices
        self.edges = edges
        self.inner_angles = self.compute_inner_angles()
        self.is_regular = self.check_regular()

    def compute_area(self):
        raise NotImplementedError("Este método debe ser implementado por las subclases.")

    def compute_perimeter(self):
        return sum(edge.get_length() for edge in self.edges)

    def compute_inner_angles(self):
        """Calcula los ángulos internos (solo para polígonos convexos)."""
        angles = []
        for i in range(len(self.vertices)):
            p1 = self.vertices[i - 1]
            p2 = self.vertices[i]
            p3 = self.vertices[(i + 1) % len(self.vertices)]

            a = p1.compute_distance(p2)
            b = p2.compute_distance(p3)
            c = p1.compute_distance(p3)

            angle = acos((a**2 + b**2 - c**2) / (2 * a * b))
            angles.append(degrees(angle))
        return angles

    def check_regular(self):
        """Verifica si la figura es regular."""
        if len(self.edges) < 3:
            return False

        first_length = self.edges[0].get_length()
        first_angle = self.inner_angles[0]

        return all(edge.get_length() == first_length for edge in self.edges) and \
               all(angle == first_angle for angle in self.inner_angles)


class Rectangle(Shape):
    """Clase que representa un rectángulo."""
    def __init__(self, bottom_left: Point, top_right: Point):
        width = top_right.get_x() - bottom_left.get_x()
        height = top_right.get_y() - bottom_left.get_y()

        vertices = [
            bottom_left,
            Point(top_right.get_x(), bottom_left.get_y()),
            top_right,
            Point(bottom_left.get_x(), top_right.get_y())
        ]

        edges = [
            Line(vertices[0], vertices[1]),
            Line(vertices[1], vertices[2]),
            Line(vertices[2], vertices[3]),
            Line(vertices[3], vertices[0])
        ]

        super().__init__(vertices, edges)
        self.width = width
        self.height = height

    def compute_area(self):
        return self.width * self.height


class Square(Rectangle):
    """Clase que representa un cuadrado (subclase de Rectángulo)."""
    def __init__(self, bottom_left: Point, side_length: float):
        top_right = Point(bottom_left.get_x() + side_length, bottom_left.get_y() + side_length)
        super().__init__(bottom_left, top_right)

    def compute_area(self):
        return self.width**2

---

# Ejemplo de uso
if __name__ == "__main__":
    # Crear puntos
    p1 = Point(0, 0)
    p2 = Point(4, 4)

    # Crear un rectángulo
    rect = Rectangle(p1, p2)
    print(f"Área del rectángulo: {rect.compute_area()}")
    print(f"Perímetro del rectángulo: {rect.compute_perimeter()}")

    # Crear un cuadrado
    square = Square(p1, 4)
    print(f"Área del cuadrado: {square.compute_area()}")
    print(f"Perímetro del cuadrado: {square.compute_perimeter()}")
```
```
class MenuItem:
    """Clase base para elementos del menú."""
    def __init__(self, name: str, price: float):
        self._name = name
        self._price = price

    def get_name(self):
        return self._name

    def set_name(self, value):
        self._name = value

    def get_price(self):
        return self._price

    def set_price(self, value):
        self._price = value

    def calculate_total_price(self):
        return self._price


class Beverage(MenuItem):
    def __init__(self, name: str, price: float, is_alcoholic: bool):
        super().__init__(name, price)
        self._is_alcoholic = is_alcoholic

    def get_is_alcoholic(self):
        return self._is_alcoholic

    def set_is_alcoholic(self, value):
        self._is_alcoholic = value


class Appetizer(MenuItem):
    pass


class MainCourse(MenuItem):
    pass


class Order:
    """Clase que representa un pedido de un cliente."""
    def __init__(self):
        self.items = []

    def add_item(self, item: MenuItem):
        self.items.append(item)

    def calculate_total(self):
        total = sum(item.calculate_total_price() for item in self.items)

        # Aplicar descuento si el pedido incluye un plato principal
        if any(isinstance(item, MainCourse) for item in self.items):
            beverage_discount = 0.1  # 10% de descuento en bebidas
            for item in self.items:
                if isinstance(item, Beverage):
                    total -= item.get_price() * beverage_discount

        return total

    def show_order_summary(self):
        print("Resumen del pedido:")
        for item in self.items:
            print(f"{item.get_name()} - ${item.get_price():.2f}")
        print(f"Total: ${self.calculate_total():.2f}")


class Payment:
    """Clase para manejar los pagos."""
    def __init__(self, order: Order):
        self.order = order
        self.amount_paid = 0.0

    def make_payment(self, amount: float):
        self.amount_paid += amount

    def is_payment_complete(self):
        return self.amount_paid >= self.order.calculate_total()

    def show_payment_status(self):
        total = self.order.calculate_total()
        print(f"Total a pagar: ${total:.2f}")
        print(f"Monto pagado: ${self.amount_paid:.2f}")
        if self.is_payment_complete():
            print("El pago está completo. Gracias por su compra.")
        else:
            print(f"Falta por pagar: ${total - self.amount_paid:.2f}")


# Ejemplo de uso
if __name__ == "__main__":
    # Crear elementos del menú
    beverage1 = Beverage("Cerveza", 5.0, True)
    beverage2 = Beverage("Refresco", 2.0, False)
    appetizer = Appetizer("Nachos", 6.0)
    main_course = MainCourse("Hamburguesa", 10.0)

    # Crear un pedido
    order = Order()
    order.add_item(beverage1)
    order.add_item(beverage2)
    order.add_item(appetizer)
    order.add_item(main_course)

    # Mostrar el resumen del pedido
    order.show_order_summary()

    # Realizar el pago
    payment = Payment(order)
    payment.show_payment_status()
    payment.make_payment(15.0)
    payment.show_payment_status()
    payment.make_payment(10.0)
    payment.show_payment_status()

```
```python
# Example structure for the Shape package using individual modules

# __init__.py

# Import all necessary classes to make them available at the package level
from .point import Point
from .line import Line
from .shape import Shape
from .rectangle import Rectangle
from .square import Square

# This file allows us to treat the Shape directory as a package

# 1. File: point.py
from math import sqrt

class Point:
    """Clase que representa un punto en un plano bidimensional."""
    def __init__(self, x: float = 0, y: float = 0):
        self._x = x
        self._y = y

    def get_x(self):
        return self._x

    def set_x(self, value):
        self._x = value

    def get_y(self):
        return self._y

    def set_y(self, value):
        self._y = value

    def compute_distance(self, other_point):
        return sqrt((self.get_x() - other_point.get_x())**2 + (self.get_y() - other_point.get_y())**2)


# 2. File: line.py
from point import Point
from math import sqrt

class Line:
    """Clase que representa una línea en un plano bidimensional."""
    def __init__(self, start_point: Point, end_point: Point):
        self._start_point = start_point
        self._end_point = end_point
        self._length = self.compute_length()

    def get_start_point(self):
        return self._start_point

    def set_start_point(self, value):
        self._start_point = value
        self._length = self.compute_length()

    def get_end_point(self):
        return self._end_point

    def set_end_point(self, value):
        self._end_point = value
        self._length = self.compute_length()

    def get_length(self):
        return self._length

    def compute_length(self):
        return self.get_start_point().compute_distance(self.get_end_point())


# 3. File: shape.py
from point import Point
from line import Line
from math import acos, degrees

class Shape:
    """Superclase que representa una figura geométrica."""
    def __init__(self, vertices: list[Point], edges: list[Line]):
        self.vertices = vertices
        self.edges = edges
        self.inner_angles = self.compute_inner_angles()
        self.is_regular = self.check_regular()

    def compute_area(self):
        raise NotImplementedError("Este método debe ser implementado por las subclases.")

    def compute_perimeter(self):
        return sum(edge.get_length() for edge in self.edges)

    def compute_inner_angles(self):
        """Calcula los ángulos internos (solo para polígonos convexos)."""
        angles = []
        for i in range(len(self.vertices)):
            p1 = self.vertices[i - 1]
            p2 = self.vertices[i]
            p3 = self.vertices[(i + 1) % len(self.vertices)]

            a = p1.compute_distance(p2)
            b = p2.compute_distance(p3)
            c = p1.compute_distance(p3)

            angle = acos((a**2 + b**2 - c**2) / (2 * a * b))
            angles.append(degrees(angle))
        return angles

    def check_regular(self):
        """Verifica si la figura es regular."""
        if len(self.edges) < 3:
            return False

        first_length = self.edges[0].get_length()
        first_angle = self.inner_angles[0]

        return all(edge.get_length() == first_length for edge in self.edges) and \
               all(angle == first_angle for angle in self.inner_angles)


# 4. File: rectangle.py
from shape import Shape
from point import Point
from line import Line

class Rectangle(Shape):
    """Clase que representa un rectángulo."""
    def __init__(self, bottom_left: Point, top_right: Point):
        width = top_right.get_x() - bottom_left.get_x()
        height = top_right.get_y() - bottom_left.get_y()

        vertices = [
            bottom_left,
            Point(top_right.get_x(), bottom_left.get_y()),
            top_right,
            Point(bottom_left.get_x(), top_right.get_y())
        ]

        edges = [
            Line(vertices[0], vertices[1]),
            Line(vertices[1], vertices[2]),
            Line(vertices[2], vertices[3]),
            Line(vertices[3], vertices[0])
        ]

        super().__init__(vertices, edges)
        self.width = width
        self.height = height

    def compute_area(self):
        return self.width * self.height


# 5. File: square.py
from rectangle import Rectangle
from point import Point

class Square(Rectangle):
    """Clase que representa un cuadrado (subclase de Rectángulo)."""
    def __init__(self, bottom_left: Point, side_length: float):
        top_right = Point(bottom_left.get_x() + side_length, bottom_left.get_y() + side_length)
        super().__init__(bottom_left, top_right)

    def compute_area(self):
        return self.width**2

```
```python
# Unique Module Inside the Shape Package

from math import sqrt, acos, degrees

class Point:
    """Clase que representa un punto en un plano bidimensional."""
    def __init__(self, x: float = 0, y: float = 0):
        self._x = x
        self._y = y

    def get_x(self):
        return self._x

    def set_x(self, value):
        self._x = value

    def get_y(self):
        return self._y

    def set_y(self, value):
        self._y = value

    def compute_distance(self, other_point):
        return sqrt((self.get_x() - other_point.get_x())**2 + (self.get_y() - other_point.get_y())**2)


class Line:
    """Clase que representa una línea en un plano bidimensional."""
    def __init__(self, start_point: Point, end_point: Point):
        self._start_point = start_point
        self._end_point = end_point
        self._length = self.compute_length()

    def get_start_point(self):
        return self._start_point

    def set_start_point(self, value):
        self._start_point = value
        self._length = self.compute_length()

    def get_end_point(self):
        return self._end_point

    def set_end_point(self, value):
        self._end_point = value
        self._length = self.compute_length()

    def get_length(self):
        return self._length

    def compute_length(self):
        return self.get_start_point().compute_distance(self.get_end_point())


class Shape:
    """Superclase que representa una figura geométrica."""
    def __init__(self, vertices: list[Point], edges: list[Line]):
        self.vertices = vertices
        self.edges = edges
        self.inner_angles = self.compute_inner_angles()
        self.is_regular = self.check_regular()

    def compute_area(self):
        raise NotImplementedError("Este método debe ser implementado por las subclases.")

    def compute_perimeter(self):
        return sum(edge.get_length() for edge in self.edges)

    def compute_inner_angles(self):
        """Calcula los ángulos internos (solo para polígonos convexos)."""
        angles = []
        for i in range(len(self.vertices)):
            p1 = self.vertices[i - 1]
            p2 = self.vertices[i]
            p3 = self.vertices[(i + 1) % len(self.vertices)]

            a = p1.compute_distance(p2)
            b = p2.compute_distance(p3)
            c = p1.compute_distance(p3)

            angle = acos((a**2 + b**2 - c**2) / (2 * a * b))
            angles.append(degrees(angle))
        return angles

    def check_regular(self):
        """Verifica si la figura es regular."""
        if len(self.edges) < 3:
            return False

        first_length = self.edges[0].get_length()
        first_angle = self.inner_angles[0]

        return all(edge.get_length() == first_length for edge in self.edges) and \
               all(angle == first_angle for angle in self.inner_angles)


class Rectangle(Shape):
    """Clase que representa un rectángulo."""
    def __init__(self, bottom_left: Point, top_right: Point):
        width = top_right.get_x() - bottom_left.get_x()
        height = top_right.get_y() - bottom_left.get_y()

        vertices = [
            bottom_left,
            Point(top_right.get_x(), bottom_left.get_y()),
            top_right,
            Point(bottom_left.get_x(), top_right.get_y())
        ]

        edges = [
            Line(vertices[0], vertices[1]),
            Line(vertices[1], vertices[2]),
            Line(vertices[2], vertices[3]),
            Line(vertices[3], vertices[0])
        ]

        super().__init__(vertices, edges)
        self.width = width
        self.height = height

    def compute_area(self):
        return self.width * self.height


class Square(Rectangle):
    """Clase que representa un cuadrado (subclase de Rectángulo)."""
    def __init__(self, bottom_left: Point, side_length: float):
        top_right = Point(bottom_left.get_x() + side_length, bottom_left.get_y() + side_length)
        super().__init__(bottom_left, top_right)

    def compute_area(self):
        return self.width**2


# Ejemplo de uso
if __name__ == "__main__":
    # Crear puntos
    p1 = Point(0, 0)
    p2 = Point(4, 4)

    # Crear un rectángulo
    rect = Rectangle(p1, p2)
    print(f"Área del rectángulo: {rect.compute_area()}")
    print(f"Perímetro del rectángulo: {rect.compute_perimeter()}")

    # Crear un cuadrado
    square = Square(p1, 4)
    print(f"Área del cuadrado: {square.compute_area()}")
    print(f"Perímetro del cuadrado: {square.compute_perimeter()}")
```
