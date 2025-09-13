<p align="center">
  <img src="https://i.pinimg.com/originals/37/1a/c8/371ac843551c2f299675c76d510eab62.gif" alt="Bienvenida" width="800"/>
</p>

---

# 📝 Gestor de Tareas en Python

El **Gestor de Tareas en Python** es una aplicación de consola diseñada para organizar y administrar pendientes de manera sencilla y eficiente.  
Fue desarrollada como práctica de programación en **Python**, con un enfoque en la manipulación de datos mediante **JSON** y el uso del sistema de archivos para garantizar la persistencia de la información.  

---

## 📌 ¿Cómo funciona?

El programa permite al usuario interactuar con un menú en consola desde el cual puede:

- 📋 **Visualizar tareas**: mostrar en pantalla todas las tareas registradas junto con su estado (pendiente o completada).  
- ➕ **Agregar nuevas tareas**: ingresar un título que se almacenará automáticamente en un archivo JSON.  
- ✅ **Marcar tareas como completadas**: actualizar el estado de cualquier tarea seleccionada.  
- 🗑️ **Eliminar tareas**: borrar aquellas que ya no sean necesarias.  
- 💾 **Guardar datos de manera persistente**: toda la información se almacena en `tareas.json`, lo que asegura que tus registros no se pierdan al cerrar el programa.  

---

## 🎯 Objetivo

El objetivo principal de este proyecto es servir como **ejemplo práctico** de:

- Programación estructurada en **Python**.  
- Manejo de **archivos JSON** como base de datos ligera.  
- Uso de **Visual Studio Code** como entorno de desarrollo.  
- Práctica de interacción con el **usuario mediante consola**.  

---

## 🚀 Ideal para

- Estudiantes que desean practicar programación básica en Python.  
- Personas que quieran aprender cómo gestionar datos con JSON.  
- Cualquiera que necesite un gestor de tareas rápido y ligero para la terminal.  
 

---
## ⚙️ Herramientas utilizadas

| Visual Studio Code | Python | JSON |
|--------------------|--------|------|
| <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/vscode/vscode-original.svg" alt="Visual Studio Code" width="60" height="60"/> | <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="Python" width="60" height="60"/> | <img src="https://assets.streamlinehq.com/image/private/w_34,h_34,ar_1/f_auto/v1/icons/development/json-v4ofnse1dqj8zl0otiifzw.png/json-2vox5uwk85x39kfwdwhtju.png" alt="JSON" width="60" height="60"/> |


---

## 🚀 Funcionalidades

- 📌 Ver todas las tareas registradas.  
- ➕ Agregar nuevas tareas.  
- ✅ Marcar tareas como completadas.  
- 🗑️ Eliminar tareas de la lista.  
- 💾 Persistencia de datos en archivo `tareas.json`.  

---
## 💻 Código Python
```python
import json
import os

# =============================
#   GESTOR DE TAREAS EN PYTHON
#   Autor: Wily Duvan Villamil Rey
#   LinkedIn: www.linkedin.com/in/wily-rey-administrador-bases-datos
# =============================

DB_FILE = "tareas.json"


def cargar_tareas():
    """Carga las tareas desde el archivo JSON, si existe."""
    if not os.path.exists(DB_FILE):
        return []
    with open(DB_FILE, "r", encoding="utf-8") as file:
        return json.load(file)


def guardar_tareas(tareas):
    """Guarda la lista de tareas en el archivo JSON."""
    with open(DB_FILE, "w", encoding="utf-8") as file:
        json.dump(tareas, file, indent=4, ensure_ascii=False)


def mostrar_tareas(tareas):
    """Muestra todas las tareas con su estado."""
    if not tareas:
        print("\n📌 No hay tareas registradas.")
        return
    print("\n=== LISTA DE TAREAS ===")
    for i, tarea in enumerate(tareas, start=1):
        estado = "✅ Completada" if tarea["completada"] else "❌ Pendiente"
        print(f"{i}. {tarea['titulo']} - {estado}")


def agregar_tarea(tareas):
    """Agrega una nueva tarea."""
    titulo = input("\nEscribe el título de la nueva tarea: ").strip()
    if titulo:
        tareas.append({"titulo": titulo, "completada": False})
        guardar_tareas(tareas)
        print("✅ Tarea agregada con éxito.")
    else:
        print("⚠️ El título no puede estar vacío.")


def marcar_completada(tareas):
    """Marca una tarea como completada."""
    try:
        num = int(input("\nNúmero de la tarea a completar: "))
        if 1 <= num <= len(tareas):
            tareas[num - 1]["completada"] = True
            guardar_tareas(tareas)
            print("🎉 Tarea marcada como completada.")
        else:
            print("⚠️ Número inválido.")
    except ValueError:
        print("⚠️ Debes ingresar un número.")


def eliminar_tarea(tareas):
    """Elimina una tarea de la lista."""
    try:
        num = int(input("\nNúmero de la tarea a eliminar: "))
        if 1 <= num <= len(tareas):
            tarea_eliminada = tareas.pop(num - 1)
            guardar_tareas(tareas)
            print(f"🗑️ Tarea '{tarea_eliminada['titulo']}' eliminada.")
        else:
            print("⚠️ Número inválido.")
    except ValueError:
        print("⚠️ Debes ingresar un número.")


def menu():
    """Menú principal de la aplicación."""
    tareas = cargar_tareas()
    while True:
        print("\n========= GESTOR DE TAREAS =========")
        print("1. Ver tareas")
        print("2. Agregar tarea")
        print("3. Marcar tarea como completada")
        print("4. Eliminar tarea")
        print("5. Salir")
        opcion = input("\nSelecciona una opción: ").strip()

        if opcion == "1":
            mostrar_tareas(tareas)
        elif opcion == "2":
            agregar_tarea(tareas)
        elif opcion == "3":
            mostrar_tareas(tareas)
            marcar_completada(tareas)
        elif opcion == "4":
            mostrar_tareas(tareas)
            eliminar_tarea(tareas)
        elif opcion == "5":
            print("\n👋 ¡Hasta luego! Tus tareas se han guardado.")
            break
        else:
            print("⚠️ Opción inválida. Intenta nuevamente.")


if __name__ == "__main__":
    menu()
```

## 📷 Vista previa

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1WHKgzsVDNzIcTWmNezrQXA0tvh3o28ZN" alt="Vista previa del Gestor de Tareas" width="900"/>
</p>

