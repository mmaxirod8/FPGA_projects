# 🖼️ Image Generator: Synthetic Street Scene

Este proyecto implementa un generador de señal de video sintética en VHDL. Su función principal es simular la entrada de una cámara para sistemas de asistencia al conductor (ADAS), generando una escena de carretera con movimiento y curvas sin necesidad de hardware de captura externo. Este proyecto se realizo con una FPGA Altera Cyclone IV (EP4CE22E22C7).

## 📂 Contenido de la Carpeta

### 🎥 Módulo Generador (Core)
* **`street_image.vhd`**: El corazón del proyecto. Genera señales de sincronismo VGA (640x480 @ 60Hz) y "dibuja" procedimentalmente la escena.
    * **Elementos generados:** Cielo, pasto y una carretera gris con línea central.
    * **Animación:** Simula una carretera curva calculando la posición central (`center_pos`) variable línea por línea.

### 🕵️ Módulos de Procesamiento (Lane Detection)
*Esta carpeta también incluye los archivos fuente del algoritmo de detección que se alimenta de este generador:*
* **`lane.vhd`**: Entidad superior que toma la señal de video y aplica detección de bordes.
* **`lane_sobel.vhd`**: Implementación del filtro Sobel para detectar los carriles.
* **`lane_linemem.vhd`**: Memoria de línea (Line Buffer) para el procesamiento de ventanas 3x3.

### 🧪 Simulación
* **`sim_street_image.vhd`**: Testbench diseñado para validar visualmente el generador.
    * Genera un archivo de salida `.ppm` (Portable Pixel Map) que permite ver en la computadora la imagen exacta que la FPGA enviaría al monitor VGA.

## 🚀 Cómo probar el Generador

Este proyecto no requiere una cámara real. Puedes visualizar la salida directamente mediante simulación:

1.  **Abrir ModelSim:** Carga el archivo `sim_street_image.vhd` y compila el proyecto.
2.  **Ejecutar Simulación:** Corre la simulación durante al menos 1 frame de video (aprox 16.7ms).
3.  **Verificar Salida:** El testbench creará un archivo llamado `image_out.ppm`.
    * Puedes abrir este archivo con *IrfanView*, *GIMP* o conversores online para ver la carretera generada sintéticamente.

## ⚙️ Detalles Técnicos VGA
El generador sigue el estándar de temporización VGA industrial:
* **Reloj de Píxel:** 25 MHz.
* **Resolución Activa:** 640 x 480 píxeles.
* **Sincronismo:** Generación manual de pulsos `h_sync` y `v_sync` basada en contadores.