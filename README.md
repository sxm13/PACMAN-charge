<h1 align="center">PACMAN</h1>

<h4 align="center">

</h4>              

A **P**artial **A**tomic **C**harge Predicter for Porous **Ma**terials based on Graph Convolutional Neural **N**etwork (**PACMAN**)

- DDEC6 ([1](https://doi.org/10.1039/C6RA04656H), [2](https://doi.org/10.1039/C6RA05507A), [3](https://doi.org/10.1039/C7RA07400J), [4](https://doi.org/10.1039/C7RA11829E)), [Bader](https://doi.org/10.1021/jp0482666), [Charge Model 5 (CM5)](https://doi.org/10.1021/ct200866d), [REPEAT](https://doi.org/10.1021/ct9003405) for metal-organic frameworks (MOFs)
- DDEC6 for covalent-organic frameworks (COFs)


[![Requires Python 3.9](https://img.shields.io/badge/Python-3.9-blue.svg?logo=python&logoColor=white)](https://python.org/downloads)[![PyPI version](https://badge.fury.io/py/pyEQL.svg)](https://pypi.org/project/PACMAN-charge/) [![Zenodo](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.10822403-blue)](https://doi.org/10.5281/zenodo.10822403)  [![MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/sxm13/PACMAN/LICENSE.txt) [![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sxmzhaogb@gmail.com) [![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)]() [![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)]()          

**Developed by:** [Guobin Zhao](https://github.com/sxm13)

# Installation                             
                                 
**[pip](https://pypi.org/project/PACMAN-charge/)**                                                              

```sh
pip install PACMAN-charge
```

**Git clone**                          

```sh
git clone https://github.com/mtap-research/PACMAN-charge.git
cd PACMAN-charge
pip install -r requirements.txt
```                            
         
# How to Use PACMAN charge               
           
**Jupyter notebook (using pip)**                      
                
```sh      
from PACMANCharge import pmcharge
pmcharge.predict(cif_file="./test/Cu-BTC.cif",charge_type="DDEC6",digits=10,atom_type=True,neutral=True,keep_connect=True)

```                                                               
                                  
**Terminal**
```sh
python pmcharge.py folder-name[path] --charge_type[DDEC6/Bader/CM5/REPEAT] --digits[int] --atom_type[bool] --neutral[bool] --keep_connect[bool]
```
**Example command:** ```python pmcharge.py test_file/test-1/ --charge_type DDEC6 --digits 10```                                                    

**Help usage information:** ```python pmcharge.py -h```                                     

* folder-name: relative path to a folder with cif files without partial atomic charges                            
* charge-type (default: DDEC6): DDEC6, Bader, CM5 or REPEAT
* digits (default: 6): number of decimal places to print for partial atomic charges. ML models were trained on a 6-digit dataset                                                    
* atom-type (default: True): Default is to keep the same partial atomic charge for the same atom types (based on the similarity of partial atomic charges up to 3 decimal places)                    
* neutral (default: True): Default is to keep the net charge is zero. We use "mean" method to neuralize the system where the excess charges are equally distributed across all atoms              
* keep_connect (default: True): Retain the atomic and connection information (such as _atom_site_adp_type, bond) for the structure             

# Website & Zenodo
* Predict partial atomic charges using an online APP :point_right: [link](https://pacman-charge-mtap.streamlit.app/)
* Full code and dataset can be downloaded from :point_right: [link](https://zenodo.org/records/10822403)
* Note: All future releases will be uploaded on Github and pip only

# Reference
If you use PACMAN charge, please consider citing [this paper](https://pubs.acs.org/doi/10.1021/acs.jctc.4c00434):
```bib
@article{,
    title={PACMAN: A Robust Partial Atomic Charge Predicter for Nanoporous Materials based on Crystal Graph Convolution Network},
    DOI={10.1021/acs.jctc.4c00434},
    journal={Journal of Chemical Theory and Computation},
    author={Zhao, Guobin and Chung, Yongchul},
    year={2024},
    volume = {20},
    number = {12},
    pages={5368-5380}
}
```

| Databases with partial atomic charges                                                                                                                                      | url                                                                                                                                        | size                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QMOF | [link](https://github.com/Andrew-S-Rosen/QMOF) | 16,779 |
| CoRE MOF 2014 DDEC | [link](https://zenodo.org/records/3986573#.XzfKiJMzY8N) | 2,932 |
| CoRE MOF 2014 DFT-optimized | [link](https://zenodo.org/records/3986569#.XzfKcpMzY8N) | 502 | 
| CURATED-COFs | [link](https://github.com/danieleongari/CURATED-COFs) | 612 |
| ARC-MOF | [link](https://zenodo.org/records/10818822) | 279,118 |                                         


# Bugs and Issues

 If you encounter any problem during using **PACMAN**, please email ```sxmzhaogb@gmail.com``` or create "issues"

 
# Repository Structures

#### Model Architecture            
<img src="./figs/workflow.png" alt="workflow" width="500">             


### Directory Organization
```
.
├── ..
├── figs                                                # Figures used for introduction 
│   ├── toc.jpg                                         # Table of Contents
│   └── workflow.png                                    # Workflow of this project
│
├── model                                               # Python files used for dataset prepartion & GCN training
│   ├── GCN_E.py                                        # Networks model for energy/bandgap training
│   ├── GCN_charge.py                                   # Networks model for atomic charge training
│   ├── cif2data.py                                     # Convert QMOF database to dataset
│   ├── data_E.py                                       # Convert cif to graph & target (energy/bandgap)
│   ├── data_charge.py                                  # Convert cif to graph & target (atomic charge)
│   └── utils.py                                        # Normalizer, sampling, AverageMeter, save_checkpoint
│
├── model4pre                                           # Python files used for prediction
│   ├── GCN_E.py                                        # Networks model for energy/bandgap prediction
│   ├── GCN_charge.py                                   # Networks model for atomic charge prediction
│   ├── atom_init.json                                  # a JSON file that stores the initialization vector for each element
│   ├── cif2data.py                                     # Read/write cif file
│   ├── data.py                                         # Convert cif to graph & target (energy/bandgap)
│   ├── data_charge.py                                  # Convert cif to graph & target (atomic charge)
│   └── utils.py                                        # Normalizer, sampling, AverageMeter, save_checkpoint
│
├── pth                                                 # Models of this project
│   ├── best_bader                                      # Bader
│   │   ├── bader.pth                                   # Bader charge model
│   │   └── normalizer-bader.pkl                        # Normalizer of bandgap
│   ├── best_bandgap                                    # Bandgap
│   │   ├── bandgap.pth                                 # Bandgap model
│   │   └── normalizer-bandgap.pkl                      # Normalizer of bandgap
│   ├── best_cm5                                        # CM5
│   │   ├── bandgap.pth                                 # ///
│   │   └── normalizer-bandgap.pkl                      # ///
│   ├── best_ddec                                       # ///
│   │   ├── ddec.pth                                    # ///
│   │   └── normalizer-ddec.pkl                         # ///
│   ├── best_pbe                                        # ///
│   │   ├── pbe-atom.pth                                # ///
│   │   └── normalizer-pbe.pkl                          # ///
│   ├── best_repeat                                     # ///
│   │   ├── repeat.pth                                  # ///
│   │   └── normalizer-repeat.pkl                       # ///
│   ├── chk_bader                                       # Bader
│   │   └── checkpoint.pth                              # Checkpoint of bader
│   ├── chk_bandgap                                     # Bandgap
│   │   └── checkpoint.pth                              # Checkpoint of bandgap
│   ├── chk_cm5                                         # CM5
│   │   └── checkpoint.pth                              # ///
│   ├── chk_ddec                                        # ///
│   │   └── checkpoint.pth                              # ///
│   ├── chk_pbe                                         # ///
│   │   └── checkpoint.pth                              # ///
│   └── chk_repeat                                      # ///
│       └── checkpoint.pth                              # ///
│
├── pmcharge.py                                         # main python file for atomic charge assignment by command line
├── LICENSE.txt                                         # MIT license
├── README.md                                           # Usage/Source
├── requirements.txt                                    # packages need to be installed
├── train_E.py                                          # main python file for energy/bandgap training
└── train_charge.py                                     # main python file for atomic charge training

```

# Supported elements                                                                  
(Elements that have been used by the model training process, not all the elements contained in the database)

*  DDEC6/CM5/Bader Charges                                                              
<img src="./figs/Element_QMOF.png" alt="QMOF-Element" width="500">                                       

*  REPEAT Charges                                                                                                
<img src="./figs/Element_ARC-MOF.png" alt="ARC-MOF-Element" width="500">                        

                                                           
# Models Performance                                    
*  DDEC6 Charges                                            
Parity plot of partial atomic charges from DDEC6 and PACMAN on the test set (QMOF).                         
<img src="./figs/DDEC6.png" alt="DDEC6" width="500">                                       

*  CM5 Charges                       
Parity plot of partial atomic charges CM5 and PACMAN on the test set (QMOF).                             
<img src="./figs/CM5.png" alt="CM5" width="500">                                       

*  Bader Charges                            
Parity plot of partial atomic charges from Bader and PACMAN on the test set (QMOF).                                       
For the Bader model, use caution with Th-MOF predictions due to just 2 points used in traning set. The big error shows in the below figure is `Th`.                        
<img src="./figs/Bader.png" alt="Bader" width="500">                                       

*  REPEAT Charges                              
Parity plot of partial atomic charges from REPEAT and PACMAN on the test set (ARC-MOF). 
<img src="./figs/REPEAT.png" alt="REPEAT" width="500">                                       


                    
## AUTHORS

### Maintainer
* Guobin Zhao (sxmzhaogb@gmail.com)

### Project Contributors
* Guobin Zhao (sxmzhaogb@gmail.com): models, training, data preparation
* Yongchul G. Chung (drygchung@gmail.com): supervising



 
