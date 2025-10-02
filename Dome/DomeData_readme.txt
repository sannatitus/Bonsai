# DomeData acquisition readme (Bonsai, HARP TTL, camera and neuropixel acquisition + data transfer) | last updated by Sanna, 1/10/25 s.titus@ucl.ac.uk

## This readme is identical across the following platforms, please reupload the document across these if any changes occur: 
- ceph Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments (and shortcut to this available in ceph Z:\raw\CrabLab\Bonsai\110-Dome) 
- 110-Dome desktop C:\Users\110-dome\Desktop\bonsai
- Google drive (Crabitat_photos\Afruca-tangeri_crabitat\Bonsai) 
- github https://github.com/sannatitus/Bonsai/tree/c65d48e328033ab44e8f85aaca8f4040032067fd/Dome 

-----------------------------------------------------------------------------------------------------

## QUICKSTART INSTRUCTIONS (For further details, reference sections below) 
1. Ensure hardware connections to the HARP Output Expander are as follows: Out0 = neuropixel, Out1 = FLIR camera (i.e., the one with WAGO connectors). If required, a picture of this is stored in the ceph at Z:\raw\CrabLab\Bonsai\110-Dome\harp-hardware_Out0neuropixel-Out1FLIR.png
2. On the 110-crab desktop, begin playing the desired dome video via KommanderZ1 software 
3. On the remote desktop station, initiate neuropixel acquisition 
4. On the 110-dome desktop, open the bonsai application at C:\Users\110-dome\Desktop\bonsai\DomeData_harp+camera+neuropixel\.bonsai\bonsai
5. Subsequent directions are all on the 110-dome desktop unless otherwise stated; in this Bonsai window, open the 'DomeData.bonsai' workflow (stored in C:\Users\110-dome\Desktop\bonsai\DomeData_harp+camera+neuropixel\workflows\DomeData.bonsai) 
6. Hit the green start arrow (this initiates the TTL signaling from the HARP output expander, a small diaglogue box should pop up in Bonsai that changes every few seconds. If this does not automatically show up, you can view it by double clicking VideoController group node and then double clicking StartOutputExpander. The TTL signals should also be visible on the neuropixel remote desktop station). 
7. On the keyboard, hold SHIFT+F1 (this iniates the camera acquisition, a small window should show up with the view. If not, double click the blue Value.Image node)

8. Acquire data for as long as you want! Camera and TTL data will be saved on an hourly basis to 110-dome desktop's D:\DomeData\<acquisition timestamp binned by parent hour>\ (neuropixel data should be saving on the remote station as described in step 3). 

9. When finished, stop the Bonsai workflow with the red square. Ensure you upload the data to ceph from BOTH desktops. On the 110-dome desktop, double click the script stored as D:\robocopy-script_dome.bat . On the remote desktop station with the neuropixel data, please upload everything to the ceph at Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\<acquisition timestamp binned by parent hour>\neuropixel .

-----------------------------------------------------------------------------------------------------

## CEPH TRANSFER - The robocopy-script_dome.bat is a batch script that uploads the dome data (aquired with Bonsai, i.e., the TTL signal omitted from the Harp Output Expander that can be used to sync the camera with the neuropixel data) within D:\DomeData\ to the ceph, at Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData continuously. The ceph must be mounted to drive letter Z:\ in order for this to work. This is run locally from the 110-Dome desktop. Transfer success is monitored on 110-Dome's D:\robocopy-log. If the script ever spontaneously ceases, it can be restarted by double clicking on 110-Dome's local version of D:\robocopy-script_dome.bat

-----------------------------------------------------------------------------------------------------

## POST-ACQUISITION TTL ALIGNMENT - After acquiring behavioural data in the dome, and uploading the 110-dome desktop data (from Bonsai to ceph via the D:\robocopy-script_dome.bat) plus the neuropixel remote acquisition desktop data (neuropixel data to the ceph), one must employ a python script to align the TTL signals with the video + neuropixel data. The way the TTL signal works in our Bonsai pipeline is that every 8-16 seconds, a 100ms TTL signal is sent to the camera and neuropixel. The timing in between these signals is always unique so that alignment post-acquisition can happen at any point throughout any data. There is one .bin file for each TTL signal (stored in D:\DomeData\<acquisition timestamp binned by parent hour>\TTL, which should have already been uploaded to the ceph at Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\<acquisition timestamp binned by parent hour>\TTL from the aforementioned .bat script). Each TTL signal is described uniquely from the harp-tech/device.outputexpander/device.yml file available in github at: https://github.com/harp-tech/device.outputexpander/blob/main/device.yml . For post-acquisition alignment, follow harp-tech's harp-python script available at: https://harp-tech.org/articles/python.html . 

### This python script environment has been setup on the 110-dome and SannaDesk desktops. To run this post-acquisition alignment via the python script, copy the device.yaml file into the TTL folder of the relevant experiment (stored within the ceph, at \zoo\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData or download from the aforementioned https://github.com/harp-tech/device.outputexpander/blob/main/device.yml ). 

On 110-dome, open cmd (with administrator priviledges) and type mamba activate harp-python 
On SannaDesk, open cmd and type conda activate harp-python 

python 
import harp
reader = harp.create_reader("device.harp") ####currently we are stuck here!  I recieve the following error regardless of the file paths attempted (~~~below).    
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
>>> reader.OperationControl.read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: _compose_parser.<locals>.parser() missing 1 required positional argument: 'data'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ attempted file paths: 
reader = harp.create_reader(r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\"
reader = harp.create_reader(r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL"
reader = harp.create_reader(r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\device.yml"
reader = harp.create_reader(r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\device.harp" #where I renamed the device.yml to device.harp
reader = harp.create_reader(harp_path) #when harp_path = below options 
harp_path = r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL" 
harp_path = r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\" 
harp_path = r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\device.yml" 
harp_path = r"Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL\device.harp" 

# Andre was chasing this up for us but hasn't gotten back to us. You could also attempt the following: 
# before conda activate harp-python environment, cd into Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26 then
import harp
reader = harp.create_reader("TTL")

# before conda activate harp-python environment, cd into Z:\raw\CrabLab\Behaviour\LED-arena_110\experiments\DomeData\2025-03-20T15-55-26\TTL then
import harp
reader = harp.create_reader("device.yml")
reader = harp.create_reader("device.harp")

#It might be worth considering recording keypress events in Kommander.Z1 and align it with the TTL to associate loom initiation with neural data. 
