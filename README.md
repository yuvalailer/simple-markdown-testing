# Crazy Game - User's Guide

Useful markdown links:
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet 
https://github.com/yuvalailer/plant-watering-via-BLE 
Install “Markdown Sidebar” from the: Add-ons -> get Add-ons tab (here, in google docs)  to roughly see how your Markdown will look like. Mind that it looks better in Github


## Introduction  
This project was made as a part of the [“Motion Planning for Robots”](http://acg.cs.tau.ac.il/projects “course website”) workshop in Tel-Aviv University, the department of CS, 2018, under the guidance of [Prof. Dan Halperin
](http://acg.cs.tau.ac.il/danhalperin/homepage ).


In this project, we created a framework for developing games of controlling real world robots in a competition between men and computer players. We also made two games using this framework, that can be played once the system is up. The system was developed with special emphasis on motion planning algorithms, and the games are meant to display the quality of the automated motion, in compercent to the human controlled one.

 We used the **Crazyflie drones**, **Optitrack** motion tracking system and various software (further details later in this document). 


This guide provides the links and instructions for the steps needed in order to set up this project and play the games. The proceeding [Developers Guide](https://github.com/yuvalailer/CrazyFlie/blob/master/README.md ) gives a deeper look into the software we wrote and can be usefull for creating your own games and framworks.

## Watch it in action:
[![](https://github.com/yuvalailer/plant-watering-via-BLE/blob/master/video_image.jpeg)](https://youtu.be/z5ZcZOntGuo)

## Table of Content
#### 1. Installation and Prerequisites 
a. Hardware - OptiTrack, VM, Windows, Peripherals (Joystick, LED)
     
b. Software - Git
#### 2. Crazy Game
a. Capture the Flag  - 2 players (human or machine), fly 2-4 drones in a competition to capture the rival’s flags.
 
b. Catch’em all - 2 players (human or machine), taking turns flying one drone on a mission to capture all the targets in the shortest time.
     
c. How to run the game

#### 3. Thanks and Disclaimer

# Installation and Prerequisites 
## Hardware
This project strongly based on existing optical motion capture system from OptiTrack,
Thus hardware from Optitrack is needed.
- [Flex 3 capture cameras](http://optitrack.com/products/flex-3/) .
There isn’t fixed number of cameras required for the purpose of this project to work. The amount  depend on the the work area size, but in order the system to work at least 3 cameras have to be able to see all infrared markers related to an “rigid object” at any given moment.
We had 6 cameras cover area about 1.5X1.5 meter, 0.5 meter above the ground.
- [Infrared markers](http://optitrack.com/products/motion-capture-markers/)
Optitrack Cameras able to identify object by the reflection of IR li from those IR markers.
For example, 4 markers used for each Crazyflie 2.0 drone, each drone is consider as 1 “rigid object”.
- [Calibration tools](http://optitrack.com/products/tools/). We used CW-500 Calibration Wand Kit for calibrating the cameras and CS-200 Calibration Square to set (X, Y, Z) coordinates directions. Calibration process will be further details later in this document.
- [Hardware key.](http://optitrack.com/products/keys/)
Key is needed for Motive software to work.
- [OptiHub 2.0](http://optitrack.com/products/optihub/)
All cameras connect to OptiHub device that connect to the PC running the VM.
All of those hardware components and software can be bought together in the following link:
[Full system.](http://optitrack.com/cart/?shopurl=http://optitrack.com/systems/)
 

Other required hardware.
- [2/4 Crazyflie 2.0 drones.](https://www.bitcraze.io/crazyflie-2/)
- [Arduino Joystick.](https://store.arduino.cc/grove-thumb-joystick)
- WS2811 Controlled Leds for “Catch Them All” game.
- USB - RF antenna for communicating with Crazyflie drones.


## VM:
The project’s games framework depend on two software environments which one of them is bitcraze virtual machine image contain version of xubuntu-14.04.4 and Ros code, launch file necessary for the system to work. Taken from another project, this Image is unique and need to be download from [here.](https://github.com/bitcraze/bitcraze-vm/releases/).



In addition, VM contain game server-side codes for the game that can be found in CrazyGame VM code repository.



As mentioned before,  VM environment have the role of a server. The main game (on Windows) communicate with the VM over TCP and other code parts in the VM handle the communication with the drones.

## Windows:
The second software environment is Windows 10, contain Motive software and
files related to the game. Those files can be found in CrazyGame for Windows PC - GUI repository (without the motive software).


# Software
## Motive
Motive is a the software used for controlling and processing the information received from the Optitrack cameras set. It is proprietary and requires a license. In Motive, collections of markers, identified by the cameras, are grouped together into trackable ‘rigid bodies’, that represent the location of objects in the real word. In our project, such objects are the Crazyflie Drones and the LEDs. it is very important to follow the next **naming convention** in order to use our system “as is” without changes.
#### For Drones:
- Drone number X will be called **crazyflieX** in Motive (as a ‘rigid body’).
- Its designated MAC address will be **E7E7E7E70X**.

For example: 

    drone 3 will be called **crazyflie3** and have the address **E7E7E7E703**. 
    drone 15 will be called **crazyflie15** and have the address **E7E7E7E715**.

#### For LEDs:
- LED number X will be called **ledX** in Motive (as a ‘rigid body’).

For example: 

    LED 3 will be called **led3**.  
    LED 15 will be called **led15**.

 ## Git
Our project is divided into five different Git repositories. Each one can be used by its own, but of course the parts were built to fit together, and therefore some adjustments will be necessary. In order to install the full framework, follow the steps provided in the installation guide.

### Repositories:
-  [CrazyGame Website](https://github.com/xqgex/CrazyFlie_Website)
- [CrazyGame for Windows PC - GUI](https://github.com/xqgex/CrazyFlie)
- [CrazyGame VM code - Communication with the drones](https://github.com/xqgex/CrazyFlie_ros ) 
- [CrazyGame Arduino code - For joystick and led strips](https://github.com/xqgex/CrazyFlie_Arduino )
- [CrazyGame Automatic player](https://github.com/xqgex/CrazyFlie_Autoplayer )

## Dependencies:
Different parts of the project are made using different inviruments and software dependencies. Best practise of using this project is following the installation guide, on a **Windows** computer strong enough to carry the simultaneous load of the VM and the GUI software, Which means **minimum 8 GB of RAM and virtualization capabilities**.
Alternatively it is possible to use it in other configurations but we don’t offer additional support for it.

## Installation Guide:
Assuming:
- you are using a Windows computer that meets the demands in the dependencies section - that the Optitrack + motive system is installed and ready to go.
- that the Crazyflie antenna dongle is connected

1. Download and install  [Oracle VirtualBox](https://www.virtualbox.org/ ) or alternative VM host software of your choice.
2. Download the [linux kubuntu VM](https://www.virtualbox.org/ ) we supply in our git repository. It is based on the [original Crazyflie project VM](https://wiki.bitcraze.io/projects:virtualmachine:index ). You can move to the next steps while it is downloading. 
3. Install [python 3.6](https://www.python.org/downloads/release/python-366/ ) on the windows PC.
4. Install the needed Python dependencies by opening Windows CMD and typing: 
```
pip install shapely pyserial munch
```
5. Download and Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git ) on the Windows PC. 
6.Clone the Windows-side repository by opening the now installed **Git bash** program, and typing in the command:
```
git clone https://github.com/xqgex/CrazyFlie
```
7. Import the downloaded VM from step 2, in the VM host software from step 1. You can use [this guide](https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html ).
8. Set the following configuration ([How to guide](https://www.virtualbox.org/manual/ch03.html)) for the VM:
At least 4 GB of RAM
Network definitions of: TODO
9. Start the VM, **password is “crazyflie”** 
10. **optional:** if you wish to control the drone using an Arduino Joystick + LED targets, install the [arduino IDE](https://www.arduino.cc/en/Main/Software ), and clone/use the code from the - [CrazyGame Arduino code - For joystick and led strips](https://github.com/xqgex/CrazyFlie_Arduino ) repository.

### You now have all you need to start the game. Move to the “How to run the game” part to start playing! 

  


# Crazy Game
## Capture the Flag  - goal, controls (keyboard), game modes, features (battery, drone safe zone…) 
add relevant screenshots, icons and so on to make this part understandable 

---

## Catch’em all - goal, controls (joystick), game modes, features (LED...)
add relevant screenshots, icons and so on to make this part understandable 

---

## How to run the game 
After downloads all files related to the game both VM and Windows sides and after setting the drones and leds (optional) in Motive software follow those instructions to run the game.
### VM side:
In CrazyFlie_ros/crazyflie_demo/scripts/ folder, enter: 


```
python main.py crazyflie2 crazyflie3 led1 led2
```

Replace “crazyflie2 crazyflie3 led1 led2” with your drones and leds setup in Motive

Then at the same folder, run:

```
python crazyGameVM.py
```

### Windows side:
In /CrazyFlie

```
python crazyGame.py
``` 
Enjoy the game. 











## Thanks and Disclaimer 
We would like to thank Prof. Dan Halperin and the staff of the course for their guidance, Yoni Mendel and the Advanced Control Systems Lab in TAU for hosting and supporting this project. Special Thanks to Yotam Gani and Orel Ben-Yeshai for their support and assistance. 
#### We don't own any IP rights for the software, hardware, internet articles, manuals, images (found on google image search) or any other 3rd party component of this project, which may be subjected to any kind of copyrights. All activities in this project were made for educational purposes only.




