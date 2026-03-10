# 1️⃣ Declaración XML

Tu archivo empieza con:

<?xml version="1.0" encoding="UTF-8"?>

Esto se llama **declaración XML**.

|Parte|Significado|
|---|---|
|`version="1.0"`|versión del estándar XML|
|`encoding="UTF-8"`|codificación de caracteres|

No es obligatorio, pero **es buena práctica**.

---

# 2️⃣ Elemento raíz

<odoo>

En XML **solo puede existir un elemento raíz**.

Tu árbol empieza aquí.

Estructura simplificada:

odoo  
 └── data  
      ├── record  
      ├── record  
      ├── record  
      └── menuitem

Todo lo demás **vive dentro de `<odoo>`**.

---

# 3️⃣ Segundo nivel: `<data>`

<data noupdate="0">

Aquí vemos **un elemento con atributo**.

### Elemento

data

### Atributo

noupdate="0"

En Odoo significa:

|Valor|Significado|
|---|---|
|`0`|se puede actualizar|
|`1`|no se sobrescribe en upgrades|

---

# 4️⃣ Elementos `<record>`

El XML de Odoo **define registros de base de datos**.

Ejemplo:

<record id="report_iva_cliente_cash" model="account.report">

Aquí vemos **dos atributos**.

|atributo|significado|
|---|---|
|`id`|identificador XML|
|`model`|modelo Odoo|

---

## Visualmente

record  
 ├─ id="report_iva_cliente_cash"  
 └─ model="account.report"

Esto significa:

👉 crear un registro en el modelo

account.report

---

# 5️⃣ Elementos `<field>`

Dentro del record aparecen campos:

<field name="name">IVA por Cliente (Flujo Fiscal)</field>

Aquí tenemos:

|parte|significado|
|---|---|
|`field`|campo del modelo|
|`name="name"`|nombre del campo|
|texto|valor|

---

## Estructura real

record  
 └── field  
      ├─ name="name"  
      └─ valor = "IVA por Cliente..."

---

# 6️⃣ Campo con atributo `ref`

Ejemplo:

<field name="report_id" ref="report_iva_cliente_cash"/>

Esto significa:

👉 **referenciar otro registro XML**

En tu archivo:

report_iva_cliente_cash

Que fue creado aquí:

<record id="report_iva_cliente_cash" model="account.report">

Entonces el XML está conectando:

account.report.line  
        ↓  
account.report

---

# 7️⃣ Campo con atributo `eval`

Ejemplo:

<field name="filter_date_range" eval="True"/>

Aquí **no hay texto**, el valor se evalúa en Python.

|atributo|significado|
|---|---|
|`eval="True"`|booleano True|

---

# 8️⃣ Ejemplo completo de record

<record id="iva_cliente_cash_root_line" model="account.report.line">

Campos dentro:

report_id  
name  
sequence

Estructura:

record  
 ├─ id  
 ├─ model  
 ├─ field report_id  
 ├─ field name  
 └─ field sequence

---

# 9️⃣ Muchos records iguales

Luego tienes muchos registros de tipo:

account.report.column

Ejemplo:

<record id="col_partner" model="account.report.column">

Estos crean **columnas del reporte**.

Campos típicos:

|campo|significado|
|---|---|
|name|nombre de la columna|
|expression_label|clave usada por el handler Python|
|figure_type|tipo de dato|
|sequence|orden|

---

# 🔟 Ejemplo desglosado

<record id="col_partner" model="account.report.column">

Atributos:

id = col_partner  
model = account.report.column

Campos:

report_id  
name  
expression_label  
figure_type  
sequence

---

# 11️⃣ Ejemplo de atributo importante

<field name="figure_type">float</field>

Define el tipo de dato que el reporte mostrará.

|tipo|significado|
|---|---|
|string|texto|
|float|número|
|date|fecha|

---

# 12️⃣ Elemento `<menuitem>`

Al final:

<menuitem  
    id="menu_report_iva_cliente_cash"

Esto crea un **menú en Odoo**.

Atributos:

|atributo|significado|
|---|---|
|id|id XML|
|name|texto visible|
|parent|menú padre|
|action|acción ejecutada|
|groups|permisos|

---

# 13️⃣ Relación completa del XML

Tu XML crea:

Reporte  
   ↓  
Línea raíz  
   ↓  
Columnas  
   ↓  
Acción  
   ↓  
Menú

---

# 14️⃣ Árbol XML simplificado

odoo  
 └── data  
      ├── record (account.report)  
      │  
      ├── record (report.line)  
      │  
      ├── record (report.column)  
      │  
      ├── record (report.column)  
      │  
      ├── record (ir.actions.act_window)  
      │  
      └── menuitem

---

# 15️⃣ XPath aplicado a TU XML

Ejemplos reales:

### Todos los records

//record

---

### Todos los records del modelo column

//record[@model='account.report.column']

---

### Obtener nombres de columnas

//record[@model='account.report.column']/field[@name='name']

---

### Obtener el menú

//menuitem

---

### Obtener la acción

//record[@model='ir.actions.act_window']

---

# 16️⃣ XPath para encontrar una columna específica

Por ejemplo:

col_iva

XPath:

//record[@id='col_iva']

---

# 17️⃣ XPath para obtener el label

//record[@id='col_iva']/field[@name='expression_label']

Resultado:

iva

---

# 18️⃣ XPath para todas las columnas float

//record[@model='account.report.column']/field[text()='float']

---

# 19️⃣ XPath para columnas del reporte específico

//record[field[@name='report_id']]

---

# 20️⃣ XPath para obtener el orden

//record[@model='account.report.column']/field[@name='sequence']

---

# 🚀 Conclusión importante sobre TU XML

Tu archivo **no es solo XML**, es:

XML + ORM de Odoo

Cada `<record>`:

INSERT / UPDATE en la base de datos

---

# Si quieres, en el siguiente paso puedo explicarte algo MUY importante para Odoo

Te puedo mostrar:

### 🔥 Cómo Odoo realmente interpreta este XML internamente

XML → ORM → PostgreSQL