# 📘 Documentación del Proyecto: Aplicación Demo con Tkinter

## 1. Descripción General
Este proyecto es una **aplicación de escritorio en Python** construida con la librería **Tkinter**.  
Funciona como una aplicación de demostración (MVP) para mostrar diferentes ventanas y funcionalidades gráficas:

- **Home**: ventana de bienvenida.  
- **Formulario**: captura y guarda datos en un archivo.  
- **Lista**: gestión básica de ítems (CRUD simple en memoria).  
- **Tabla**: visualización de datos desde un archivo CSV usando `Treeview`.  
- **Canvas**: espacio de dibujo con formas predefinidas.  

---

## 2. Estructura del Proyecto
```
/src/app/
│   main.py          # Punto de entrada principal
│   win_home.py      # Ventana de bienvenida
│   win_form.py      # Formulario con validación y guardado
│   win_list.py      # Lista CRUD en memoria
│   win_table.py     # Tabla cargada desde CSV
│   win_canvas.py    # Canvas para dibujo
/data/
│   sample.csv       # Archivo de datos de ejemplo
```

---

## 3. Dependencias
- **Python 3.8+**
- Librerías estándar:
  - `tkinter` y `tkinter.ttk` → GUI
  - `messagebox`, `filedialog` → diálogos
  - `csv` y `pathlib` → lectura de CSV
- No requiere librerías externas.

---

## 4. Descripción de los Módulos

### 4.1 `main.py`
- **Función `main()`**:  
  - Crea la ventana principal con `Tk()`.  
  - Define un `Frame` y un menú de botones para abrir las diferentes ventanas (`open_win_home`, `open_win_form`, etc.).  
  - Incluye un botón **Salir** para cerrar la app.  

Ejemplo de botones:
```python
ttk.Button(frame, text="1) Home / Bienvenida", command=lambda: open_win_home(root)).pack()
```

---

### 4.2 `win_home.py`
- Ventana secundaria (`Toplevel`) con:
  - Mensaje de bienvenida.  
  - Botón que muestra un **messagebox informativo**.  
  - Botón para cerrar la ventana.  

---

### 4.3 `win_form.py`
- Ventana para capturar:
  - **Nombre** (texto).  
  - **Edad** (número entero).  
- Botón **Guardar**:
  - Valida que el nombre no esté vacío.  
  - Valida que la edad sea un número entero.  
  - Guarda los datos en un archivo `.txt` elegido por el usuario.  
- Botón **Cerrar** para salir de la ventana.

---

### 4.4 `win_list.py`
- Ventana con un **Listbox** y botones CRUD:
  - **Agregar**: añade un ítem desde un campo `Entry`.  
  - **Eliminar seleccionado**: borra el ítem marcado.  
  - **Limpiar**: elimina todos los ítems.  
  - **Cerrar**: cierra la ventana.  

---

### 4.5 `win_table.py`
- Ventana con un **Treeview** (tabla).  
- Lee datos desde `/data/sample.csv`.  
- Muestra las columnas: `nombre`, `valor1`, `valor2`.  
- Si el archivo no existe, muestra un mensaje de advertencia.  
- Botón **Cerrar** para salir de la ventana.

---

### 4.6 `win_canvas.py`
- Ventana con un **Canvas**.  
- Dibuja ejemplos de:
  - Rectángulo.  
  - Óvalo relleno.  
  - Línea.  
  - Texto.  
- Botón **Cerrar** para salir de la ventana.  

---

## 5. Flujo de la Aplicación
1. Se ejecuta `main.py`.  
2. Se muestra la **ventana principal** con un menú de botones.  
3. El usuario puede abrir cualquiera de las ventanas modulares.  
4. Cada ventana se abre en una nueva ventana secundaria (`Toplevel`).  
5. El usuario interactúa y cierra las ventanas según necesidad.  
6. La aplicación termina al pulsar el botón **Salir**.  

---

## 6. Posibles Extensiones
- **Persistencia** de datos en lista y formulario usando SQLite.  
- **Edición** y **borrado** en la tabla (CRUD completo).  
- **Herramientas de dibujo** más avanzadas en el Canvas.  
- **Estilos personalizados** con `ttk.Style` para mejorar la interfaz.  
