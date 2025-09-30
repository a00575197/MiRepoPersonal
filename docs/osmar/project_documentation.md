
# Documentación del proyecto: Aplicación de ventanas Tkinter

**Descripción breve**  
Este proyecto es una pequeña aplicación de escritorio creada con `tkinter` y `ttk` que contiene varias ventanas (Toplevel) con funcionalidades básicas: una pantalla de bienvenida, un formulario con guardado a archivo, una lista con operaciones CRUD básicas, una tabla que lee un CSV y un ejemplo de dibujo con Canvas.

---

## Estructura de archivos (sugerida)
```
/repo-root
│
├─ data/
│  └─ sample.csv
│
├─ src/
│  ├─ win_home.py
│  ├─ win_form.py
│  ├─ win_list.py
│  ├─ win_table.py
│  └─ win_canvas.py
│
└─ main.py  # archivo lanzador (ejemplo más abajo)
```

---

## Requisitos
- Python 3.8+ (probado con 3.10+)
- Librería estándar: `tkinter`, `csv`, `pathlib`. (tkinter normalmente viene con Python; en algunas distribuciones es un paquete adicional).

---

## Cómo ejecutar (ejemplo)
Crea un archivo `main.py` en la raíz del proyecto con el siguiente contenido para lanzar la ventana principal y acceder a las subventanas:

```python
import tkinter as tk
from tkinter import ttk
from src import win_home, win_form, win_list, win_table, win_canvas

def main():
    root = tk.Tk()
    root.title("App Principal")
    root.geometry("320x220")
    frm = ttk.Frame(root, padding=12)
    frm.pack(fill="both", expand=True)

    ttk.Label(frm, text="Panel principal", font=("Segoe UI", 12, "bold")).pack(pady=(0,8))

    ttk.Button(frm, text="Home", command=lambda: win_home.open_win_home(root)).pack(fill="x", pady=4)
    ttk.Button(frm, text="Formulario", command=lambda: win_form.open_win_form(root)).pack(fill="x", pady=4)
    ttk.Button(frm, text="Lista", command=lambda: win_list.open_win_list(root)).pack(fill="x", pady=4)
    ttk.Button(frm, text="Tabla (CSV)", command=lambda: win_table.open_win_table(root)).pack(fill="x", pady=4)
    ttk.Button(frm, text="Canvas", command=lambda: win_canvas.open_win_canvas(root)).pack(fill="x", pady=4)
    ttk.Button(frm, text="Salir", command=root.quit).pack(fill="x", pady=(8,0))

    root.mainloop()

if __name__ == '__main__':
    main()
```

---

## Descripción de los módulos

### `win_home.py`
- Función exportada: `open_win_home(parent: tk.Tk)`
- Crea una ventana `Toplevel` con título "Home / Bienvenida".
- Contenido: etiquetas de bienvenida, botón que muestra un `messagebox.showinfo("Info", "¡Equipo listo!")`, y botón para cerrar la ventana.
- Observaciones: UI básica y ejemplo claro del uso de `ttk.Frame`, `ttk.Label` y `ttk.Button` con `messagebox`.

### `win_form.py`
- Función exportada: `open_win_form(parent: tk.Tk)`
- Crea un formulario con campos `Nombre` y `Edad`.
- Validaciones:
  - `Nombre` es obligatorio (no vacío).
  - `Edad` debe ser un número entero (verifica `isdigit()`).
- Guardado:
  - Usa `filedialog.asksaveasfilename` para elegir ruta y guarda un archivo `.txt` con el contenido `Nombre: ...\nEdad: ...\n` codificado en UTF-8.
  - Muestra mensajes de error o confirmación usando `messagebox`.
- Observaciones y mejoras propuestas:
  - `isdigit()` no acepta números negativos ni valida rangos; usar manejo con `int()` y `try/except` para mayor robustez.
  - Agregar validación de rango de edad (ej. 0–130) según necesidad.
  - Manejar excepción de IO al escribir el archivo (try/except alrededor del `open`).

### `win_list.py`
- Función exportada: `open_win_list(parent: tk.Tk)`
- Controles:
  - `Listbox` para mostrar elementos.
  - `Entry` para ingresar texto.
  - Botones: `Agregar`, `Eliminar seleccionado`, `Limpiar`, `Cerrar`.
- Comportamiento:
  - `Agregar` inserta el texto al final si no está vacío; muestra advertencia si vacío.
  - `Eliminar` toma la selección actual (`lb.curselection()`) y elimina el ítem seleccionado (si hay selección).
  - `Limpiar` elimina todos los elementos.
- Observaciones:
  - No hay control de duplicados; se puede añadir lógica para impedir duplicados si se desea.
  - `Eliminar` no muestra mensaje si no hay selección; sería útil añadir feedback al usuario.

### `win_table.py`
- Función exportada: `open_win_table(parent: tk.Tk)`
- Presenta un `ttk.Treeview` con columnas `nombre`, `valor1`, `valor2`.
- Lee el archivo CSV: `data/sample.csv` desde la raíz del repo calculada con:
  ```py
  ruta = Path(__file__).resolve().parents[2] / "data" / "sample.csv"
  ```
  Esto asume la estructura `/repo-root/src/<módulos>` y que `data` está en la raíz del repo. Ajustar `parents[2]` según la ubicación real.
- Si no existe el archivo, muestra un `messagebox.warning` y aborta.
- Lee el CSV con `csv.DictReader` y agrega filas al Treeview.
- Observaciones y mejoras:
  - La forma de calcular la ruta es frágil si la estructura cambia; recomendamos usar rutas relativas desde la raíz (o configurar una variable `DATA_DIR` central).
  - Manejar excepciones al leer CSV (archivos con encoding distinto, columnas faltantes, filas mal formadas).
  - Añadir posibilidad de recargar o seleccionar otro CSV con `filedialog.askopenfilename` para hacerlo más genérico.
  - Añadir ordenamiento de columnas y resize dinámico de columnas (`treeview.heading(..., command=lambda c=c: sort_by(tv, c, False))`).

### `win_canvas.py`
- Función exportada: `open_win_canvas(parent: tk.Tk)`
- Crea un `Canvas` y dibuja formas básicas (rectángulo, óvalo, línea, texto).
- Útil como ejemplo para aprender dibujo en `tkinter` y eventos (se pueden añadir handlers de mouse o botones para dibujo dinámico).

---

## Sugerencias de mejoras generales
1. **Centralizar configuración**: Crear un módulo `config.py` con rutas, constantes, tipografías y tamaños. Evita hardcoding de rutas y tamaños en cada módulo. Por ejemplo:
   ```py
   from pathlib import Path
   BASE_DIR = Path(__file__).resolve().parents[1]
   DATA_DIR = BASE_DIR / "data"
   ```
2. **Manejo de errores**: Añadir bloques `try/except` donde se realicen operaciones de I/O y conversiones (ej. `int()`), y mostrar errores amigables al usuario.
3. **Internacionalización y textos**: Si la app crece, separar los textos en un archivo de traducciones o constantes para facilitar cambios de idioma.
4. **Pruebas unitarias**: Separar la lógica de validación a funciones puras que puedan probarse sin GUI. Ejemplo: `def validar_edad(texto): -> (bool, mensaje)`.
5. **Packaging**: Añadir `requirements.txt` (aunque stdlib) y un `setup.py` o `pyproject.toml` si quieres distribuir la app.
6. **Mejorar la UX**: Confirmaciones al eliminar, atajos de teclado, enfoque inicial en `Entry` con `ent.focus_set()` y manejo de accesibilidad (tab order).
7. **Logging**: Añadir logging a eventos importantes (errores en IO, excepciones) para debug.

---

## Notas específicas detectadas en el código existente
- `win_table.py` usa `Path(__file__).resolve().parents[2]` para llegar a `/repo-root/data/sample.csv`. Esto funciona si el árbol de carpetas es exactamente `repo-root/<algo>/<archivo>`. Verificar y documentar la estructura o preferir una ruta configurable.
- Uso de `isdigit()` en `win_form.py` es limitado para la validación de enteros. `'-1'.isdigit()` devuelve `False`, lo que puede o no ser deseado.
- No se cierran explícitamente los archivos (aunque `with open(...)` sí lo hace); buen uso de `encoding="utf-8"` al escribir.
- En `win_list.py`, al eliminar se usa `lb.delete(sel[0])` sin manejo de índices fuera de rango (actualmente está protegido por `if sel:`). OK.

---

## Ideas de extensiones (features)
- Guardar/recuperar la lista (win_list) a un archivo JSON o CSV.
- Edición en la tabla (`Treeview`) con doble-clic para editar celdas.
- Exportar la tabla a Excel/CSV desde UI.
- Añadir un sistema de pestañas en la ventana principal en lugar de ventanas `Toplevel` (usar `ttk.Notebook`).

---

## Checklist de estilo y calidad
- [ ] Añadir docstrings a cada módulo y función.
- [ ] Añadir typing (ya se usa `parent: tk.Tk` en firmas; extender tipos de retorno).
- [ ] Añadir pruebas unitarias para validaciones (por ejemplo con `pytest`).
- [ ] Añadir CI básico (GitHub Actions) para linting (`flake8`/`ruff`) y pruebas.

---

## Licencia y atribución
Si este es un proyecto personal o educativo, añadir un `LICENSE` (por ejemplo MIT) y un `README.md` con instrucciones rápidas y créditos.

---

### Contacto / Autor
Documentación generada automáticamente por un asistente - revisar y adaptar según las necesidades del proyecto.
