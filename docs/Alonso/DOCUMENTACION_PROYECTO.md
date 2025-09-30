# 📘 Documentación del Proyecto - Aplicación Demo (tkinter)

## 📌 Descripción General
Este proyecto es una aplicación gráfica desarrollada en **Python** utilizando la librería **tkinter**.  
Se trata de un **MVP (Producto Mínimo Viable)** que muestra diferentes ventanas de ejemplo: una pantalla de bienvenida, un formulario, una lista editable, una tabla de datos y un canvas de dibujo.  

El programa está organizado de manera modular, cada ventana se encuentra en un archivo separado dentro de la carpeta `app/`.

---

## 🗂️ Estructura del Proyecto
```
proyecto/
│── main.py                # Ventana principal
│── app/
│   ├── win_home.py         # Ventana de bienvenida
│   ├── win_form.py         # Ventana de formulario
│   ├── win_list.py         # Ventana con CRUD en lista
│   ├── win_table.py        # Ventana con tabla Treeview
│   ├── win_canvas.py       # Ventana con canvas y dibujos
│── data/
    └── sample.csv          # Archivo CSV con datos de ejemplo
```

---

## ⚙️ Archivos del Proyecto

### 1. **main.py**
- Es el **punto de entrada** de la aplicación.
- Crea la ventana principal con un menú de botones para abrir cada sección:
  - **Home**
  - **Formulario**
  - **Lista**
  - **Tabla**
  - **Canvas**
- Tiene un botón para **cerrar la aplicación**.

---

### 2. **win_home.py**
- Ventana simple de **bienvenida**.
- Contiene:
  - Etiqueta con mensaje de saludo.
  - Botón para mostrar un `messagebox` con un mensaje de información.
  - Botón para cerrar la ventana.

---

### 3. **win_form.py**
- Ventana de **formulario con validaciones**.
- Incluye campos:
  - **Nombre** (obligatorio).
  - **Edad** (debe ser número entero).
- Botón **Guardar**:
  - Valida los campos.
  - Permite guardar la información en un archivo `.txt`.
  - Muestra confirmación con `messagebox`.
- Botón **Cerrar** para salir de la ventana.

---

### 4. **win_list.py**
- Ventana con **CRUD básico** usando un `Listbox`.
- Funcionalidades:
  - **Agregar** un ítem.
  - **Eliminar** el ítem seleccionado.
  - **Limpiar** toda la lista.
- Usa `messagebox` para advertencias si se intenta agregar un texto vacío.

---

### 5. **win_table.py**
- Ventana con un `Treeview` para mostrar una **tabla de datos**.
- Carga datos desde un archivo CSV: `data/sample.csv`.
- Columnas: `nombre`, `valor1`, `valor2`.
- Muestra advertencia si el archivo CSV no existe.
- Botón **Cerrar** para salir.

Ejemplo de CSV (`sample.csv`):
```csv
nombre,valor1,valor2
A,10,20
B,15,25
C,12,30
```

---

### 6. **win_canvas.py**
- Ventana con un **canvas de dibujo**.
- Dibuja ejemplos:
  - Un rectángulo.
  - Un círculo.
  - Una línea.
  - Texto.
- Botón **Cerrar** para salir de la ventana.

---

## 📦 Dependencias
Este proyecto solo requiere librerías estándar de Python:
- `tkinter`
- `csv`
- `pathlib`

No se necesita instalar paquetes externos.

---

## ▶️ Ejecución
1. Asegúrate de tener Python 3 instalado.
2. Estructura las carpetas como se muestra en la sección de estructura.
3. Ejecuta:
   ```bash
   python main.py
   ```
4. Navega entre las ventanas usando los botones.

---

## ✅ Conclusión
Este proyecto es un **ejemplo educativo** que integra distintos componentes de `tkinter`:
- Ventanas modales.
- Formularios con validación.
- CRUD básico en listas.
- Lectura de datos desde CSV en un `Treeview`.
- Dibujos en `Canvas`.

Sirve como base para aplicaciones más grandes con interfaz gráfica en Python.
