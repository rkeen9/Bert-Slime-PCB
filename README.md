# Bert-Slime-Tracker
**DOES NOT WORK YET.** If you build this, you will get a non-functional tracker. This repository will be updated once troubleshooting is complete.

Another slime tracker. This one was designed for small form factor and easy DIY that involves minimal soldering and easily obtainable parts. This is essentially just an ICM-45686 breakout board which you can install a D1 mini directly to via 2x8 port 2.54 mm female headers. A TP-4056 charger module can also be installed directly to the board via 2.54mm male headers. Assembly instructions to come once this project is functional.

# Folder Structure 
- **Bert-Slime-Tracker/** Main folder. Contains KiCAD project files and all other folders.
- **Bert-Slime-Tracker/Libraries** Contains all custom symbols and footprints used in this project
- **Bert-Slime-Tracker/assembly-files** Contains all files that would be needed to have this project built by JLCPCB (https://jlcpcb.com/).
- **Bert-Slime-Tracker/Schematics** Contains the schematic in PDF form.
- **Bert-Slime-Tracker/Troubleshooting** Contains my efforts to get this project functional :).

# KiCAD Environment Setup
This project was made in KiCAD 9.0. KiCAD is free PCB design software which can be downloaded from https://www.kicad.org/download/. If you are familiar with KiCAD and Github, all you need to know is that the required files for all custom components are in the **Libraries** folder.

If you're new to KiCAD or need a refresher, the following is step by step instructions for opening this project following a fresh KiCAD install:
1. Download this project through GitHub's **Download Zip** option as shown below and extract it to the desired project location:
![github](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/1-github.png)
2. Run KiCAD and open the **Footprint Editor** from the start screen
![Main Screen](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/2a-kicad-main-footprint.png)
Continue with the default options if this popup appears:
![default](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/2b-default.png)
3. From the **Footprint Editor**, Go to **File>Add Library**

![footprint](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/3a-footprint_editor_add.png)

Navigate to where you extracted the project files, select the **Libraries/Bert-Slime-PCB.pretty** folder, and hit **Select Folder**
![pretty file](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/3b-symbol-library-file.png)

4. Exit from the **Footprint Editor** and open the **Symbol Editor** from the KiCAD start screen
![Main Screen](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/4a-symbol_editor_add.png)
Continue with the default options if this popup appears:
![default](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/4b.png)
5. From the **Symbol Editor**, Go to **File>Add Library**
![Symbol](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/5a.png)

Navigate to where you extracted the project files and open the **Libraries/Bert-Slime-PCB.kicad_sym** file.
![Symbol Path](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/5b.png)

6. Exit from the **Symbol Editor** and open the project from the KiCAD start screen as shown:
![Open Proj](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/6a-Open_project.png)

Now navigate to the project folder and open the **bert_slime_tracker.kicad_pro** file
![Open Proj](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/6b-Open_project.png)

7. The project can now be edited in KiCAD. the **bert_slime_tracker.kicad_sch** file contains the project schematics and the **slime_tracker.kicad_pcb** file contains the PCB design itself.

![done](https://github.com/rkeen9/Bert-Slime-Tracker/blob/main/images/environment_setup/7-done.png)
