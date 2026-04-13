# 📘 Portafolio de Ejercicios - Java Swing

## 👨‍💻 Autor
- Nombre: ______________________
- Curso: Programación Orientada a Objetos
- Fecha: ______________________

---

# 🟢 Actividad 1: Sistema de Venta (Producto)

## 📌 Enunciado
Desarrollar una aplicación que calcule el importe de compra de productos en docenas, aplicando descuentos según la cantidad adquirida.

## ⚙️ Reglas del Negocio

| Condición | Resultado |
|----------|----------|
| ≥ 10 docenas | 20% de descuento |
| < 10 docenas | 10% de descuento |
| Importe ≥ 200 | Obsequio de lapiceros |

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

## 🎨 Diseño de la Interfaz

- 📥 Entrada:
  - Precio por docena
  - Cantidad de docenas
- 🔘 Botones:
  - Calcular
  - Limpiar
  - Salir
- 📤 Salida:
  - Importe de compra
  - Descuento aplicado
  - Total a pagar
  - Obsequios

---

## 💻 Lógica del Sistema

```java
double importeCompra = precio * cantidad;
double descuento = cantidad >= 10 ? 0.20 : 0.10;
double total = importeCompra - (importeCompra * descuento);
```

---

# 🔵 Actividad 2: Sistema de Sueldo (Empleado)

## 📌 Enunciado
Desarrollar una aplicación que calcule el sueldo de un empleado según su categoría, horas trabajadas y número de hijos.

---

## ⚙️ Reglas del Negocio

### Categoría

| Categoría | Pago por hora |
|----------|--------------|
| A | S/ 45.00 |
| B | S/ 37.50 |

### Bonificación

| Hijos | Bonificación |
|------|-------------|
| ≤ 3 | S/ 40.5 por hijo |
| > 3 | S/ 35.0 por hijo |

### Descuento

| Sueldo Bruto | Descuento |
|-------------|----------|
| ≥ 3500 | 13.5% |
| < 3500 | 10% |

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

## 🎨 Diseño de la Interfaz

- 📥 Entrada:
  - Horas trabajadas
  - Número de hijos
  - Categoría (ComboBox)
- 🔘 Botones:
  - Calcular
  - Limpiar
  - Salir
- 📤 Salida:
  - Sueldo básico
  - Bonificación
  - Sueldo bruto
  - Descuento
  - Sueldo neto

---

## 💻 Lógica del Sistema

```java
double sueldoBasico = horas * tarifa;
double bonificacion = hijos <= 3 ? hijos * 40.5 : hijos * 35.0;
double sueldoBruto = sueldoBasico + bonificacion;
double descuento = sueldoBruto >= 3500 ? 0.135 : 0.10;
double sueldoNeto = sueldoBruto - (sueldoBruto * descuento);
```

---

# 🧠 Conclusión

Se desarrollaron dos aplicaciones utilizando Java Swing, aplicando:

- Programación Orientada a Objetos
- Interfaces gráficas con JFrame
- Validación de datos
- Lógica de negocio

Estas aplicaciones permiten automatizar cálculos reales de manera eficiente.

---

# 🚀 Cómo ejecutar

1. Abrir el proyecto en NetBeans
2. Ejecutar la clase `App.java`
3. Ingresar los datos
4. Presionar **Calcular**

---

# 📎 Evidencias (opcional)

👉 Aquí puedes agregar capturas de pantalla del programa funcionando
