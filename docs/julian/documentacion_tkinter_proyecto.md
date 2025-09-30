
# Documentación del Proyecto (Interfaz Tkinter con Ventanas)

Este proyecto implementa una **aplicación de escritorio en Python** utilizando la librería estándar **Tkinter**.  
Se compone de varias ventanas (cada una definida en un archivo independiente) que ilustran distintos controles gráficos (labels, entry, listbox, treeview, canvas, etc.).

---

## 1. Estructura de archivos
```
/{repo_root}
├── win_home.py      # Ventana de bienvenida
├── win_form.py      # Ventana de formulario con validación y guardado
├── win_list.py      # Ventana con Listbox (CRUD básico)
├── win_table.py     # Ventana con Treeview cargando CSV
├── win_canvas.py    # Ventana de dibujo en Canvas
└── data/sample.csv  # Archivo CSV de ejemplo para la tabla
```

---

## 2. Descripción de cada módulo

### **win_home.py**
- **Función principal:** `open_win_home(parent: tk.Tk)`
- **Propósito:** Mostrar una ventana de bienvenida con un mensaje y botones de acción.
- **Elementos:**
  - `Label`: mensaje de bienvenida.
  - `Button`: 
    - Mostrar un `messagebox` con "¡Equipo listo!".  
    - Cerrar la ventana.

---

### **win_form.py**
- **Función principal:** `open_win_form(parent: tk.Tk)`
- **Propósito:** Formulario simple para capturar nombre y edad, con validación y opción de guardar en archivo `.txt`.
- **Lógica clave:**
  - Validar que el nombre no esté vacío.
  - Validar que la edad sea un número entero.
  - Guardar en archivo elegido mediante `filedialog.asksaveasfilename`.
  - Mostrar mensajes de error o confirmación con `messagebox`.

---

### **win_list.py**
- **Función principal:** `open_win_list(parent: tk.Tk)`
- **Propósito:** CRUD básico usando un `Listbox`.
- **Funciones internas:**
  - `agregar()`: Inserta texto del `Entry` en la lista.
  - `eliminar()`: Borra el ítem seleccionado.
  - `limpiar()`: Elimina todos los elementos de la lista.
- **Elementos UI:**
  - `Listbox` para mostrar los ítems.
  - Botones: Agregar, Eliminar seleccionado, Limpiar, Cerrar.

---

### **win_table.py**
- **Función principal:** `open_win_table(parent: tk.Tk)`
- **Propósito:** Mostrar una tabla (`ttk.Treeview`) con datos cargados desde un archivo CSV.
- **Elementos:**
  - Columnas: `nombre`, `valor1`, `valor2`.
  - Lectura de `/data/sample.csv` mediante `csv.DictReader`.
- **Control de errores:**
  - Si el archivo no existe, muestra un `messagebox.showwarning` pidiendo crearlo.

Ejemplo de CSV incluido (`data/sample.csv`):
```csv
nombre,valor1,valor2
A,10,20
B,15,25
C,12,30
```

---

### **win_canvas.py**
- **Función principal:** `open_win_canvas(parent: tk.Tk)`
- **Propósito:** Demostrar uso del widget `Canvas` dibujando formas básicas.
- **Elementos:**
  - `create_rectangle`, `create_oval`, `create_line`, `create_text`.
  - Botón para cerrar la ventana.

---

## 3. Dependencias
- Python 3.x (se recomienda 3.8+)
- Librerías estándar usadas: `tkinter`, `ttk`, `csv`, `pathlib`
- No requiere instalación adicional vía `pip`.

---

## 4. Ejecución
Cada archivo define una ventana independiente que debe abrirse desde una ventana raíz `Tk()`.  
Ejemplo de uso:
```python
import tkinter as tk
from win_home import open_win_home
from win_form import open_win_form

root = tk.Tk()
root.title("App Principal")
root.geometry("300x200")

# Botones para abrir ventanas secundarias
import tkinter.ttk as ttk
ttk.Button(root, text="Home", command=lambda: open_win_home(root)).pack(pady=6)
ttk.Button(root, text="Formulario", command=lambda: open_win_form(root)).pack(pady=6)

root.mainloop()
```

---

## 5. Posibles mejoras
- Agregar una ventana principal (`main.py`) que centralice la navegación a las demás.
- Internacionalización (traducción de mensajes).
- Persistencia de datos más robusta (SQLite en vez de `.txt`/`.csv`).
- Uso de `Pydantic` o validadores externos para datos.

---

**Fin de la documentación**
