# 📟 This repository contains several projects I've completed on various FPGAs, including code, help files, and results.

### 📌 Some abbreviations (like "C_V", "C_IV", "X_N_3", etc.) are for the following FPGAs:
 - C --> Altera Cyclone / V, IV (Board model)
 - X --> Xilinx / N --> Nexys (Board model) / N° [e.g: 3] (Version number of the board model)
 - X --> Xilinx / Z --> Zedboard (Board model) 

### 🗃️ Estructura del Proyecto
```
FPGA_projects/
├── FIR_Filter_C_V  
│   ├── Octave Images/
│   │   ├── street_A.bmp
│   │   └── street_AA.bmp
│   │
│   ├── Octave testing/
│   │   ├── prueba1.m
│   │   ├── sharp_generate_testbench_images.m
│   │   ├── sharp_image_filter.m
│   │   └── write_ascii_ppm.m
│   │
│   ├── VHD Files/
│   │   ├── sharp.vhd
│   │ 
│   ├── README.md
│   │
│   ├── sharp.sdc
│   │
│   └── sharp_default_Cyclone_V.qsf
│
│
├── Image_Generator_C_IV/         
│   ├── Lane_detection_VHD_Files/
│   ├── Street_image_VHD_Files/
│   ├── README.md
│   └── lane_default_Cyclone_IV
│       
│
├── Lane_detection_C_V/         
│   ├── C files/
│   │   ├── bmp24_io.c
│   │   ├── bmp2sim.c
│   │   ├── lane_fixed.c
│   │   ├── lane_float.c
│   │   ├── lane_testbench.c
│   │   └── simp2bmp.c
│   │
│   ├── Images/
│   │   ├── Simulation Looks like
│   │   │   ├── VHDL Simulation 2.png
│   │   │   ├── VHDL Simulation.png
│   │   │     
│   │   ├── Street_A_edge_fixed.bmp
│   │   ├── Street_C_edge_float.bmp
│   │   ├── street_A.bmp
│   │   ├── street_A_edge_float.bmp
│   │   ├── street_B.bmp
│   │   ├── street_B_edge_float.bmp
│   │   └── street_C.bmp
│   │
│   ├── Input and Output images txt (self-testbench)/
│   │   ├── street_0_expected.txt
│   │   └── street_0_stimuli.txt
│   │
│   ├── VHD Files/
│   │   ├── lane.vhd
│   │   ├── lane_g_matrix.vhd
│   │   ├── lane_g_root.mif
│   │   ├── lane_g_root_IP.vhd
│   │   ├── lane_linemem.vhd
│   │   ├── lane_sobel.vhd
│   │   ├── lane_sync.vhd
│   │   └── sim_lane.vhd
│   │
│   ├── README.md
│   │
│   └── a.exe
│
│
├── Projects_results
│   ├── FIR Filter Cyclone V/
│   ├── Image Generator Cyclone/
│   ├── Lane detection Cyclone V/
│   ├── Test Images/
│   ├── Machine Learning Result.png
│   └── README.md
│
│
└── README.md
```

¡I hope you find it useful!


🙌 Credits to: 
- *Prof. Dr. Marco Winzker* from Bonn-Rhein-Sieg University of Applied Sciences
- *Andrea Schwandt* from Bonn-Rhein-Sieg University of Applied Sciences
- *Alejandro Enrique Nuñez Manquez* from Universidad Nacional de San Luis
