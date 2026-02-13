# 📶 FIR Filter: Image Sharpening (Cyclone V)

Este directorio contiene la implementación en hardware de un filtro FIR (Finite Impulse Response) configurado como un filtro de nitidez (*Image Sharpening*) para procesamiento de imágenes en tiempo real sobre una FPGA Cyclone V.

## 📂 Contenido de las Carpetas

* **`VHD Files/`**: Código fuente en VHDL. Incluye:
    * `sharp.vhd`: Top entity del filtro.
    * `sharp_slice.vhd`, `sharp_linemem.vhd`: Lógica de buffers de línea y slices para el procesamiento de ventanas de píxeles.
    * `sharp_control.vhd`: Máquina de estados para el control de flujo.
    * `sim_*.vhd`: Testbenches para la simulación (incluyendo *self-checking*).
* **`Octave testing/`**: Scripts para MATLAB/Octave (`.m`) utilizados para generar los estímulos de prueba y verificar matemáticamente el algoritmo (abrirlos con NotePad++ o editor de texto).
* **`Octave Images/`**: Imágenes de entrada (Bitmaps) y resultados generados por los scripts de prueba.
* **Archivos Raíz**:
    * `sharp.sdc`: Archivo de restricciones de tiempo (Synopsys Design Constraints).
    * `sharp_default_Cyclone_V.qsf`: Configuración de pines y proyecto para Quartus Prime.

## 🚀 Cómo usar este proyecto

El flujo de trabajo es híbrido, utilizando Octave para pre-procesar las imágenes y ModelSim para la simulación del hardware.

1.  **Generar Self-Testbench:** Ejecutar el script `sharp_generate_testbench_images.m` (abriendolo con NotePad++ u otro editor de texto, y copiando el codigo en Octave/MatLab). Este codigo lo que hace es: 
- Aplicar FIR Filter a la imagen input [image stimulation] (que como consecuencia generará una imagen output [image expected])
- Transformar a ambas imagenes (entrada y salida) en imagenes con formato PPM, con codificacion ASCII (necesarios que la FPGA "lee" durante la simulación.)
Basicamente tomará de la carpeta (en donde se ubica el script o archivo.m, que debe encontrarse en la misma ubicacion donde esta la imagen a trabajar) la imagen a la que queremos aplicar el FIR Filter, y generara 2 archivos (imagen PPM input e imagen PPM output [FIR Filter Aplicado])
**Se deben cambiar los nombres de las imagenes tanto en el script a implementar como en archivo VHD testebench (`sim_sharp.vhd`)**
2.  **Simulación HDL:** Abre el proyecto en ModelSim, compila los archivos de `VHD Files/` y ejecuta el testbench `sim_sharp.vhd`.
3.  **Validación Cruzada:** El script `sharp_image_filter.m` contiene el algoritmo a implementar. Puedes comparar la salida de la simulación de la FPGA con la salida generada por este script para asegurar que el hardware se comporta exactamente como el modelo matemático. Basicamente esto es una verificacion del algoritmo, que queremos que realice el FPGA, y de forma rapida verificamos si el algoritmo realiza lo que deseamos usando Octave/MatLab para posterior implementacion en la placa.

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
