# Bonsai repository readme

This folder contains functional Bonsai environments and workflow files for automatic camera acquisition. Associated with various research projects in the Branco and Margrie groups at the Sainsbury Wellcome Centre for Neural Circuits and Behaviour. 

---

## Software dependencies
These should only need to be installed once on a fresh new system, and are not required if simply refreshing the install or deploying to a new folder.

- Windows 10
- [Git for Windows](https://gitforwindows.org/) (recommended for cloning and manipulating this repository)
- [Visual C++ Redistributable for Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30679) (native dependency for OpenCV)
- [Spinnaker SDK 1.29.0.5](https://www.teledynevisionsolutions.com/en-GB/products/spinnaker-sdk/?model=Spinnaker%20SDK&vertical=machine%20vision&segment=iis) (device drivers for FLIR cameras). Install via FLIR website: Download > archive > 1.29.0.5 > SpinnakerSDK_FULL_1.29.0.5_x64.exe

---

## Folder Structure

### `/CrabitatCam`
- Contains workflows designed for daily automatic video camera acqusition of West African fiddler crabs (*Afruca tangeri*) in captive enviroments.
- `/110` subfolder workflows acquire footage from 7:00-19:00, using Logitech Brio 4K webcams.
- `/B2` subfolder films 24/7, with frames synced across four cameras (FLIR BlackFly S) via a HARP Output Expander. Videos and frame metadata are binned by the hour. This acquisition pipeline incorporates some components from the [Aeon project at the Sainsbury Wellcome Centre](https://github.com/SainsburyWellcomeCentre/aeon_acquisition), specifically Aeon.Acquisition Bonsai nodes.

  
### `/Dome`
- This workflow acquries video footage, and syncs TTLS across frames amongst the camera (FLIR BlackFly S) with neuropixel acquisition via a HARP Output Expander. Please reference `DomeData_readme.txt` for quickstart instructions, as the genlock cables have to be connected to the correct outputs.

  
### `/Robocopy`
- Backup .bat scripts for the Bonsai workflows within `/CrabitatCam`, specific to the relevant desktop (i.e., 110_tank+tub.bat corresponds to output file paths within `/CrabitatCam/110`)

- ---

## Contact

For questions or collaboration, please contact sannatitus@yahoo.com

| Last updated by Sanna Titus, sannatitus@yahoo.com, June 2025 
