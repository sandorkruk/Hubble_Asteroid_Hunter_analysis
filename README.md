# Analysis of the Hubble Asteroid Hunter citizen science project www.asteroidhunter.org

The Zooniverse project ran between 21-07-2019 to 12-08-2019, with a total of 10,874 images, 293,319 classifications and 1,923 volunteers participating in the project. The statistics of the project can be seen at https://www.zooniverse.org/projects/sandorkruk/hubble-asteroid-hunter/stats. 

The HST images were split into two subject sets: 

a) 3,741 images based on predicted asteroid positions from the ESA **SSO pipeline**. These images were shown to the volunteers with the predicted positions of the asteroid trails marked with green circles. The images were taken with the ACS, WFC3, and WFPC2 instruments. The retirement limit of the images was N=40.

b) 7,133 images based on **blind** HST fields within 10 degress of the ecliptic plane. These were blank images taken with the ACS and WFC3 instruments, without marked positions. The retirement limit of the images was N=20. 

The workflow of the project had four tasks:
T0 - Q: Is there an asteroid trail visible in the images? A: Yes / No / Impossible-to-tell
T1 - Mark the beginning and end position of the asteroid trail in the image.
T2 - Q: Is there any other asteroid trail visible in the image? A: Yes / No
T3 - Mark the beginning and end position of the other asteroid trail in the image.

Subsequently, the analysis is split into the two subject sets. The individual markings were aggregated into clusters with the HDBSCAN ML algorithm (https://hdbscan.readthedocs.io/en/latest/), with the parameters (min_cluster_size: 10, min_samples: 5 for the SSO pipeline) and (min_cluster_size: 5, min_samples: 5 for the blind images). 

The classifications and aggregated answers and markings are given in the files: 
*asteroid_SSO_classifications_markings.csv*
*asteroid_blind_classifications_markings.csv*

The two Jupyter notebooks show the analysis of the classifications and markings for the two subject sets, separately. 
The images that were used in the project can be found on the Google Drive: https://drive.google.com/open?id=1WMAj9lDTNxU83W7WokZQFKdGpMdgm037 or online on Zooniverse, in the field indicated in the csv tables.
_______________________________________________________________________________________________________________________

Results: 

We used a threshold of p_yes>0.3 to select images with asteroids to inspect. 

In the **SSO pipeline** dataset, after cleaning the classifications, 1333 images were identified as having asteroids (35.6% of the images). The classifications are accurate (>95%) for the ACS and WFC3 images, while for WFPC2 it is fairly low (False positive rate ~50%), due to CR trails being misclassified as asteroids. 

In the **blind** images, after clearning the classifications, 468 images are identified as having asteroids (6.6% of the images). For this dataset, the false positive rate is quite high, ~50%, probably due to the lack of guidance from the green markers. Common misclassifications: gravitational lensing (26), edge-on galaxies (18), quasar jets (6), stellar diffraction spike (71), cosmic rays (359) and image artefacts (72). 
