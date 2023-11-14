# Diffuse Optical Tomography Dataset

## Overview
This repository houses a simulated dataset designed for Frequency-domain Diffuse Optical Tomography (FD-DOT) experiments. Each example comprises a target volume representing 3D absorption and reduced scattering properties randomized within a biologically realistic range for breast tissue. Additionally, it includes amplitude and phase components of corresponding frequency-domain reflectance measurements simulated using a high-density grid of source/detector pairs. The dataset encompasses raw data, preprocessed data, mesh information, and supplementary metadata. A detailed description of the dataset structure and contents is provided below.

## File Structure

### Mesh 
- `data/mesh.mat`: The mesh used to generate the data in Matlab using the NIRFAST package.

### Main Data 
- `data/simulated_linescans`: The main dataset.

#### Dataset Information
- `data/simulated_linescans/dataset_info.json`: Information about the dataset in JSON format.

#### Measurement List
- `data/simulated_linescans/measurement_list.csv`: A table containing information on source and detector positions for each SD pair used to generate the data. Each row corresponds to one value in the raw data measurements.

#### Raw Data
- `data/simulated_linescans/raw/1.mat`: Raw data for example 1.
  - Each /mat data file contains the following fields:
    - `amplitude_clean`: Amplitude measurements for each source/detector pair.
    - `amplitude_noisy`: Amplitude_clean plus added noise based on a system-derived amplitude-dependent noise model.
    - `phase_clean`: Phase measurements for each source/detector pair.
    - `phase_noisy`: Phase_clean plus added noise based on a system-derived amplitude-dependent noise model.
    - `target`: Ground truth optical properties used to simulate the data. Dimensions represent [x position, y position, z position (depth), optical property (1=mua, 2=mus’)]
    - `roi_mask`: Binary mask indicating the presence of anomalies in the target volume. Dimensions represent [x position, y position, z position (depth)]
    - `info`: Example-specific information, including the background optical properties, and spatial & contrast details of each anomaly.

#### Preprocessed Data 
- `data/simulated_linescans/prepro/prepro_info.json`: Information about the preprocessing procedure used to generate this data.
- `data/simulated_linescans/prepro/train`
  - `X.npy`: Preprocessed measurement data in the train split in .numpy format. Dimensions represent [number of examples, number of measurements]
  - `Y.npy`: Preprocessed target volume data in the train split in .numpy format. Dimensions represent [number of examples, x position, y position, z position (depth), optical property (1=mua, 2=mus’)]
  - `W.npy`: Preprocessed region of interest masks in the train split in .numpy format. Dimensions represent [number of examples, x position, y position, z position (depth)]
- `data/simulated_linescans/prepro/val`:
  - Same structure for the validation split.

### Test Disk Data 
- `data/simulated_linescans_testdisks`: Test dataset containing manually designed volumes to test parameter separation and depth sensitivity. 
  - Same structure as `data/simulated_linescans` but also contains:
    - `data/simulated_linescans_testdisks/example_list.csv`: Depth and optical property information for each test disk example.


This dataset was produced as part of a project supported by the National Institute of Biomedical Imaging and Bioengineering (NIBIB) of the National Institutes of Health (NIH) Award Number R01EB029595.
Feel free to contact Robin Dale at rbd079@student.bham.ac.uk for any inquiries or additional information.
