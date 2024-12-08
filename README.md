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
