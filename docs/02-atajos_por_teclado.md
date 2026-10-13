# Dominio de la Línea de Comandos: Atajos Esenciales en RHEL 10

> **Nota Contexto Real:**  
> Cuando administramos servidores empresariales Linux, **no tenemos entorno gráfico (GUI) ni mouse**. Todo se gestiona mediante sesiones remotas por SSH. El cual es indispensable saber moverse por la terminal el cual es una habilidad crítica para operar con velocidad, evitar errores y resolver incidentes bajo presión.


## Guía de Supervivencia: Atajos Esenciales de la Shell

A continuación, resumo los atajos que considero importantes en la terminal:

| Combinacion de teclas | ¿Qué hace? | 🛠️ ¿Por qué lo aplico en entornos reales? |
| :--- | :--- | :--- |
| **`Ctrl + c`** (cancel) | Cancela el proceso interactivo actual. | **Cancelación ante comandos colgados:** Lo uso de inmediato cuando un comando como un `ping` continuo o una consulta pesada se queda congelado y necesito recuperar el control de la terminal. |
| **`Ctrl + d`** (delete)| Envía una señal de fin de archivo | **Cierre limpio de sesión:** Sirve para salir de la shell actual de manera rápida y segura (equivale a escribir `exit` o `logout`). |
| **`Ctrl + a`** | Mueve el cursor al **inicio** de la línea de comandos. | **Edición rápida:** En lugar de usar las flechas del teclado n veces a la izquierda, me ayuda a ubicarme al inicio del comando con la finalidad de  corregir una sintaxis. |
| **`Ctrl + e`** (end) | Mueve el cursor al **final** de la línea de comandos. | **Agilidad en comandos largos:** Me permite saltar al final de una línea compleja para agregar redireccionamientos (`>`) o parámetros adicionales. |
| **`Ctrl + r`** | Búsqueda en el historial de comandos (`reverse-i-search`). | **Memoria histórica:** Es mi atajo favorito. En lugar de presionar la flecha arriba 50 veces hasta encontrar el comando qeu estoy buscando **Unicamente hago Ctrl + r escribo nano y sigo presionando Ctrl + r y me iran apareciendo todos los comandos con nano qeu hice anteriormente** . |
| **`Ctrl + l`** | Limpia la pantalla de la consola. | **limpieza:** Es mucho más rápido que escribir `clear`. Mantiene la terminal limpia mientras trabajo en múltiples configuraciones. |
| **`Ctrl + u`** | Borra toda la línea desde el cursor hacia la izquierda. | **Corrección de errores:** Si escribí mal la mitad de un comando largo, lo borro por completo de un solo golpe sin tener que mantener presionada la tecla de retroceso (`Backspace`). |
| **`Alt + b`** (backward/atras)  | Mueven el cursor una palabra atrás. | **Navegación precisa:** Permiten saltar palabra por palabra al revisar rutas de directorios extensas (ej. `/etc/systemd/system/`). |
|  **`Alt + f`** /(forward/adelante) | Mueven el cursor una palabra adelante. | **Navegación precisa:** Permiten saltar palabra por palabra al revisar rutas de directorios extensas (ej. `/etc/systemd/system/`). |

---

## **Trucos Extra** 

> **Consejo Práctico:**  
> * **`Ctrl + z`**: Envía un proceso activo a segundo plano (`background`). Muy útil si estás editando un archivo o ejecutando una tarea y necesitas hacer otra consulta rápida sin cerrar lo anterior.
> * **`!!` (Doble exclamación)**: Repite de inmediato el comando anterior. Lo uso muchísimo cuando olvido poner `sudo` al inicio: solo escribo `sudo !!` y me ahorra volver a teclear todo el comando.

---

## **Conclusión del Laboratorio**
El dominio de la terminal es la base de todo lo demás (desde configurar un servidor web hasta desplegar clústeres de almacenamiento con Stratis o reglas estrictas de SELinux).
