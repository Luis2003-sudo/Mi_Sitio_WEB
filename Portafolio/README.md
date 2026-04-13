# 📁 Portafolio de Ejercicios
### Actividad N° 01 — Apache Maven

| | |
|---|---|
| **Tecnología** | Apache Maven + Java Swing |
| **Ejercicios** | 2 aplicaciones de escritorio |
| **Contenido** | Enunciado · Diagrama de clases · Diseño · Código |

---

## Índice

- [Enunciado 01 — Venta de Camisas con Descuento 7% + 7%](#enunciado-01--venta-de-camisas-con-descuento-7--7)
- [Enunciado 02 — Distribución de Inversión en Feria](#enunciado-02--distribución-de-inversión-en-feria)

---

## Enunciado 01 — Venta de Camisas con Descuento 7% + 7%

### 1. Enunciado del proyecto

Una tienda ha puesto en oferta la venta de camisas ofreciendo un descuento por temporada de verano denominado **7% + 7%**. Los cálculos se efectúan de la siguiente manera:

- El importe de la compra es igual al producto del precio de la camisa por la cantidad de unidades adquiridas.
- El importe del primer descuento es igual al 7% del importe de la compra.
- El importe del segundo descuento es igual al 7% de lo que queda de restar el importe de la compra menos el primer descuento.
- El importe del descuento total es igual a la suma de los dos descuentos anteriores.
- El importe por pagar es igual al importe de la compra menos el descuento total.

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
┌─────────────────────────────────────────┐
│              FrmCamisas                 │
├─────────────────────────────────────────┤
│ - txtPrecio: JTextField                 │
│ - txtCantidad: JTextField               │
│ - txtResultado: JTextArea               │
│ - formato: DecimalFormat                │
├─────────────────────────────────────────┤
│ + FrmCamisas()                          │
│ - configurarVentana(): void             │
│ - agregarComponentes(): void            │
│ - calcular(): void                      │
│ - leerDecimal(String, String): double   │
│ - leerEntero(String, String): int       │
│ - limpiar(): void                       │
│ - mostrarError(String): void            │
└─────────────────────────────────────────┘
```

---

### 3. Diseño de la aplicación

La aplicación fue diseñada con una ventana JFrame titulada **"Tienda de Camisas - Descuento 7% + 7%"**.

**Componentes principales:**
- Título principal: "Venta de Camisas"
- Caja de texto para ingresar el precio de la camisa
- Caja de texto para ingresar la cantidad de unidades adquiridas
- Botón **Calcular**: realiza todos los cálculos solicitados
- Botón **Limpiar**: borra los datos ingresados y los resultados
- Botón **Salir**: cierra la ventana
- Área de resultados: muestra importe de compra, primer descuento, segundo descuento, descuento total e importe por pagar

**Proceso de cálculo:**
```
importeCompra    = precio × cantidad
primerDescuento  = importeCompra × 0.07
segundoDescuento = (importeCompra − primerDescuento) × 0.07
descuentoTotal   = primerDescuento + segundoDescuento
importePagar     = importeCompra − descuentoTotal
```

---

### 4. Código de la aplicación

#### Archivo: `App.java`

```java
package com.tienda.camisas;

import javax.swing.SwingUtilities;

public class App {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            FrmCamisas ventana = new FrmCamisas();
            ventana.setVisible(true);
        });
    }
}
```

#### Archivo: `FrmCamisas.java`

```java
package com.tienda.camisas;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.text.DecimalFormat;
import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.SwingConstants;

public class FrmCamisas extends JFrame {
    private final JTextField txtPrecio;
    private final JTextField txtCantidad;
    private final JTextArea  txtResultado;
    private final DecimalFormat formato;

    public FrmCamisas() {
        formato      = new DecimalFormat("S/ #,##0.00");
        txtPrecio    = new JTextField(12);
        txtCantidad  = new JTextField(12);
        txtResultado = new JTextArea(8, 28);
        configurarVentana();
        agregarComponentes();
    }

    private void configurarVentana() {
        setTitle("Tienda de Camisas - Descuento 7% + 7%");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(560, 430);
        setMinimumSize(new Dimension(520, 400));
        setLocationRelativeTo(null);
        getContentPane().setBackground(new Color(245, 247, 250));
    }

    private void calcular() {
        try {
            double precio   = leerDecimal(txtPrecio.getText(), "precio de la camisa");
            int    cantidad = leerEntero(txtCantidad.getText(), "cantidad de unidades");

            if (precio   <= 0) { mostrarError("El precio debe ser mayor que cero.");   txtPrecio.requestFocus();   return; }
            if (cantidad <= 0) { mostrarError("La cantidad debe ser mayor que cero."); txtCantidad.requestFocus(); return; }

            double importeCompra    = precio * cantidad;
            double primerDescuento  = importeCompra * 0.07;
            double segundoDescuento = (importeCompra - primerDescuento) * 0.07;
            double descuentoTotal   = primerDescuento + segundoDescuento;
            double importePagar     = importeCompra - descuentoTotal;

            txtResultado.setText(
                "Importe de la compra : " + formato.format(importeCompra)   + "\n"
              + "Primer descuento 7%  : " + formato.format(primerDescuento)  + "\n"
              + "Segundo descuento 7% : " + formato.format(segundoDescuento) + "\n"
              + "Descuento total      : " + formato.format(descuentoTotal)   + "\n"
              + "Importe por pagar    : " + formato.format(importePagar)
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
            throw new NumberFormatException("Ingrese un valor numérico válido para " + campo + ".");
        }
    }

    private int leerEntero(String texto, String campo) {
        String valor = texto.trim();
        if (valor.isEmpty()) throw new NumberFormatException("Ingrese la " + campo + ".");
        try { return Integer.parseInt(valor); }
        catch (NumberFormatException ex) {
            throw new NumberFormatException("Ingrese un número entero válido para " + campo + ".");
        }
    }

    private void limpiar() {
        txtPrecio.setText("");
        txtCantidad.setText("");
        txtResultado.setText("");
        txtPrecio.requestFocus();
    }

    private void mostrarError(String mensaje) {
        JOptionPane.showMessageDialog(this, mensaje, "Dato inválido", JOptionPane.WARNING_MESSAGE);
    }
}
```

---

## Enunciado 02 — Distribución de Inversión en Feria

### 1. Enunciado del proyecto

Una empresa expondrá sus productos en una feria. La empresa considera que el monto total de dinero a invertir estará distribuido de la siguiente manera:

| Rubro | Porcentaje |
|---|:---:|
| Alquiler de espacio en la feria | 23% |
| Publicidad | 7% |
| Transporte | 26% |
| Servicios feriales | 12% |
| Decoración | 21% |
| Gastos varios | 11% |

Dado el monto total de dinero a invertir, diseñe un programa que determine cuánto gastará la empresa en cada rubro.

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
┌─────────────────────────────────────────────┐
│                  FrmFeria                   │
├─────────────────────────────────────────────┤
│ - txtMontoTotal: JTextField                 │
│ - modeloTabla: DefaultTableModel            │
│ - formato: DecimalFormat                    │
├─────────────────────────────────────────────┤
│ + FrmFeria()                                │
│ - configurarVentana(): void                 │
│ - agregarComponentes(): void                │
│ - cargarTablaInicial(): void                │
│ - calcular(): void                          │
│ - leerMonto(String): double                 │
│ - agregarFila(String, String, String): void │
│ - limpiar(): void                           │
│ - mostrarError(String): void                │
└─────────────────────────────────────────────┘
```

---

### 3. Diseño de la aplicación

La aplicación fue diseñada con una ventana JFrame titulada **"Distribución de Inversión para Feria"**.

**Componentes principales:**
- Título principal: "Enunciado 02 - Inversión en Feria"
- Caja de texto para ingresar el monto total a invertir
- Botón **Calcular**: calcula el monto correspondiente a cada rubro
- Botón **Limpiar**: borra el monto ingresado y limpia los resultados
- Botón **Salir**: cierra la ventana
- Tabla de resultados con tres columnas: Rubro, Porcentaje y Monto

**Proceso de cálculo:**
```
Alquiler de espacio en la feria = montoTotal × 0.23
Publicidad                      = montoTotal × 0.07
Transporte                      = montoTotal × 0.26
Servicios feriales              = montoTotal × 0.12
Decoración                      = montoTotal × 0.21
Gastos varios                   = montoTotal × 0.11
```

---

### 4. Código de la aplicación

#### Archivo: `App.java`

```java
package com.empresa.feria;

import javax.swing.SwingUtilities;

public class App {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            FrmFeria ventana = new FrmFeria();
            ventana.setVisible(true);
        });
    }
}
```

#### Archivo: `FrmFeria.java`

```java
package com.empresa.feria;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.text.DecimalFormat;
import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.SwingConstants;
import javax.swing.table.DefaultTableModel;

public class FrmFeria extends JFrame {
    private final JTextField       txtMontoTotal;
    private final DefaultTableModel modeloTabla;
    private final DecimalFormat    formato;

    public FrmFeria() {
        txtMontoTotal = new JTextField(14);
        formato = new DecimalFormat("S/ #,##0.00");
        modeloTabla = new DefaultTableModel(new Object[]{"Rubro", "Porcentaje", "Monto"}, 0) {
            @Override
            public boolean isCellEditable(int row, int column) { return false; }
        };
        configurarVentana();
        agregarComponentes();
        cargarTablaInicial();
    }

    private void configurarVentana() {
        setTitle("Distribución de Inversión para Feria");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(650, 450);
        setMinimumSize(new Dimension(600, 420));
        setLocationRelativeTo(null);
        getContentPane().setBackground(new Color(245, 248, 252));
    }

    private void cargarTablaInicial() {
        modeloTabla.setRowCount(0);
        agregarFila("Alquiler de espacio en la feria", "23%", "");
        agregarFila("Publicidad",          "7%",  "");
        agregarFila("Transporte",           "26%", "");
        agregarFila("Servicios feriales",  "12%", "");
        agregarFila("Decoración",           "21%", "");
        agregarFila("Gastos varios",        "11%", "");
    }

    private void calcular() {
        try {
            double montoTotal = leerMonto(txtMontoTotal.getText());
            if (montoTotal <= 0) {
                mostrarError("El monto total debe ser mayor que cero.");
                txtMontoTotal.requestFocus();
                return;
            }
            modeloTabla.setRowCount(0);
            agregarFila("Alquiler de espacio en la feria", "23%", formato.format(montoTotal * 0.23));
            agregarFila("Publicidad",          "7%",  formato.format(montoTotal * 0.07));
            agregarFila("Transporte",           "26%", formato.format(montoTotal * 0.26));
            agregarFila("Servicios feriales",  "12%", formato.format(montoTotal * 0.12));
            agregarFila("Decoración",           "21%", formato.format(montoTotal * 0.21));
            agregarFila("Gastos varios",        "11%", formato.format(montoTotal * 0.11));
        } catch (NumberFormatException ex) {
            mostrarError(ex.getMessage());
            txtMontoTotal.requestFocus();
        }
    }

    private double leerMonto(String texto) {
        String valor = texto.trim().replace(',', '.');
        if (valor.isEmpty()) throw new NumberFormatException("Ingrese el monto total a invertir.");
        try { return Double.parseDouble(valor); }
        catch (NumberFormatException ex) {
            throw new NumberFormatException("Ingrese un monto numérico válido.");
        }
    }

    private void agregarFila(String rubro, String porcentaje, String monto) {
        modeloTabla.addRow(new Object[]{rubro, porcentaje, monto});
    }

    private void limpiar() {
        txtMontoTotal.setText("");
        cargarTablaInicial();
        txtMontoTotal.requestFocus();
    }

    private void mostrarError(String mensaje) {
        JOptionPane.showMessageDialog(this, mensaje, "Dato inválido", JOptionPane.WARNING_MESSAGE);
    }
}
```

---

*Portafolio de Ejercicios — Actividad N° 01 | Apache Maven*
