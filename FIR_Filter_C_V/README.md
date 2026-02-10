# 📶 FIR Filter: Image Sharpening (Cyclone V)

Este directorio contiene la implementación en hardware de un filtro FIR (Finite Impulse Response) configurado como un filtro de nitidez (*Image Sharpening*) para procesamiento de imágenes en tiempo real sobre una FPGA Cyclone V.

## 📂 Contenido de las Carpetas

* **`VHD Files/`**: Código fuente en VHDL. Incluye:
    * `sharp.vhd`: Top entity del filtro.
    * `sharp_slice.vhd`, `sharp_linemem.vhd`: Lógica de buffers de línea y slices para el procesamiento de ventanas de píxeles.
    * `sharp_control.vhd`: Máquina de estados para el control de flujo.
    * `sim_*.vhd`: Testbenches para la simulación (incluyendo *self-checking*).
* **`Octave testing/`**: Scripts de MATLAB/Octave (`.m`) utilizados para generar los estímulos de prueba y verificar matemáticamente el algoritmo.
* **`Octave Images/`**: Imágenes de entrada (Bitmaps) y resultados generados por los scripts de prueba.
* **Archivos Raíz**:
    * `sharp.sdc`: Archivo de restricciones de tiempo (Synopsys Design Constraints).
    * `sharp_default_Cyclone_V.qsf`: Configuración de pines y proyecto para Quartus Prime.

## 🚀 Cómo usar este proyecto

El flujo de trabajo es híbrido, utilizando Octave para pre-procesar las imágenes y ModelSim para la simulación del hardware.

1.  **Generar Testbench:** Ejecuta el script `sharp_generate_testbench_images.m` en Octave/Matlab. Esto tomará las imágenes de la carpeta `Octave Images` y generará los archivos de texto/hexadecimal necesarios que la FPGA "lee" durante la simulación.
2.  **Simulación HDL:** Abre el proyecto en ModelSim, compila los archivos de `VHD Files/` y ejecuta el testbench `sim_sharp.vhd`.
3.  **Validación Cruzada:** El script `sharp_image_filter.m` contiene el modelo de referencia en software ("Golden Model"). Puedes comparar la salida de la simulación de la FPGA con la salida generada por este script para asegurar que el hardware se comporta exactamente como el modelo matemático.

## 🛠️ Herramientas de Verificación (Octave Scripts)

A diferencia de proyectos anteriores en C, este diseño utiliza scripts de alto nivel (`.m`) para automatizar el flujo de datos.

### Funciones Principales
* **`sharp_generate_testbench_images.m`**:
    * Actúa como el puente entre el mundo de las imágenes (`.bmp`, `.jpg`) y el mundo digital.
    * Convierte la matriz de píxeles de la imagen en vectores de prueba compatibles con el Testbench VHDL.
* **`sharp_image_filter.m`**:
    * Implementa el algoritmo de convolución del filtro de nitidez en software.
    * Sirve para validar que la lógica aritmética (`sharp_arith.vhd`) implementada en la FPGA calcula los valores de píxel correctos, manejando desbordamientos y saturación de la misma manera que el hardware.
* **`write_ascii_ppm.m`**:
    * Utilidad para exportar los resultados visuales en formato PPM (Portable Pixel Map), facilitando la visualización rápida de la salida de la simulación sin necesidad de visores complejos.