## clases y objetos 
las clases son como plantillas para crear objetos

un objeto es una instancia de una clase


Una clase persona que tiene un constructor y un metodo saludar

class Persona:  
    def __init__(self, nombre, edad):  
        self.nombre = nombre  
        self.edad = edad  
  
    def saludar(self):  
        print("Hola, soy", self.nombre)  

Un objeto de la clase persona que estamos instanciando para poder usar en este caso pasamos los parametros al constructor y usamos el metodo saluda
# Crear objeto  
p1 = Persona("Ana", 25)  
  
p1.saludar()

## Decoradores
un decorador es una funciona que modifica otra sin cambiar su codigo se usa con @

aqui declaro me funcion
def mi_decorador(func):
    def wrapper():
        print("Antes de ejecutar")
        func()
        print("Después de ejecutar")
    return wrapper

aqui la mando llamar y la peronalizo 
@mi_decorador
def saludar():
    print("Hola")

saludar()


func y wrapper son parte clave para entender como una funcion puede moficar el comportamiento de otra funcion

func
es la funcion original que queremos decorar o modificar cuando usas un decorador con @ python pasa automaticamente la funcion original como argumento al decorador

def mi_decorador(func):
    print("Decorando la función")