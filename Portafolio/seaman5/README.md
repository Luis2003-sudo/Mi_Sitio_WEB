# 📁 Portafolio de Ejercicios
### Actividad N° 02 — Métodos | Apache Maven

| | |
|---|---|
| **Universidad** | Universidad Peruana Los Andes |
| **Facultad** | Ingeniería de Sistemas y Computación |
| **Curso** | Desarrollo de Aplicaciones I |
| **Tecnología** | Apache Maven + Java Swing |
| **Tema** | Métodos |

---

## Índice

- [Ejercicio 01 — Venta de Producto con Descuento y Lapiceros](#ejercicio-01--venta-de-producto-con-descuento-y-lapiceros)
- [Ejercicio 02 — Cálculo de Sueldo de Empleado](#ejercicio-02--cálculo-de-sueldo-de-empleado)

---

## Ejercicio 01 — Venta de Producto con Descuento y Lapiceros

### 1. Enunciado del proyecto

Una tienda ha puesto en oferta la venta de un producto ofreciendo un porcentaje de descuento sobre el importe de la compra de acuerdo con la siguiente tabla:

| Docenas adquiridas | Descuento |
|:---:|:---:|
| ≥ 10 | 20% |
| < 10 | 10% |

Adicionalmente, la tienda obsequia lapiceros de acuerdo con la siguiente tabla:

| Importe a pagar | Lapiceros |
|:---:|:---:|
| ≥ 200 | 2 por cada docena |
| < 200 | 0 |

Dado el precio de la docena y la cantidad de docenas adquiridas, diseñe un programa que determine el importe de la compra, el importe del descuento, el importe a pagar y la cantidad de lapiceros de obsequio.

---

### 2. Diagrama de clases

```
┌─────────────────────────────┐
│            App              │
├─────────────────────────────┤
│ + main(String[] args): void │
└─────────────┬───────────────┘
              │ crea y muestra
              ▼
┌──────────────────────────────────────────┐
│              FrmProducto                 │
├──────────────────────────────────────────┤
│ - txtPrecioDocena: JTextField            │
│ - txtCantidadDocenas: JTextField         │
│ - txtResultado: JTextArea                │
│ - formato: DecimalFormat                 │
├──────────────────────────────────────────┤
│ + FrmProducto()                          │
│ - configurarVentana(): void              │
│ - agregarComponentes(): void             │
│ - calcular(): void                       │
│ - leerDecimal(String, String): double    │
│ - leerEntero(String, String): int        │
│ - limpiar(): void                        │
│ - mostrarError(String): void             │
└──────────────────────────────────────────┘
```

---

### 3. Diseño de la aplicación

La aplicación fue diseñada con una ventana JFrame titulada **"Tienda - Descuento y Lapiceros de Obsequio"**.

**Componentes principales:**
- Título principal: "Venta de Producto con Descuento"
- Campo de texto para ingresar el precio de la docena
- Campo de texto para ingresar la cantidad de docenas
- Botón **Calcular**: realiza todos los cálculos
- Botón **Limpiar**: borra los datos ingresados y los resultados
- Botón **Salir**: cierra la ventana
- Área de resultados: muestra importe de compra, descuento, importe a pagar y lapiceros de obsequio

**Proceso de cálculo:**
```
importeCompra    = precioDocena × cantidadDocenas
pctDescuento     = (cantidadDocenas >= 10) ? 20% : 10%
importeDescuento = importeCompra × pctDescuento
importePagar     = importeCompra − importeDescuento
lapiceros        = (importePagar >= 200) ? 2 × cantidadDocenas : 0
```

---

### 4. Código de la aplicación

#### Archivo: `App.java`

```java
package com.tienda.producto;

import javax.swing.SwingUtilities;

public class App {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            FrmProducto ventana = new FrmProducto();
            ventana.setVisible(true);
        });
    }
}
```

#### Archivo: `FrmProducto.java`

```java
package com.tienda.producto;

import java.awt.*;
import java.text.DecimalFormat;
import javax.swing.*;

public class FrmProducto extends JFrame {

    private final JTextField txtPrecioDocena;
    private final JTextField txtCantidadDocenas;
    private final JTextArea  txtResultado;
    private final DecimalFormat formato;

    public FrmProducto() {
        formato            = new DecimalFormat("S/ #,##0.00");
        txtPrecioDocena    = new JTextField(12);
        txtCantidadDocenas = new JTextField(12);
        txtResultado       = new JTextArea(6, 30);
        configurarVentana();
        agregarComponentes();
    }

    private void configurarVentana() {
        setTitle("Tienda - Descuento y Lapiceros de Obsequio");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(520, 420);
        setLocationRelativeTo(null);
        setResizable(false);
        getContentPane().setBackground(new Color(245, 247, 250));
    }

    private void agregarComponentes() {
        JLabel titulo = new JLabel("Venta de Producto con Descuento", SwingConstants.CENTER);
        titulo.setFont(new Font("Arial", Font.BOLD, 20));
        titulo.setForeground(new Color(11, 61, 143));
        titulo.setBorder(BorderFactory.createEmptyBorder(15, 10, 10, 10));
        add(titulo, BorderLayout.NORTH);

        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBackground(new Color(245, 247, 250));
        panel.setBorder(BorderFactory.createEmptyBorder(10, 30, 10, 30));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(8, 8, 8, 8);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        JLabel lblPrecio   = new JLabel("Precio de la docena (S/.):");
        JLabel lblCantidad = new JLabel("Cantidad de docenas:");
        lblPrecio.setFont(new Font("Arial", Font.PLAIN, 14));
        lblCantidad.setFont(new Font("Arial", Font.PLAIN, 14));
        txtPrecioDocena.setFont(new Font("Arial", Font.PLAIN, 14));
        txtCantidadDocenas.setFont(new Font("Arial", Font.PLAIN, 14));

        JButton btnCalcular = new JButton("Calcular");
        JButton btnLimpiar  = new JButton("Limpiar");
        JButton btnSalir    = new JButton("Salir");
        btnCalcular.setFont(new Font("Arial", Font.BOLD, 13));
        btnLimpiar.setFont(new Font("Arial", Font.BOLD, 13));
        btnSalir.setFont(new Font("Arial", Font.BOLD, 13));

        btnCalcular.addActionListener(e -> calcular());
        btnLimpiar.addActionListener(e -> limpiar());
        btnSalir.addActionListener(e -> dispose());

        txtResultado.setEditable(false);
        txtResultado.setFont(new Font("Monospaced", Font.PLAIN, 13));
        txtResultado.setBackground(Color.WHITE);
        txtResultado.setBorder(BorderFactory.createEmptyBorder(8, 8, 8, 8));

        gbc.gridx = 0; gbc.gridy = 0;
        panel.add(lblPrecio, gbc);
        gbc.gridx = 1;
        panel.add(txtPrecioDocena, gbc);

        gbc.gridx = 0; gbc.gridy = 1;
        panel.add(lblCantidad, gbc);
        gbc.gridx = 1;
        panel.add(txtCantidadDocenas, gbc);

        JPanel panelBotones = new JPanel();
        panelBotones.setBackground(new Color(245, 247, 250));
        panelBotones.add(btnCalcular);
        panelBotones.add(btnLimpiar);
        panelBotones.add(btnSalir);

        gbc.gridx = 0; gbc.gridy = 2; gbc.gridwidth = 2;
        panel.add(panelBotones, gbc);

        gbc.gridy = 3;
        gbc.fill = GridBagConstraints.BOTH;
        gbc.weightx = 1; gbc.weighty = 1;
        panel.add(new JScrollPane(txtResultado), gbc);

        add(panel, BorderLayout.CENTER);
    }

    private void calcular() {
        try {
            double precio  = leerDecimal(txtPrecioDocena.getText(), "precio de la docena");
            int cantidad   = leerEntero(txtCantidadDocenas.getText(), "cantidad de docenas");

            if (precio   <= 0) { mostrarError("El precio debe ser mayor que cero.");   return; }
            if (cantidad <= 0) { mostrarError("La cantidad debe ser mayor que cero."); return; }

            double importeCompra    = precio * cantidad;
            double pctDescuento     = cantidad >= 10 ? 0.20 : 0.10;
            double importeDescuento = importeCompra * pctDescuento;
            double importePagar     = importeCompra - importeDescuento;
            int    lapiceros        = importePagar >= 200 ? 2 * cantidad : 0;

            txtResultado.setText(
                "Importe de la compra  : " + formato.format(importeCompra)    + "\n" +
                "Descuento (" + (int)(pctDescuento * 100) + "%)        : " + formato.format(importeDescuento) + "\n" +
                "Importe a pagar       : " + formato.format(importePagar)     + "\n" +
                "Lapiceros de obsequio : " + lapiceros + " unidades"
            );
        } catch (NumberFormatException ex) {
            mostrarError(ex.getMessage());
        }
    }

    private double leerDecimal(String texto, String campo) {
        String valor = texto.trim().replace(',', '.');
        if (valor.isEmpty()) throw new NumberFormatException("Ingrese el " + campo + ".");
        try { return Double.parseDouble(valor); }
        catch (NumberFormatException ex) {
            throw new NumberFormatException("Valor numérico inválido para " + campo + ".");
        }
    }

    private int leerEntero(String texto, String campo) {
        String valor = texto.trim();
        if (valor.isEmpty()) throw new NumberFormatException("Ingrese la " + campo + ".");
        try { return Integer.parseInt(valor); }
        catch (NumberFormatException ex) {
            throw new NumberFormatException("Número entero inválido para " + campo + ".");
        }
    }

    private void limpiar() {
        txtPrecioDocena.setText("");
        txtCantidadDocenas.setText("");
        txtResultado.setText("");
        txtPrecioDocena.requestFocus();
    }

    private void mostrarError(String mensaje) {
        JOptionPane.showMessageDialog(this, mensaje, "Dato inválido", JOptionPane.WARNING_MESSAGE);
    }
}
```

---

## Ejercicio 02 — Cálculo de Sueldo de Empleado

### 1. Enunciado del proyecto

El sueldo bruto de los empleados de una empresa se calcula sumando el sueldo básico más la bonificación por hijos.

El sueldo básico se calcula multiplicando las horas trabajadas por la tarifa horaria. La tarifa horaria depende de la categoría del empleado:

| Categoría | Tarifa horaria (S/.) |
|:---:|:---:|
| A | 45.0 |
| B | 37.5 |

La bonificación por hijos se calcula de acuerdo con la siguiente tabla:

| Número de hijos | Bonificación |
|:---:|:---:|
| Hasta 3 | S/. 40.5 por cada hijo |
| Más de 3 | S/. 35.0 por cada hijo |

Por ley, todo empleado está sujeto a un descuento sobre el sueldo bruto:

| Sueldo bruto (S/.) | Descuento |
|:---:|:---:|
| ≥ 3500 | 13.5% |
| < 3500 | 10.0% |

Dadas la categoría y la cantidad de horas trabajadas de un empleado, diseñe un programa que determine el sueldo básico, el sueldo bruto, el descuento y el sueldo neto.

---

### 2. Diagrama de clases

```
┌─────────────────────────────┐
│            App              │
├─────────────────────────────┤
│ + main(String[] args): void │
└─────────────┬───────────────┘
              │ crea y muestra
              ▼
┌──────────────────────────────────────────┐
│              FrmEmpleado                 │
├──────────────────────────────────────────┤
│ - txtHoras: JTextField                   │
│ - txtHijos: JTextField                   │
│ - cmbCategoria: JComboBox<String>        │
│ - txtResultado: JTextArea                │
│ - formato: DecimalFormat                 │
├──────────────────────────────────────────┤
│ + FrmEmpleado()                          │
│ - configurarVentana(): void              │
│ - agregarComponentes(): void             │
│ - calcular(): void                       │
│ - leerEntero(String, String): int        │
│ - limpiar(): void                        │
│ - mostrarError(String): void             │
└──────────────────────────────────────────┘
```

---

### 3. Diseño de la aplicación

La aplicación fue diseñada con una ventana JFrame titulada **"Cálculo de Sueldo de Empleado"**.

**Componentes principales:**
- Título principal: "Sueldo de Empleado"
- ComboBox para seleccionar la categoría del empleado (A o B)
- Campo de texto para ingresar las horas trabajadas
- Campo de texto para ingresar el número de hijos
- Botón **Calcular**: realiza todos los cálculos
- Botón **Limpiar**: borra los datos ingresados y los resultados
- Botón **Salir**: cierra la ventana
- Área de resultados: muestra categoría, tarifa, sueldo básico, bonificación, sueldo bruto, descuento y sueldo neto

**Proceso de cálculo:**
```
tarifa           = (categoría == A) ? 45.0 : 37.5
sueldoBasico     = horasTrabajadas × tarifa
bonificacion     = (hijos <= 3) ? hijos × 40.5 : hijos × 35.0
sueldoBruto      = sueldoBasico + bonificacion
pctDescuento     = (sueldoBruto >= 3500) ? 13.5% : 10.0%
descuento        = sueldoBruto × pctDescuento
sueldoNeto       = sueldoBruto − descuento
```

---

### 4. Código de la aplicación

#### Archivo: `App.java`

```java
package com.empresa.empleado;

import javax.swing.SwingUtilities;

public class App {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            FrmEmpleado ventana = new FrmEmpleado();
            ventana.setVisible(true);
        });
    }
}
```

#### Archivo: `FrmEmpleado.java`

```java
package com.empresa.empleado;

import java.awt.*;
import java.text.DecimalFormat;
import javax.swing.*;

public class FrmEmpleado extends JFrame {

    private final JTextField txtHoras;
    private final JTextField txtHijos;
    private final JComboBox<String> cmbCategoria;
    private final JTextArea  txtResultado;
    private final DecimalFormat formato;

    public FrmEmpleado() {
        formato      = new DecimalFormat("S/ #,##0.00");
        txtHoras     = new JTextField(12);
        txtHijos     = new JTextField(12);
        cmbCategoria = new JComboBox<>(new String[]{"A - S/. 45.00 por hora", "B - S/. 37.50 por hora"});
        txtResultado = new JTextArea(7, 30);
        configurarVentana();
        agregarComponentes();
    }

    private void configurarVentana() {
        setTitle("Cálculo de Sueldo de Empleado");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(520, 460);
        setLocationRelativeTo(null);
        setResizable(false);
        getContentPane().setBackground(new Color(245, 247, 250));
    }

    private void agregarComponentes() {
        JLabel titulo = new JLabel("Sueldo de Empleado", SwingConstants.CENTER);
        titulo.setFont(new Font("Arial", Font.BOLD, 22));
        titulo.setForeground(new Color(11, 61, 143));
        titulo.setBorder(BorderFactory.createEmptyBorder(15, 10, 10, 10));
        add(titulo, BorderLayout.NORTH);

        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBackground(new Color(245, 247, 250));
        panel.setBorder(BorderFactory.createEmptyBorder(10, 30, 10, 30));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(8, 8, 8, 8);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        JLabel lblCategoria = new JLabel("Categoría del empleado:");
        JLabel lblHoras     = new JLabel("Horas trabajadas:");
        JLabel lblHijos     = new JLabel("Número de hijos:");
        lblCategoria.setFont(new Font("Arial", Font.PLAIN, 14));
        lblHoras.setFont(new Font("Arial", Font.PLAIN, 14));
        lblHijos.setFont(new Font("Arial", Font.PLAIN, 14));
        cmbCategoria.setFont(new Font("Arial", Font.PLAIN, 14));
        txtHoras.setFont(new Font("Arial", Font.PLAIN, 14));
        txtHijos.setFont(new Font("Arial", Font.PLAIN, 14));

        JButton btnCalcular = new JButton("Calcular");
        JButton btnLimpiar  = new JButton("Limpiar");
        JButton btnSalir    = new JButton("Salir");
        btnCalcular.setFont(new Font("Arial", Font.BOLD, 13));
        btnLimpiar.setFont(new Font("Arial", Font.BOLD, 13));
        btnSalir.setFont(new Font("Arial", Font.BOLD, 13));

        btnCalcular.addActionListener(e -> calcular());
        btnLimpiar.addActionListener(e -> limpiar());
        btnSalir.addActionListener(e -> dispose());

        txtResultado.setEditable(false);
        txtResultado.setFont(new Font("Monospaced", Font.PLAIN, 13));
        txtResultado.setBackground(Color.WHITE);
        txtResultado.setBorder(BorderFactory.createEmptyBorder(8, 8, 8, 8));

        gbc.gridx = 0; gbc.gridy = 0;
        panel.add(lblCategoria, gbc);
        gbc.gridx = 1;
        panel.add(cmbCategoria, gbc);

        gbc.gridx = 0; gbc.gridy = 1;
        panel.add(lblHoras, gbc);
        gbc.gridx = 1;
        panel.add(txtHoras, gbc);

        gbc.gridx = 0; gbc.gridy = 2;
        panel.add(lblHijos, gbc);
        gbc.gridx = 1;
        panel.add(txtHijos, gbc);

        JPanel panelBotones = new JPanel();
        panelBotones.setBackground(new Color(245, 247, 250));
        panelBotones.add(btnCalcular);
        panelBotones.add(btnLimpiar);
        panelBotones.add(btnSalir);

        gbc.gridx = 0; gbc.gridy = 3; gbc.gridwidth = 2;
        panel.add(panelBotones, gbc);

        gbc.gridy = 4;
        gbc.fill = GridBagConstraints.BOTH;
        gbc.weightx = 1; gbc.weighty = 1;
        panel.add(new JScrollPane(txtResultado), gbc);

        add(panel, BorderLayout.CENTER);
    }

    private void calcular() {
        try {
            int horas = leerEntero(txtHoras.getText(), "horas trabajadas");
            int hijos = leerEntero(txtHijos.getText(), "número de hijos");

            if (horas <= 0) { mostrarError("Las horas deben ser mayor que cero.");       return; }
            if (hijos <  0) { mostrarError("El número de hijos no puede ser negativo."); return; }

            boolean esA      = cmbCategoria.getSelectedIndex() == 0;
            double tarifa    = esA ? 45.0 : 37.5;
            String categoria = esA ? "A" : "B";

            double sueldoBasico      = horas * tarifa;
            double bonificacionHijos = hijos <= 3 ? hijos * 40.5 : hijos * 35.0;
            double sueldoBruto       = sueldoBasico + bonificacionHijos;
            double pctDescuento      = sueldoBruto >= 3500 ? 0.135 : 0.10;
            double descuento         = sueldoBruto * pctDescuento;
            double sueldoNeto        = sueldoBruto - descuento;

            txtResultado.setText(
                "Categoría              : " + categoria                         + "\n" +
                "Tarifa horaria         : " + formato.format(tarifa)            + " / hora\n" +
                "Sueldo básico          : " + formato.format(sueldoBasico)      + "\n" +
                "Bonificación por hijos : " + formato.format(bonificacionHijos) + "\n" +
                "Sueldo bruto           : " + formato.format(sueldoBruto)       + "\n" +
                "Descuento (" + (int)(pctDescuento * 100) + "%)        : " + formato.format(descuento) + "\n" +
                "Sueldo neto            : " + formato.format(sueldoNeto)
            );
        } catch (NumberFormatException ex) {
            mostrarError(ex.getMessage());
        }
    }

    private int leerEntero(String texto, String campo) {
        String valor = texto.trim();
        if (valor.isEmpty()) throw new NumberFormatException("Ingrese el " + campo + ".");
        try { return Integer.parseInt(valor); }
        catch (NumberFormatException ex) {
            throw new NumberFormatException("Número entero inválido para " + campo + ".");
        }
    }

    private void limpiar() {
        cmbCategoria.setSelectedIndex(0);
        txtHoras.setText("");
        txtHijos.setText("");
        txtResultado.setText("");
        txtHoras.requestFocus();
    }

    private void mostrarError(String mensaje) {
        JOptionPane.showMessageDialog(this, mensaje, "Dato inválido", JOptionPane.WARNING_MESSAGE);
    }
}
```

---

*Portafolio de Ejercicios — Actividad N° 02 | Métodos | Apache Maven*
