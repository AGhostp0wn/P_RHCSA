# Módulo: Navegación Avanzada, Enlaces y Procesamiento en la Consola RHEL

> **Consolas Virtuales:**  
Saber movernos entre consolas virtuales (`chvt`), entender los inodos, gestionar enlaces eficientemente para ahorrar almacenamiento y extraer datos estructurados con herramientas de texto (`awk`, `cut`, `sort`) es lo que diferencia a un administrador eficiente.

---

## 1. Gestión de Consolas Virtuales (TTY)
Cuando trabajamos en modo consola en Linux, podemos abrir múltiples sesiones independientes sin necesidad de abrir ventanas gráficas:
* **`sudo chvt 4`**: Crea o salta directamente a la consola virtual número 4. Si la consola ya existe previamente, te redirige a ella; si no existe, la inicializa en segundo plano.
* **`w` o `who`**: Permite listar las sesiones de terminal activas en el sistema, identificándolas mediante su identificador `tty` correspondiente.
* **`sudo pkill -9 -t tty4`**: Elimina la consola virtual tty4 esto dependera de qeu consola virtual deseo eliminar guiarme con el comando  `w` o `who` para identificar cual eliminar.
---

## 2. Búsqueda de Archivos con Patrones
Para buscar o listar archivos específicos utilizando patrones de caracteres:
* **`ls -lda a*`**: Lista únicamente los directorios o archivos cuyo nombre comience con la letra `a`.
* **`ls -l -d a??a* /etc`**: Busca elementos que comiencen con `a`, tengan exactamente dos caracteres cualesquiera (`??`), luego una letra `a`, y continúen con cualquier otro patrón.
* **`ls -l -d a*a*` /etc**: Filtra archivos que contengan al menos dos letras `a` en su estructura dentro de /etc.
* **`ls -l /lib/modules/$(uname -r)`**: Lista de manera dinámica el contenido del directorio de módulos del kernel correspondiente exactamente a la versión en ejecución (`uname -r`).
* **`man hier`**: Muestra un resumen detallado de la jerarquía de directorios estándar en Linux y qué propósito cumple cada ruta principal.

---

## 3. Inodos y Enlaces (Duros vs. Simbólicos)
Para optimizar recursos y gestionar accesos a archivos:
* **`ls -li`**: Muestra el listado detallado incluyendo el número de **inodo** (el puntero único en disco que identifica al archivo).
* **Enlaces Duros (`ln /ruta_original /ruta_nueva`)**: Apuntan exactamente al mismo inodo en disco. Si modificas uno, el otro cambia al instante; e incluso si eliminas el archivo original, la copia sigue funcionando porque comparten la misma estructura física.
* **Enlaces Simbólicos (`ln -s /ruta_absoluta /ruta_nueva`)**: Funcionan como un acceso directo avanzado. Ahorran espacio masivo en disco ya que no duplican la información (ideal para gigabytes de datos). **TENER CUIDADO:** Si la ruta o archivo original es eliminado, el enlace simbólico se rompe y deja de funcionar.

---

| Característica | Enlace Duro (Hard Link) | Enlace Simbólico (Soft/Symlink) |
| :--- | :--- | :--- |
| **Naturaleza** | Apunta directamente al mismo inodo y bloques de datos en disco. | Es un archivo independiente que almacena la ruta hacia el archivo o carpeta original. |
| **Inodo** | Comparte exactamente el mismo inodo que el archivo original. | Tiene su propio inodo, diferente al del archivo original. |
| **Directorios** | No se pueden crear para directorios (por seguridad y evitar ciclos). | Sí se pueden crear para directorios. |
| **Sistemas de archivos** | Limitados al mismo sistema de archivos o partición. | Pueden cruzar entre diferentes particiones, discos o sistemas de archivos. |
| **Si se borra el original** | Los datos siguen accesibles a través del enlace duro. | El enlace se rompe y queda "huérfano" (no apunta a nada útil). |
| **Comando de creación** | `ln <origen> <enlace>` | `ln -s <origen> <enlace>` |
| **Identificación visual** | Se ve como un archivo normal (el contador de enlaces del inodo aumenta). | Se identifica con una `l` al inicio de los permisos (`ls -l`). |
 ## Cuándo usar 


| Si quieres hacer esto... | Usa... | ¿Por qué? |
| :--- | :--- | :--- |
| **Un acceso directo a una carpeta** | Simbólico | El enlace duro no lo permite por restricciones del sistema. |
| **Conectar archivos entre distintos discos** | Simbólico | El enlace duro está limitado estrictamente al mismo disco o partición. |
| **Proteger un archivo para que nunca se borre por error** | Duro | Aunque borres el original, el archivo sigue vivo en el enlace duro. |
| **Crear "atajos" normales en tu día a día** | Simbólico | Es mucho más fácil de rastrear, borrar y administrar visualmente. |
| **Hacer respaldos eficientes (Backups/Snapshots)** | Duro | Permite que un archivo aparezca en múltiples fechas de respaldo sin duplicar su tamaño en disco (como hace *Rsync*). |
| **Mantener un archivo activo en dos rutas a la vez** | Duro | Ideal para descargar un archivo gigante (ej. Torrent), moverlo a tu carpeta multimedia para verolo y dejar el otro sembrando sin duplicar espacio. |



## 4. Filtrado, Ordenamiento y Transferencia de Datos 
* `cut -d : -f 3 /etc/passwd | sort` delimita el archivo por dos puntos (`-d :`), extrae exclusivamente la tercera columna (`-f 3`) y la ordena alfabéticamente.
*  `sort -t : -k3n /etc/passwd` muestra todo el contenido del archivo de usuarios, ordena numericamente (`n`) tomando como referencia  la tercera columna (`-k3`).
*  `awk -F : ' /alexander/ { print $4 }' /etc/passwd` utiliza `:` como separador, busca las coincidencias con la palabra "alexander" e imprime únicamente el valor del cuarto campo de esa línea.
* **Transferencias seguras por Red (`scp`)**: 
  `scp /etc/passwd juan@IP:/tmp/` transfiere de forma cifrada un archivo local hacia un servidor remoto mediante el protocolo SSH.

### PARA MAS INFORMACIÓN PODEMOS USAR EL COMANDO MAN 
EJEMPLO:

man awk, man sort,man grep

ESTO NOS AYUDA A VER COMO FUNCIONA EL COMANDO Y LOS PARAMETROS ADMITIDOS Y APRA QEU SIRVEN.