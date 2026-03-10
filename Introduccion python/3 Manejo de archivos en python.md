# 📂 Manejo de archivos en Python

Python puede **leer y escribir archivos**.

### Abrir archivo

archivo = open("datos.txt", "r")  
contenido = archivo.read()  
print(contenido)  
archivo.close()

### Forma recomendada

with open("datos.txt", "r") as archivo:  
    contenido = archivo.read()  
    print(contenido)

### Modos

|modo|significado|
|---|---|
|r|leer|
|w|escribir|
|a|agregar|
|rb|leer binario|

# 1️⃣ ¿Qué es manejar archivos?

El **manejo de archivos (file handling)** es cuando un programa puede:

- **leer archivos**
    
- **escribir archivos**
    
- **modificar archivos**
    
- **crear archivos**
    

Ejemplos reales:

- guardar logs
    
- leer configuraciones
    
- guardar resultados
    
- procesar datos
    

---

# 2️⃣ Abrir un archivo

Para trabajar con un archivo primero debes **abrirlo**.

archivo = open("datos.txt", "r")

Esto hace 3 cosas:

1 Python busca el archivo  
2 lo abre en memoria  
3 devuelve un objeto archivo

Entonces:

archivo = objeto tipo file

---

# 3️⃣ Leer el archivo

contenido = archivo.read()

Esto significa:

leer todo el archivo

Ejemplo archivo `datos.txt`:

Hola  
Python  
Archivos

Código:

archivo = open("datos.txt", "r")  
contenido = archivo.read()  
  
print(contenido)  
  
archivo.close()

Salida:

Hola  
Python  
Archivos

---

# 4️⃣ Cerrar el archivo

archivo.close()

Esto es **muy importante** porque:

- libera memoria
    
- evita errores
    
- libera el archivo para otros programas
    

Si no lo cierras puedes tener problemas.

---

# 5️⃣ Forma moderna: `with open`

La forma recomendada es:

with open("datos.txt", "r") as archivo:  
    contenido = archivo.read()  
    print(contenido)

Esto hace lo mismo pero **Python cierra el archivo automáticamente**.

Internamente pasa esto:

open()  
↓  
usar archivo  
↓  
close() automático

---

# 6️⃣ Modos de apertura

Cuando abres un archivo debes decir **cómo lo vas a usar**.

## r → read

Leer archivo.

open("datos.txt", "r")

⚠️ Error si el archivo no existe.

---

## w → write

Escribir archivo.

open("datos.txt", "w")

⚠️ Importante:

borra todo el contenido anterior

Ejemplo:

with open("datos.txt", "w") as archivo:  
    archivo.write("Hola mundo")

Archivo final:

Hola mundo

---

## a → append

Agregar contenido al final.

open("datos.txt", "a")

Ejemplo:

with open("datos.txt", "a") as archivo:  
    archivo.write("\nNueva línea")

Archivo:

Hola  
Python  
Nueva línea

---

## rb → read binary

Leer archivos binarios.

Ejemplo:

- imágenes
    
- pdf
    
- videos
    

with open("imagen.jpg", "rb") as archivo:  
    datos = archivo.read()

Aquí los datos no son texto, son **bytes**.

---

# 7️⃣ Escribir en archivos

Ejemplo simple:

with open("archivo.txt", "w") as archivo:  
    archivo.write("Hola\n")  
    archivo.write("Python\n")

Resultado archivo:

Hola  
Python

---

# 8️⃣ Leer línea por línea

A veces el archivo es grande y no quieres cargar todo.

with open("datos.txt", "r") as archivo:  
    for linea in archivo:  
        print(linea)

Esto lee **una línea a la vez**.

Ejemplo salida:

Hola  
Python  
Archivos

---

# 9️⃣ Leer todas las líneas

with open("datos.txt", "r") as archivo:  
    lineas = archivo.readlines()  
  
print(lineas)

Resultado:

['Hola\n', 'Python\n', 'Archivos\n']

Es una **lista de líneas**.

---

# 🔟 Escribir listas

lineas = ["uno\n", "dos\n", "tres\n"]  
  
with open("numeros.txt", "w") as archivo:  
    archivo.writelines(lineas)

Archivo:

uno  
dos  
tres

---

# 11️⃣ Saber si un archivo existe

import os  
  
if os.path.exists("datos.txt"):  
    print("Existe")  
else:  
    print("No existe")

---

# 12️⃣ Ejemplo real completo

Programa que guarda usuarios.

nombre = input("Nombre: ")  
  
with open("usuarios.txt", "a") as archivo:  
    archivo.write(nombre + "\n")  
  
print("Usuario guardado")

Archivo:

Ana  
Luis  
Carlos

---

# 13️⃣ Cosas importantes que debes recordar

### 1

Siempre usa:

with open()

---

### 2

Diferencia:

w → borra archivo  
a → agrega contenido

---

### 3

Tipos de lectura:

read() → todo el archivo  
readline() → una línea  
readlines() → lista de líneas

---

# 14️⃣ Diagrama simple

archivo.txt  
     ↓  
open()  
     ↓  
objeto archivo  
     ↓  
read() / write()  
     ↓  
close()

---

# 15️⃣ Tipos de archivos que puedes manejar

Python puede leer:

txt  
csv  
json  
xml  
imagenes  
pdf  
logs