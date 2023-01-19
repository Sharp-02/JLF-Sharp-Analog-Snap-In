# Sharp Analog Snap-In Mod
### A full analog addition to the Sanwa JLF that replaces your lever's restrictor gate
> Picture of lever from below



# Features
- Full analog range from 0V-3.3V for Joystick X and Y
- Drop-in modification for easy installation
- Designed for fully 3D-Printable mechanical assembly
- Maintains original digital signals for both D-Pad and 
- Low profile and doesn't add much height to the stock joystick assembly
- No potentiometers that wear down with usage
- Linear hall effect sensors with sliding magnet mounts
- Dedicated space for "Snapback Filtering"
- Custom PCB for footprint and consistent reproduction


#Overview
This project is a mod that snaps onto a Sanwa JLF lever. The Sanwa JLF is a very widespread and easily obtainable lever. However, this lever, like most others on the market, has only digital inputs. This means that you can press up, down, left, and right, but you can't lightly move in one direction. You would want this functionality in games such as Super Smash Brothers, where analog inputs are needed for different inputs and actions. 
The Sharp Analog Snap-In creates this functionality. By measuring the position of the bottom of the lever, it outputs an analog voltage that can connect to most controller boards (boards that have 3.3V logic). To do this, the mod mounts magnets that move with the lever, and measures their location through a linear hall-effect sensor. This sensor outputs a voltage, which is amplified to match the 0V-3.3V range that most controllers use. *This does not use a microcontroller, and cannot be programmed.* A lack of programmability is desireable for cases such as tournament use or for simple implementations. By having no programming, the output is a direct relationship to the lever position and cannot "correct" itself automatically.
*For it's main purpose, this is just a lever that can replace a thumbstick/analog input.*



# Assembly and Installation
The mod is implemented by replacing the restrictor gate of the Sanwa JLF with a custom restrictor gate assembly. In this assembly are the base custom restrictor gate replacement, control PCB with the hall-effect sensors, slider arms that follow the lever's position, and the shroud to maintain the motion of the slider arms.

## Electronics
Components:

- DRV5053 Linear Hall Effect Sensors (x2)
- TLC2254 Op-Amp (x1)
- 0603 SMD resistors (xxx Value and xxx Value)
- THT Trimpots (xxx Value and xxx Value)
- 90 degree JST PH 4 position connector
- PCB

PCB:
On the PCB are the hall-effect sensors that measure the lever position, as well as potentiometers that determine the offset and voltage swing of the individual X and Y axes. All references to the "front" of the PCB refer to the side with arrows and values printed on, and is the side that most components solder to. The "rear" is the opposite side, with only the op-amp soldered on it. Inspect the PCB for any manufacturing errors that affect the copper traces near the outer edges and inner ring. Note that the PCB has SMD solder connections on both its front and rear.

Hall-Effect Sensors:
This modification uses DRV5053CAQLPGM Linear Hall Effect Sensors to measure position of the lever. The DRV5053 sensors used are in a TO-92 package, not the SOT-23 package. These sensors must mount facing the arrows on the PCB. Once soldered, the outstanding legs on the opposite side of the PCB must be trimmed flush. 

Trimpots:
The trimpots are used to alter the gain and the offset of the output voltage, and are labeled as such. The gain potentiometers adjust how much movement is required to register as a certain position. Adjust this potentiometer if the controller cannot register full motions across the X or the Y axis. The offest potentiometers adjust the center point of the output voltage. If the joystick center drifts off center *or* if the controller can register full motion in one direction but not the opposite (example: 100% left to 80% right), adjust this potentiometer for the required axis. Once soldered, trim the legs below flush to the PCB.

Op-Amp:
The build is tested on the TLC2254 Op-Amp (SMD). This is a rail-to-rail operational amplifier and is the recommended Op-Amp to use for this mod. The op amp serves the purpose of amplifying the voltage from the hall effect sensor and applying an offset through the trimpots as outlined above. Other op-amps *may* work, but are not guaranteed to. 

Connector:
The JST PH connector ***is a 2.0mm pitch, not the US standard 2.54mm pitch***. This connector *must* be a 90 degree connector and must face out and away from the center of the PCB. From the front of the PCB, with the connector oriented to the right, the connector pins are as follows: [V+ (top), GND, Signal Y, Signal X (bottom)]. Once soldered in, trim the legs of the connector flush to the PCB.
> insert diagram of connection order

The PCB assembly can be tested independent of the full assembly with only a magnet. Orient the magnet's north and south poles along the arrow outlined in front of the sensor under testing. The output voltage can be measured and compared to the expected range (typically 0V - 3.3V).


## Mechanical and 3D Printing
The mechanical housing and components are designed for and around additive manufacturing processes, most specifically to consumer grade FDM 3D printers. 

Components: 

- Restrictor Gate Replacement (printed)
- Slider Arms (x2, printed)
- Arm Shroud (printed)
- VALUE x VALUE bar magnet (x2)
- LENGTH M3 screws (x4)

Printed Part Material:
All printed parts are recommended to be printed in Nylon. All parts will undergo a sliding/rubbing motion, and any friction will result in less ideal movements of the lever. If resin printing is available, it is a good alternative. The assembly works fine with PLA/ABS as well, but may require more post processing and frequent application of a dry lubricant.

Restrictor Gate Replacement:
The restrictor gate replacement is the base of the SASI. It houses the PCB, mounts onto the JLF, and acts as it's own restrictor gate. The restrictor gate's shape alters the movement of the stick and limits the shape that it can move along. For example, Gamecube Controllers have an *octagonal gate*, whereas the Pro Controller and Xbox Controllers have a *circle gate*. Which you use is simply a matter of preference. The files contain multiple gate shapes to be used. 
> footnote: For those interested in implementing controller notches, it may be more difficult to let the stick "lock" into a notch, as the shaft is wide and has a long area that it can slide along.

Slider Arms:
Two slider arms must be printed ***as mirrors of one another***. This allows them to overlap in the center. In ***only one side of each arm***, insert a magnet and push it until the magnet cannot go any further. When testing, you may find that the magnet direction must be flipped. Keep this in mind before pushing in too tight or if no tools are available to extract the magnet from the arm (i.e. another stronger magnet). ***TEST THIS BEFORE ASSEMBLY***
If printing in Nylon or another warp-prone material, use the Slider Arm with Brim file, which limits the warping on the small arms.

## Assembly

## Installation

## Problems and Troubleshooting
