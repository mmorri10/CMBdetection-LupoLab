# CMBdetection-LupoLab
This public repository contains a user-guided tool for semi-automated cerebral microbleed detection and volume segmentation.
The algorithm was developed by Dr. Janine Lupo's group in the Department of Radiology and Biomedical Imaging at the University of California San Francisco. 

The algorithm initiates with a Fast Radial Symmetry Transform (FRST) to detect all putative CMB candidates (note: the transform has been modified to detect dark lesion on a light background). Each candidate then undergoes region growing, and hand-crafted features (e.g. circularity, size, centroid shift) are used to discriminate true CMBs from false positives. While this removes many false positives, a handful still remain at this stage.

The remaining candidates are then segmented using a local thresholding technique to quantify individual volumes, and further classify CMBs into one of three categories: 1) A CMB belonging to a single slice, 2) A traveling CMB, or otherwise 3) A possible true CMB or hard mimic. These categories will aid the user in classifying the candidate CMBs in the next step, and are of interest with respect to reporting CMB characteristics.

In the final step, the user is visually presented, one-by-one, with a candidate CMB (and a description of the category they fall under), and asked to classify the candidate as a true CMB or false positive using 'y' and 'n' keyboard responses. The user can also use scrolling to move through the image slices and/or zoom by clicking and simultaneously dragging the mouse upward or downward.

# AUTHORS/CONTRIBUTORS:
Melanie A Morrison, Seyedmehdi Payabvash, Yicheng Chen, Sivakami Avadiappan, Mihir Shah, Xiaowei Zou, Christopher P Hess, Janine M Lupo

# REVELANT PUBLICATIONS:
Bian et al. 2013 NeuroImage:Clinical 2:282–290 - describes original detection algorithm 

Morrison et al. 2018 NeuroImage:Clinical 20:498-505 - extension of Bian et al. to a user-guided tool with segementation capabilities *latest version of algorithm*

# INPUT: 
The algorithm accepts a single, non-projected volumetric T2*-weighted or SWI dataset in NIFTI format (.nii). 
A file with input parameters called cmb_threshold is also required. This file is included; a detailed description of each parameter can be found in Bian et al. 2013.

# OUTPUT: 
Primary outputs include:

a) scaled_[rootName].nii – image scaled to [0,255]

b) FRST_map_masked[rootName].nii – cmb candidates after FRST

c) FRST_Vessel_mask[rootName].nii – mask of vessels 

d) cmb[rootName].nii – cmb candidates after region growing 

e)  nonproj_cmbseg_v5_thresdeg2x5final_usercorrected[rootName].nii – *final cmb candidates*

f) nonproj_cmbseg_v5_thresdeg2x5denoised[rootName].nii – all cmb candidates automatically removed at denoising stage

g)  nonproj_cmbseg_v5_thresdeg2x5false_positives[rootName].nii – all cmb candidates manually removed as false positives by the user

h) result_[rootName].txt – a text file containing all cmb counts and cmb volumes
   
# FORMAT: 
MATLAB Protected Files 

# USAGE: 
cmb_detection('input file','path to cmb_threshold parameter file in directory','diagnostics flag','semi-automatic detection flag');

e.g. 
cmb_detection(‘test_swi.nii’, ‘/yourPath/cmb_detection_2018_nifti_protected’, ‘diagoff’, ‘semion’);

*When diagoff, the script runs faster and does not produce intermediate files for optimization purposes.

*When semion, the user-guided classification is enabled.

Note: Please use MATLAB version(s) R2017+ for full functionality (i.e. slice scroll, window zoom) of the user-guided GUI. 

# PERFORMANCE: 
The algorithm was optimized on a 7T SWI dataset acquired from 10 adult brain tumor patients with radiological evidence of CMBs following radiation therapy. The overall sensitivity is 86.7%. Performance measures will vary with user classification outcomes.

# TEST SET: 
A test set has been included in this repository. This includes 10 SWI datasets with radiotherapy-induced cerebral microbleed. Five were acquired on a 3T GE system (P01-P05), the other 5 were acquired on a 7T GE system (P06-P10).

# USER SUPPORT:
Melanie A. Morrison 
E: melanie.morrison@ucsf.edu, melanie.morrison@hotmail.com
