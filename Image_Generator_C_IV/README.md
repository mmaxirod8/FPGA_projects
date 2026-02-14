# 🖼️ Image Generator: Synthetic Street Scene

This project implements a synthetic video signal generator in VHDL. Its main function is to simulate the input from a camera for Advanced Driver Assistance Systems (ADAS), generating a road scene with movement and curves without the need for external capture hardware. This project was carried out using an Altera Cyclone IV FPGA (EP4CE22E22C7).

## 📂 Folder Content

### 🎥 Generator Module (Core)
* **`street_image.vhd`**: The heart of the project. It generates VGA sync signals (640x480 @ 60Hz) and procedurally "draws" the scene.
    * **Elementos generados:** Sky, grass and a gray road with a center line.
    * **Animación:** Simulate a curved road by calculating the variable center position (`center_pos`) line by line.
    
### 🕵️ Processing Modules (Lane Detection)
*This folder also includes the source files for the edge detection algorithm that this generator uses. As you'll see, these are the same files found in the FPGA project `Lane_detection_C_V` (from this same repository), so we can apply its algorithm to `Image_Generator_C_IV`.:*
* **`lane.vhd`**: Upper entity that takes the video signal and applies edge detection.
* **`lane_sobel.vhd`**: Implementation of the Sobel filter to detect lanes.
* **`lane_linemem.vhd`**: Line buffer for 3x3 window processing.

### 🧪 Simulation
* **`sim_street_image.vhd`**: Testbench designed to visually validate the generator.
    * It generates an `.ppm` (Portable Pixel Map) output file that allows you to see on your computer the exact image that the FPGA would send to the VGA monitor.

## 🚀 How to test the Generator

This project does not require a real camera. You can view the output directly through simulation:

1.  **Open ModelSim:** Load the `sim_street_image.vhd` file and compile the project.
2.  **Run Simulation:** Run the simulation for at least 1 video frame (approx. 16.7ms).
3.  **Verify Output:** The testbench will create a file called `image_out.ppm`.
    * You can open this file with *IrfanView*, *GIMP* or online converters to see the synthetically generated road.

## ⚙️ VGA Technical Details
The generator follows the industrial VGA timing standard:
* **Pixel Clock:** 25 MHz.
* **Active Resolution:** 640 x 480 pixels.
* **Synchronization:** Manual generation of `h_sync` and `v_sync` pulses based on counters.
