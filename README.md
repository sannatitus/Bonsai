# Bonsai repo readme

This folder contains functional Bonsai environments and workflow files for automatic camera acquisition. 

---

## Folder Structure
- 
### `/CrabitatCam`
- Contains workflows designed for daily automatic video camera acqusition of West African fiddler crabs (*Afruca tangeri*) in captive enviroments.
- `/110` subfolder workflows acquire footage from 7:00-19:00, using Logitech Brio 4K webcams.
- `/B2` subfolder films 24/7, with frames synced across four cameras (FLIR BlackFly S) via a HARP Output Expander. Videos and frame metadata are binned by the hour. This acquisition pipeline incorporates some components from the Aeon project at the Sainsbury Wellcome Centre, specfically Aeon.Aquisitiion nodes.

- 
### `/Dome`
- This workflow acquries video footage, and syncs TTLS across frames amongst the camera (FLIR BlackFly S) with neuropixel acquisition via a HARP Output Expander. Please reference `DomeData_readme.txt` for quickstart instructions, as the genlock cables have to be connected to the correct outputs.

- 
### `/Robocopy`
- Backup .bat scripts for the Bonsai workflows within `/CrabitatCam`, specific to the relevant desktop (i.e., 110_tank+tub.bat corresponds to output file paths within `/CrabitatCam/110`)

- ---

## Contact

For questions or collaboration, please contact sannatitus@yahoo.com

| Last updated by Sanna Titus, sannatitus@yahoo.com, June 2025 
