# 🛣️ **Lane Detection in FPGA (Cyclone V)**
This directory contains the hardware implementation of a Lane Detection algorithm using image processing filters.

## 📂 Folder Content

* **`VHD Files/`**: Source code in VHDL (filtering, memory and control modules).
* **`C files/`**: C scripts (`bmp2sim`, `sim2bmp`) to convert BMP images to text and vice versa (necessary for simulation).
* **`Images/`**: Input & Output images we obtain along the project.
* **`Input and Output images txt/`**: Generated text files that represent the pixels for the simulation.

## 🚀 How to use this project

### Simulation Desing Flow for this specific project (Idea & Concepts)
<p align="center">
<img width="800" height="400" alt="Design flow Lane detection" src="https://github.com/user-attachments/assets/44bf5162-2353-4b90-9c55-0bc82e8e3f2d" />
</p>

1. What we do here is: first, we select the image to work with (input image [stimuli]). Using the C code fixed-point `lane_fixed.c`, we obtain our output image (output image [reference]) where Lane detection was applied.
2. Next, since VHDL cannot read the BMP format of the images from the previous step, we can convert them into text files (`.txt`) using the BMP files (in this case, `bmp2sim.c`). Each pixel in the image is represented using RGB, so this text file is quite large.
3. Then there are the VHDL files containing the `testbench` and `design` sections. These, along with the `.txt` files from the previous step, can be integrated and used in `ModelSim` (VHDL Simulator). This results in a `.txt` file.
4. And finally, to see the results in an image, we use the BMP file `sim2bmp.c` to convert the `.txt` output of ModelSim to a viewable `.bmp` image.

---

- ***Simulation on ModelSim:***
1. Abrimos ModelSim
2. Cargamos los siguientes archivos en el programa:

<p align="center">
<img width= "500" height="600" alt="image" src="https://github.com/user-attachments/assets/c7400780-bf31-4d48-b842-eed4e78f077e" />
</p>

3. Buscamos en la seccion superior la pestaña `Compile`, la desplegamos y le damos en `Compile All`.
4. Luego buscamos nuevamente en la parte superior la pestaña `Simulate`, desplegamos y le damos en `Start Simulation`.
5. Nos aparecera una ventana en donde tenemos que clickear en el signo mas de la casilla `work`. Se desplegara una lista con los archivos que subimos anteriormente, buscamos el archivo `sim_lane`, y le damos de nuevo al signo mas, donde por ultimo se desplegara una sub-lista y se encontrara el archivo `sim` (Arquitecture). Le damos click y luego en `Ok`.
6. Luego, debemos ubicar las variables de input y output, seleccionadolas y arrastrandolas, de la siguiente manera:

<p align="center">
<img width="500" height="630" alt="image" src="https://github.com/user-attachments/assets/8120d1b4-088a-4293-b7b7-bf47bb245b69" />
</p>

<p align="center">
<img width="800" height="605" alt="image" src="https://github.com/user-attachments/assets/fff1ec1f-b0a8-43fb-bec4-ebea6e9dd86a" />
</p>

***Aclaracion***: Aqui debemos de cambiar el formato de algunas variables. Aquellas que salgan con un valor de *UUUUUUUU*, las seleccionamos, le damos click derecho, en la ventana desplegamos la opcion `Radix` y por ultimo seleccionamos `Hexadecimal`. 

7. Finalmente, le damos en `Start Simulation`:

<p align="center">
<img width="900" height="200" alt="image" src="https://github.com/user-attachments/assets/a5df0943-78b5-4413-b810-cb3b711cb2bd" />
</p>


---

- ***Implementation on Quartus Prime & FPGA board:***
1. Como primer paso, configuramos Quartus Prime, dandole la ubicacion o directorio (en este mismo se deberan encontrar todos los archivos VHDL) y nombre del proyecto (este ultimo se debe llamar como el top level file, en este caso: `lane`). Luego le damos en `Next` y en `Empty Project`, donde aqui seleccionaremos la opcion `Add all` y se cargaran todos los archivos VHDL.

<p align="center">
<img width="500" height="800" alt="Captura de pantalla 2026-02-26 143751" src="https://github.com/user-attachments/assets/4dcda073-41ed-4b60-a6da-2a1cd790ba44" />
</p>

Seguido a esto deberemos colocar nuestra placa, en este caso, la Altera Cyclone V y su modelo: 5CEBA2F17C6, y seleccionamos en la parte inferior, donde sale como una especie de lista, a nuestro modelo de placa. Finalmente generamos el proyecto.

2. En el apartado superior de `Project Navigator` lo colocamos en modo `Files`.
3. Procedemos a seleccionar con un click el archivo `lane.vhd`. Luego nos vamos a la seccion superior donde aparacera `Assigments` y dentro de esta opcion buscamos `Import Assigments`. Aqui deberemos buscar, dandole click a los tres puntos, el archivo que contiene el pin map de la placa, el cual es (para este caso) `lane_default_Cyclone_V.qsf`.
4. Una vez aplicado los pasos anteriores, le damos en `Run` (simbolo play) y nos ejecutara la Sintesis, largandonos como resultado un archivo .bit .
5. Y aplicado los anteriores pasos, ya podremos subir el arhivo .bit obtenido ( o el archivo con extension `.sof`) en una placa FPGA fisica o en un laboratorio remoto de FPGA.


## 🛠️ Processing Tools (a.exe)

The `a.exe` file included in the root of this folder is the image processing engine for the simulation.

### What exactly does it do?
Because hardware simulators like ModelSim cannot directly process complex binary files like `.bmp`, this executable performs two critical functions:
1. **Pre-processing Mode:** Reads an image from the `/Images` folder and converts it into a hexadecimal data stream in a `.txt` file. This file is what the VHDL Testbench "reads" as if it were camera input.

2. **Post-processing Mode:** Takes the output `.txt` file generated by the simulation (containing the pixels processed by the Sobel/Lane Detection filter) and reconstructs it into a `.bmp` image for visual validation.

### Technical notes
* **Compilation:** It was compiled using GCC under the **Cygwin** environment.
* **Dependencies:** To run on Windows, it requires that the path has access to `cygwin1.dll`. If you have problems running it, it is recommended to recompile the files in `C files/` using your local compiler (MinGW, Visual Studio, etc.).
