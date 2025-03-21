\zoo\raw\CrabLab\Bonsai\B2Crabitat_24-7_bonsai_readme.txt composed by Sanna (s.titus@ucl.ac.uk) 13 April 2024 

This document provides instructions for how to operate the B2 crabitat's 24/7 bonsai acquisition pipeline. This document is identical to the one stored locally on the B2Crab desktop. Completing all steps will allow videos to be automatically acquired and uploaded to the ceph, at \raw\CrabLab\CrabitatCam_daily. 

If Bonsai acquisition were to cease, please restart the workflow by: 
1. open Bonsai application (desktop folder B2-camera) 
2. load B2Crabitat_24-7.bonsai workflow 
3. hit the green arrow start button 
4. double click the control panel node (this will bring up a blank table, which should show each camera's POV in the subsequent step) 
5. hit keys: shift F1
6. check that the control panel node now shows 4 cameras. this means Bonsai is acquiring sucessfully! The videos are automatically written to D:/B2. If all the cameras do not connect, ensure that SpinView application is not open. If one camera specificially (such as camera 3) does not connect, restart the computer. If any views are washed out, ensure each camera's exposure is set to 12500 (except cam1 serial 9997, who should be set to 10000). 
7. begin the automatic ceph upload pipeline (otherwise the computer will run out of storage space within a couple days); first check the ceph is mounted to the desktop as mount letter Z: (within file explorer, navigate to This PC and it should be marked as green). If the ceph is not connected, right click this pc > map network drive > type \\ceph-gw02.hpc.swc.ucl.ac.uk\zoo > log in via AD\swcusername (insert your swc username here & log in with swc password) 
8. double click the batch file within D:\robocopy-log\robocopy-script.bat - it should bring up a cmd window automatically, and begin to transfer files. ensure no errors are reported, and then minimise the window to leave this running idefinitely in the background. 

This desktop's settings already inhibit sleep (i.e., windows sleep settings = never). Every 30 days*, log into the desktop to pause windows updates as these will spontaneously cause the desktop to restart (thus ceasing the bonsai and automatic upload pipeline). *There is a recurring event within the crabitat outlook calendar reminding to pause updates on every third Monday. 

For further information on acquired videos and an overview of hardware, reference \zoo\raw\CrabLab\CrabitatCam_daily\readme.txt 
For IR light diagrams and camera/HARP setup, reference \zoo\raw\CrabLab\Bonsai\B2-hardware\B2_camera-hardware.png & B2_IR-lights-hardware.png
For blueprints, tide diagrams, light schedules and schematics, reference \raw\CrabLab\Husbandry_SOPs\
Locate zips of relevant programmes in this folder. Note the version of SpinView necessary for Bonsai compatibility. 
