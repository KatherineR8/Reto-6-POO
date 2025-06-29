# Reto 6 POO
### Katherine Restrepo

#### 1. Add the required exceptions in the Reto 1 code assigments.
```python
#punto 1
def operacion(num1:float, num2:float,operador:str)-> float: #define una funcion que en base al operador recibido realiza una operacion
    if operador== "+":
        resultado= num1+num2
    elif operador=="-":
        resultado= num1-num2
    elif operador=="*":
        resultado= num1*num2
    elif operador== "/":
        resultado= num1/num2
        if num2==0:
            raise ValueError("No se puede dividir por cero")
        if not isinstance(num1, (int, float)) or not isinstance(num2, (int, float)):
            raise ValorInvalidoException("Los valores deben ser números.")
    else:
        print("No se esta definiendo niguna operacion valida")
    return resultado


if __name__ == "__main__":
  #El usuario ingresa los valores de las variables
  num1 = float(input("Ingrese el primer numero (en caso de ser esta o division el minuendo o dividendo respectivamente):"))
  num2 = float(input("Ingrese el segundo numero:"))
  operador = str(input("Ingrese el operador de la operacion que desea realizar:"))
  
  #se llama a la funcion y se da el resultado de la operacion
  #
  try:
        resultado = operacion(num1,num2,operador)
        print(resultado)
  except TypeError:
      print("Se introdujo un valor no numerico")

#punto 2
# se crea la condicion para que mientras la letra de izquierda a derecha este antes
# que la letra que esta en sentido contrario se verifique si estas son iguales, de no ser 
# asi se toma como que no es un palinodromo
def punto2(palabra:str):
    lista_palabra=list(palabra)
    adelante=0
    atras= len(palabra)-1
    bandera=True
    while adelante < atras:
        if lista_palabra[adelante] != lista_palabra[atras]:
            bandera=False
            adelante += 1
            atras -= 1

    if bandera==True:
        return print("La palabra es un palinodromo")
    else:
        return print("La palabra no es un palinodromo")

try:
    #El usuario ingresa la palabra y el programa la vuelve una lista
    palabra="hola"
    punto2(palabra)
except TypeError:
    print("No se ingreso una palabra")

    #punto 3
# Escribir una función que reciba una lista de números y devuelva solo aquellos que son primos. 
#La función debe recibir una lista de enteros y retornar solo aquellos que sean primos.

def numeros_primos(lista) -> list:
    lista_primos=[]
    
    for n in lista:
        if n < 2:
            continue
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                break
        else:
            lista_primos.append(n)
    return lista_primos


if __name__ == "__main__":
    try:
        lista_num=[]
        cantidad_num=int(input("De la cantidad de numeros que va a ingresar"))
        for n in range(cantidad_num):
            dato = int(input("Ingresa un dato"))
            lista_num.append(dato)
            
        primos=numeros_primos(lista_num)
        print(primos)
    except TypeError:
        print("Se introdujo un valor no numerico")

#punto 4
def mayor_suma(lista)-> int:
    suma_mayor=lista[0]+lista[1]

    for i in range(1,len(lista)-1):
        suma=lista_num[i]+lista_num[(i+1)]
        if suma>suma_mayor:
            suma_mayor=suma

    return suma_mayor



if __name__ == "__main__":
    try:

        lista_num=[]
        cantidad_num=int(input("De la cantidad de numeros que va a ingresar"))
        for n in range(cantidad_num):
            dato = int(input("Ingresa un dato"))
            lista_num.append(dato)
            

        respuesta=mayor_suma(lista_num)
        print(respuesta)
    except TypeError:
        print("Se introdujo un valor no numerico")

#punto 5
def mismas_letras(lista_palabras: list) -> list:

  palabras = {} # diccionario vacio para guardar las palabras con el mismo orden lexicografico
  resultado = [] # lista vacia para palabras con las mismas letras

  for word in lista_palabras:
    valor = "".join(sorted(word)) # Ordena la palabra lexicograficamente y guarda la palabra original
    if valor in palabras.keys():
      palabras[valor] += [word]
    else:
      palabras[valor] = [word]
  
  for value in palabras.values(): # si tiene dos o mas palabras, estas tienen las mismas letras
    if len(value) >= 2:
      resultado += value

  return resultado 

if __name__ == "__main__":
  try:
    test_list : list = ["roma", "amor", "perro", "ropa", "pora", "mora", "juan", "porre"]
    print(mismas_letras(test_list))
  except TypeError:
    print(("No se ingresaron palabras"))
```
#### 2. In the package Shape identify at least cases where exceptions are needed (maybe when validate input data, or math procedures) explain them clearly using comments and add them to the code.

```python
from Shape.shape import Shape

class Rectangle(Shape):
    def __init__(self, ancho:float, alto:float):
        super().__init__()
        self.ancho=ancho
        self.alto= alto
        if self.alto <= 0 or self.ancho<= 0:
           raise ValueError
    
    def compute_area(self):
        return self.ancho* self.alto
    
    def compute_perimeter(self):
        return 2*self.alto+ 2*self.ancho
    
    def compute_inner_angles(self):
       return 360/4
    
class Square(Rectangle):
    def __init__(self, lado:float):
        super().__init__()
        self.lado=lado
        if self.lado <= 0 :
           raise ValueError
    
    def compute_area(self)-> float:
        return self.lado**2
    
    def compute_perimeter(self)-> float:
        return 4* self.lado
    
    def compute_inner_angles(self):
       return super().compute_inner_angles()
    
class Triangle(Shape):
    def __init__(self, base:float, altura:float):
      super().__init__()
      self.base=base
      self.altura=altura
      if self.base <= 0 or self.altura<=0:
           raise ValueError
    
    def compute_area(self):
       return self.base*self.altura/2

    def compute_perimeter(self):
       pass

    def compute_inner_angles(self):
       pass
    
class Equilatero(Triangle):
    def __init__(self, lado,base,altura):
      super().__init__()
      self.lado=self.lado
      self.base=self.lado
      self.altura= self.lado*(3/2)**1/2
      if self.base <= 0 or self.altura<=0 or self.lado<=0:
           raise ValueError

    def compute_area(self):
       return super().compute_area()

    def compute_perimeter(self):
       return self.lado*3
    
    def compute_inner_angles(self):
       return 180/3
    
class Isoceles(Triangle):
    def __init__(self, lado,base,altura):
      super().__init__()
      self.lado=self.lado
      self.base=self.base
      self.altura= self.lado**(2)- (self.base/2)**2
      if self.base <= 0 or self.altura<=0 or self. lado <=0:
           raise ValueError

    def compute_area(self):
       return super().compute_area()

    def compute_perimeter(self):
       return self.lado*2 + self.base
    
    def compute_inner_angles(self):
       pass

class Escaleno(Triangle):
    def __init__(self, lado1, lado2,base):
      super().__init__()
      self.lado1=self.lado1
      self.lado2=self.lado2
      self.base=self.base
      if self.base <= 0 or self.lado1<=0 or self.lado2<=0:
           raise ValueError
      

    def compute_area(self):
       semiperimetro=(self.lado1 + self.lado2+ self.base)/2
       return (semiperimetro(semiperimetro-self.lado1)(semiperimetro-self.lado2)(semiperimetro-self.base))**1/2

    def compute_perimeter(self):
       return self.lado1 + self.lado2+ self.base
    
    def compute_inner_angles(self):
       pass

class TriRectangle(Triangle):
    def __init__(self, cateto_ady, cateto_op,hipotenusa,altura):
      super().__init__()
      self.cateto_ady=self.cateto_ady
      self.cateto_op=self.cateto_op
      self.hipoteusa=self.hipoteusa
      self.altura= (self.cateto_op*self.cateto_ady)/self.hipoteusa
      if self.cateto_ady <= 0 or self.cateto_op<=0 or self.hipoteusa <=0:
           raise ValueError

    def compute_area(self):
       return super().compute_area()

    def compute_perimeter(self):
       return self.cateto_ady + self.cateto_op+ self.hipoteusa
    
    def compute_inner_angles(self):
       pass
```
