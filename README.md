# Case Drone signature classification

## 1. Cardinal Radio Frequency (CARDRF) Dataset
Olusiji O Medaiyese (email:medaiyese09@gmail.com)  
Martins Ezuma (email: mcezuma@ncsu.edu)  
Adrian P Lauf (email:adrian.lauf@louisville.edu)  
Ayodeji A Adeniran (email:aaaden02@louisville.edu)

### INTRODUCTION

In this work, we curated an open-source dataset called the Cardinal RF dataset, abbreviated as the CardRF dataset. Here, both the UAV and UAV flight controller signals from six UAS (unmanned aerial systems), WiFi signals from two WiFi devices, and Bluetooth signals from five devices are used to acquire the CardRF dataset in an outdoor environment. The device catalogue (UAS, Bluetooth, and WiFi) is listed in Table I. The Bluetooth and WiFi devices are used to acquire Bluetooth and WiFi signals, respectively. Similarly, two components (i.e., UAV and its flight controller) of a UAS are utilized in collecting the UAS signals.

TABLE I
CATALOG OF RF DEVICES USED IN THE EXPERIMENT FOR 2.4 GHZ RF
FINGERPRINT ACQUISITION.

The experiment was conducted during the Summer of 2020 (August 2020) using the AERPAW (Aerial Experimentation Research Platform for Advanced Wireless) facility [1] which is called the Lake Wheeler site. The site is located at 4191 Mid Pines Road, Raleigh, North Carolina, USA.

### EXPERIMENTAL MODEL AND DESIGN

The experimental model and design have been discussed in [2]. Please refer to [2] for how we deal with the absence of RF signals in an environment.

This work has been supported in part by NASA under the Federal Award ID number NNX17AJ94A, and by NSF CNS-1939334 Aerial Experimentation Research Platform for Advanced Wireless (AERPAW) project that supported the experiments at NC State.

### DATA ACQUISITION

The data acquisition is categorized into visual line-of-sight (VLOS) and beyond-visual-line-of-sight (BVLOS) data collection.
1) Visual line of sight data: The VLOS is synonymous to light-of-sight (LOS). During the VLOS signal capturing, there is no obstruction between the RFSSCS (RF signal sensing and capturing system) and the device (i.e., UAV, UAV controller, or other devices). Fig 1(a) and Fig 1(b) show the VLOS capturing of a UAV controller and UAV (DJI Matrice 600), respectively. Signals are captured at a distance range of 8 - 12 meters between the devices and RFSSCS.

2) Beyond-visual-line-of-sight: BVLOS is synonymous with non-line-of-sight (NLOS). In BVLOS data capturing, there is an obstruction between the RFSSCS and the devices. This is to analyze the impact of multi-path fading or other channel effects on the RF signature. Fig 2 shows the BVLOS UAV signal capturing where the UAV is flying adjacent to a building. Only three UAVs’ signals (i.e., DJI Inspire, DJI Matrice 600, and DJI Phantom) are captured for this collection.

### DATA DESCRIPTION AND UTILIZATION

The data labeling is done by a manual process using a directory and sub-directories. Fig. 3 shows the directory tree for the labeling of the RF dataset. The root directory is the name of the dataset repository, which is called CardRF. Because signals are captured at LOS and NLOS, two sub-directories are created for LOS and NLOS. Four categories of signals (i.e., UAV, UAV controller, Bluetooth, and WiFi) are collected for the LOS data collection. So for each category of signals, a sub-directory is created under the LOS directory to store the signals. Similarly, only UAV signals are captured at NLOS. So the NLOS directory only contains the UAV sub-directory. Please refer to [2], [3] for the detailed data description. Fig. 6 shows a signal captured from DJI Phantom 4 flight controller where the transient and steady state of the signal are labeled.


Fig. 1. The RFSSCS setup for visual line of sight capturing of signals from : (a) a UAV controller, (b) a UAV (DJI Matrice 600).


Fig. 2. The RFSSCS setup for beyond-visual-line-of-sight capturing of signals from UAV.

CARDRF directory has the raw signals and it is split to train and test set already. The Processed CardRF directory has the sliced steady signals from LOS with respective class or label. Each signal in the processed CardRF directory has 1024 sampling points. MATLAB code used for processed CardRF is in code directory. In the code folder, there is a MATLAB file (SIGN ALP LOT.mlx) for plotting the signals. However, the raw signals need to be scaled by using a scale factor of 6. 581 e− 06 for the voltage. The detail of the scaling is in the file. 



Fig. 3. Directory tree for data label of the Cardinal RF dataset.


Fig. 4. Directory tree for the LOS UAV signal labels showing the UAV models and UAV flight modes as sub-directories and sub-directories of sub-directories,
respectively.


Fig. 5. Directory tree for the NLOS UAV signal labels showing the UAV models and UAV flight modes as sub-directories and sub-directories of sub-directories,
respectively.


Fig. 6. A typical example of a signal captured from DJi Phantom 4 flight controller (adopted from [2])

### Files structure

* We have kept their directory structure and their naming convention.
* The directory stucture is as follows (note that not every directory leaf has data):

| 1st level: type of experiment | 2nd level: data split | 3rd level: device type | 4th level: device | 5th level: activity (only for UAVs) |
|----------------------- |----------------------- |----------------------- |----------------------- |----------------------- |
| LOS - visual line-of-sight | Train - training data | BLUETOOTH - bluetooth mobile devices | <device_name> | FLYING |
| NLOS - beyond visual line-of-sight| Test - test data | UAV - prosumer grade drones | | HOVERING |
| | | UAV_controller - drone controllers | | VIDEOING |
| | | WIFI - wifi routers | |

* File naming convention:
```
BEEBEERUN_0000100001.mat_data.csv  
,where  
BEEBEERUN_00001 - device name and model  
00001 - consecutive number of experiment (some of them are missing)  
.mat - file extention (we should have removed it, but we did not)
_data.csv / _meta.csv - data type recorded in the file - 'data' for raw data, 'meta' - for metadata
```

* Every metadata file has these fields:
 
|NumPoints|NumSegments|WaveformType|XDispOrigin|XDispRange|XInc|XOrg|XUnits|YDispOrigin|YDispRange|YInc|YOrg|YUnits|XData|Model|Serial|Date|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|5000000|0|NORMAL|-0.0005|0.00100000004749745|5e-11|-0.000124999989494356|Second|0|0.400000005960464|6.58411814699916e-06|0.00663679109217515|Volt||MSOS604A|MY55510227|26-Aug-2020  2:32:16|

* Every data file has this data:

|Data|
|---|
|    -596|
|    -720|
|    -904|
|    -960|
|   -1208|
|   -1388|
|   -1116|
|    -744|
|    -588|
|    -496|     
|...|
