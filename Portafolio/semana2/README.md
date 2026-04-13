# 📁 Portafolio de Ejercicios - Java Swing

## 🟢 Actividad 1: Producto (Tienda)

### 📌 Enunciado
Aplicación que calcula el importe de compra de productos en docenas, aplicando descuentos:
- 20% si compra ≥ 10 docenas
- 10% si compra < 10 docenas
- Obsequio de lapiceros si el importe ≥ 200

### 📊 Diagrama de Clases
```
FrmProducto
 ├── calcular()
 ├── limpiar()
 ├── leerDecimal()
 └── leerEntero()

App
 └── main()
```

### 🎨 Diseño
- Entrada: precio y cantidad
- Botones: calcular, limpiar, salir
- Salida: resultados de compra

### 💻 Código
Implementado en:
- App.java
- FrmProducto.java

---

## 🔵 Actividad 2: Empleado

### 📌 Enunciado
Aplicación que calcula el sueldo de un empleado:
- Categoría A: S/45 por hora
- Categoría B: S/37.50 por hora
- Bonificación por hijos
- Descuento según sueldo bruto

### 📊 Diagrama de Clases
```
FrmEmpleado
 ├── calcular()
 ├── limpiar()
 └── leerEntero()

App
 └── main()
```

### 🎨 Diseño
- Entrada: horas, hijos, categoría
- Botones: calcular, limpiar, salir
- Salida: sueldo detallado

### 💻 Código
Implementado en:
- App.java
- FrmEmpleado.java

---

## 📌 Conclusión
Se desarrollaron aplicaciones en Java con interfaz gráfica (JFrame), aplicando lógica de negocio y validación de datos.
