![[nodetree.gif]]![[Pasted image 20260310162936.png]]![[samplexml.webp]]
XML (**Extensible Markup Language**) es un formato de texto usado para **almacenar y transportar datos**.  
Se organiza como **un árbol jerárquico de elementos**.

### Ejemplo básico

<libros>  
    <libro>  
        <titulo>Don Quijote</titulo>  
        <autor>Miguel de Cervantes</autor>  
        <anio>1605</anio>  
    </libro>  
</libros>

### Partes importantes

- **Elemento raíz (root)**
    
    <libros>
    
    Todo XML debe tener **un solo elemento raíz**.
    
- **Elementos hijos**
    
    <libro>
    
- **Elementos hoja**
    
    <titulo>Don Quijote</titulo>
    

### Visualmente el árbol sería

libros  
 └── libro  
      ├── titulo  
      ├── autor  
      └── anio

---

# 2. Atributos en XML

Los **atributos** agregan información adicional a un elemento.

### Ejemplo

<libro id="1" categoria="novela">  
    <titulo>Don Quijote</titulo>  
    <autor>Miguel de Cervantes</autor>  
</libro>

Aquí:

- `id="1"`
    
- `categoria="novela"`
    

son **atributos del elemento `<libro>`**.

### Reglas importantes

✔ Siempre van dentro de la etiqueta de apertura  
✔ Siempre tienen valor entre comillas  
✔ No pueden repetirse con el mismo nombre

Ejemplo incorrecto ❌

<libro id="1" id="2">


3. XPath
**XPath** es un lenguaje para **buscar elementos dentro de un XML**.

Es parecido a navegar carpetas en un sistema de archivos.

---

## Ejemplo XML

<libros>  
    <libro id="1">  
        <titulo>Don Quijote</titulo>  
        <autor>Cervantes</autor>  
    </libro>  
  
    <libro id="2">  
        <titulo>Cien años de soledad</titulo>  
        <autor>García Márquez</autor>  
    </libro>  
</libros>

---

## Ejemplos de XPath

### Seleccionar todos los libros

/libros/libro

---

### Seleccionar todos los títulos

/libros/libro/titulo

---

### Seleccionar libro con id=2

/libros/libro[@id='2']

---

### Obtener el autor del libro 1

/libros/libro[@id='1']/autor

---

### Seleccionar todos los atributos id

/libros/libro/@id

---

# Resumen rápido

|Concepto|Qué es|
|---|---|
|**XML**|Formato para almacenar datos|
|**Elemento**|Etiqueta con contenido|
|**Atributo**|Propiedad de un elemento|
|**XPath**|Lenguaje para buscar nodos en XML|

---

💡 **Idea clave:**  
XML = **datos estructurados en forma de árbol**, y XPath es la **forma de navegar ese árbol**.
