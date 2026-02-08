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