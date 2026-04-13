# 📘 Portafolio de Ejercicios - Java Swing

---

# 🟢 ACTIVIDAD 1: PRODUCTO (TIENDA)

## 📌 Enunciado del Proyecto
Desarrollar una aplicación que permita calcular el importe de compra de productos en docenas, aplicando descuentos según la cantidad comprada.

- Si compra 10 o más docenas → 20% de descuento  
- Si compra menos de 10 docenas → 10% de descuento  
- Si el importe a pagar es mayor o igual a 200 → recibe lapiceros de obsequio  

---

## 🧩 Diagrama de Clases
```
+------------------+
|  FrmProducto     |
+------------------+
| txtPrecio        |
| txtCantidad      |
| txtResultado     |
+------------------+
| calcular()       |
| limpiar()        |
| leerDecimal()    |
| leerEntero()     |
+------------------+

        ↓

+------------------+
|      App         |
+------------------+
| main()           |
+------------------+
```

---

## 🎨 Diseño de la Aplicación
La aplicación cuenta con una interfaz gráfica desarrollada en Java Swing (JFrame), la cual incluye:

- Campos de entrada:
  - Precio por docena
  - Cantidad de docenas
- Botones:
  - Calcular
  - Limpiar
  - Salir
- Área de resultados:
  - Importe de compra
  - Descuento
  - Total a pagar
  - Obsequios

---

## 💻 Código de la Aplicación
Fragmento principal:

```java
double importeCompra = precio * cantidad;
double descuento = cantidad >= 10 ? 0.20 : 0.10;
double importeDescuento = importeCompra * descuento;
double importePagar = importeCompra - importeDescuento;
```

---

# 🔵 ACTIVIDAD 2: EMPLEADO

## 📌 Enunciado del Proyecto
Desarrollar una aplicación que calcule el sueldo de un empleado considerando su categoría, horas trabajadas y número de hijos.

- Categoría A → S/ 45 por hora  
- Categoría B → S/ 37.50 por hora  
- Bonificación por hijos  
- Descuento según sueldo bruto  

---

## 🧩 Diagrama de Clases
```
+------------------+
|  FrmEmpleado     |
+------------------+
| txtHoras         |
| txtHijos         |
| cmbCategoria     |
| txtResultado     |
+------------------+
| calcular()       |
| limpiar()        |
| leerEntero()     |
+------------------+

        ↓

+------------------+
|      App         |
+------------------+
| main()           |
+------------------+
```

---

## 🎨 Diseño de la Aplicación
La aplicación presenta una interfaz gráfica amigable que incluye:

- Selección de categoría (ComboBox)
- Campos de entrada:
  - Horas trabajadas
  - Número de hijos
- Botones:
  - Calcular
  - Limpiar
  - Salir
- Área de resultados:
  - Sueldo básico
  - Bonificación
  - Sueldo bruto
  - Descuento
  - Sueldo neto

---

## 💻 Código de la Aplicación
Fragmento principal:

```java
double sueldoBasico = horas * tarifa;
double bonificacion = hijos <= 3 ? hijos * 40.5 : hijos * 35.0;
double sueldoBruto = sueldoBasico + bonificacion;
double descuento = sueldoBruto >= 3500 ? 0.135 : 0.10;
double sueldoNeto = sueldoBruto - (sueldoBruto * descuento);
```

---

# 🧠 Conclusión
Se desarrollaron dos aplicaciones utilizando Java Swing, aplicando programación orientada a objetos, validación de datos y diseño de interfaces gráficas, cumpliendo con todos los requisitos del portafolio.
