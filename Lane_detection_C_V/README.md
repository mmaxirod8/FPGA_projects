# 🛣️ Detección de Carriles en FPGA (Cyclone V)

Este directorio contiene la implementación en hardware de un algoritmo de detección de carriles (Lane Detection) utilizando filtros de procesamiento de imágenes.

## 📂 Contenido de las Carpetas

* **`VHD Files/`**: Código fuente en VHDL (módulos de filtrado, memoria y control).
* **`C files/`**: Scripts en C (`bmp2sim`, `sim2bmp`) para convertir imágenes BMP a texto y viceversa (necesario para simulación).
* **`Images/`**: Imágenes de prueba (carreteras) y resultados visuales.
* **`Input and Output images txt/`**: Archivos de texto generados que representan los píxeles para la simulación.

## 🚀 Cómo usar este proyecto

1. **Generar estímulos:** Usa `bmp2sim.exe` para convertir una imagen de la carpeta `Images` a `.txt`.
2. **Simular:** Ejecuta el testbench en ModelSim cargando el archivo `.txt` generado.
3. **Ver resultados:** Usa `sim2bmp.exe` para convertir el `.txt` de salida de ModelSim a una imagen `.bmp` visible.

## 🛠️ Herramientas de Procesamiento (a.exe)

El archivo `a.exe` incluido en la raíz de esta carpeta es el motor de procesamiento de imágenes para la simulación. 

### ¿Qué hace exactamente?
Debido a que los simuladores de hardware como ModelSim no pueden procesar archivos binarios complejos como `.bmp` directamente, este ejecutable realiza dos funciones críticas:
1. **Modo Pre-procesamiento:** Lee una imagen de la carpeta `/Images` y la convierte en un flujo de datos hexadecimal en un archivo `.txt`. Este archivo es el que "lee" el Testbench de VHDL como si fuera la entrada de una cámara.
2. **Modo Post-procesamiento:** Toma el archivo `.txt` de salida generado por la simulación (que contiene los píxeles procesados por el filtro Sobel/Lane Detection) y lo reconstruye en una imagen `.bmp` para validación visual.

### Notas técnicas
* **Compilación:** Fue compilado utilizando GCC bajo el entorno **Cygwin**.
* **Dependencias:** Para ejecutarse en Windows, requiere que la ruta tenga acceso a `cygwin1.dll`. Si tienes problemas al ejecutarlo, se recomienda recompilar los archivos en `C files/` usando tu compilador local (MinGW, Visual Studio, etc.).