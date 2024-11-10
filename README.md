# Parallel-Volume-Rendering

## Overview

The `Parallel_Distribution_Axis-Aligned_Volume_Rendering` project implements parallel volume rendering using MPI (Message Passing Interface). This Python program performs ray casting on a 3D scalar volume dataset, with data partitioned across multiple processes to achieve efficient rendering. The script uses color and opacity transfer functions for volume rendering and outputs performance metrics along with the final rendered image.

## Features
- **Parallel Volume Rendering:** Processes large datasets with MPI to leverage distributed memory systems.
- **3D Domain Partitioning:** Supports 3D decomposition of the volume dataset across X, Y, and Z axes.
- **Ray Casting:** Applies color and opacity transfer functions along each ray for rendering, using front-to-back compositing.
- **Performance Reporting:** Outputs timing metrics for decomposition, data loading, ray casting, and final composition.
- **Image Stitching:** Combines image slices from each process to create a final composite image of the volume.

## Prerequisites
Ensure the following Python libraries are installed:

- `mpi4py`: For MPI support in Python.
- `argparse`: For command-line argument parsing.
- `numpy`: For numerical operations and handling large arrays.
- `matplotlib`: For visualizing and saving rendered images.
- `time` and `os`: For timing calculations and file manipulation.



## Input Files
The program requires the following input files:

**Volume Dataset:** A .raw file containing the 3D volume data (e.g., Isabel_1000x1000x200_float32.raw).
Color Transfer Function (TF): A text file defining color mappings for scalar values (e.g., color_TF.txt).
Opacity Transfer Function (TF): A text file defining opacity mappings for scalar values (e.g., opacity_TF.txt).
Color and Opacity Transfer Files
The color transfer file should contain values formatted as (scalar, R, G, B), where R, G, B are color components for each scalar value.
The opacity transfer file should have entries like (scalar, opacity) for each scalar value.

1. **WHILE USING SINGLE SYSTEM**
   
**Running the Script**

To run the script, use mpiexec with the desired number of MPI processes. Replace <num_processes> with the number of processes, matching the specified grid dimensions (e.g., PX * PY * PZ).


mpiexec --oversubscribe -np <num_processes> python3 volume_rendering.py <input_dataset> <PX> <PY> <PZ> <stepsize> <color_tf> <opacity_tf>

2. **WHILE USING HOSTFILE(MULTIPLE SYSTEMS)**
   
**Running the Script**

mpirun --mca btl_tcp_if_include eno1 -hostfile hostfile.txt --oversubscribe -np num_of_processes python3 script.py dataset_filename PX PY PZ step_size color_tf_dataset opacity_tf_dataset

**Arguments**
<input_dataset>: Path to the volume data file (e.g., Isabel_1000x1000x200_float32.raw).
<PX> <PY> <PZ>: Number of partitions along the X, Y, and Z axes, respectively (must satisfy P = PX * PY * PZ).
<stepsize>: Step size for ray casting along the Z-axis.
<color_tf>: Path to the color transfer function file.
<opacity_tf>: Path to the opacity transfer function file.


## OUTPUT IMAGE
1. **WHILE USING SINGLE SYSTEM**
![2 1 1](https://github.com/user-attachments/assets/0be49977-499c-48c2-acb1-91b559b431e5)

![WhatsApp Image 2024-11-10 at 23 44 19_5529d90e](https://github.com/user-attachments/assets/a1894add-63ef-41bc-8800-53b965ef2443)
![WhatsApp Image 2024-11-10 at 23 42 29_6631def0](https://github.com/user-attachments/assets/b16f9576-d23e-40aa-bd63-4bdf7cb19c35)

2. **WHILE USING HOSTFILE(MULTIPLE SYSTEMS)**
![2 1 1](https://github.com/user-attachments/assets/0be49977-499c-48c2-acb1-91b559b431e5)

![hostfile_command](https://github.com/user-attachments/assets/72c7a46d-750d-40e5-ad79-61958ccbeeb7)
![hostfile](https://github.com/user-attachments/assets/9ce031a3-eca8-414f-99d5-d10a76314ae7)







