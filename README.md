# Sharp Analog Snap-In (SASI) Mod
### A full analog addition to the Sanwa JLF that replaces your lever's restrictor gate
<img src="https://user-images.githubusercontent.com/86936750/213596998-4c9b40dc-2576-41d1-aef6-5747094e6abe.jpg" width=50% height=50%>



# Features
- Full analog range from 0V-3.3V for Joystick X and Y
- Drop-in modification for easy installation
- Designed for fully 3D-Printable mechanical assembly
- Maintains original digital signals for both D-Pad and 
- Low profile and doesn't add much height to the stock joystick assembly
- No potentiometers that wear down with usage
- Linear hall effect sensors with sliding magnet mounts
- "Snapback Filtering" capability
- Custom PCB for footprint and consistent reproduction


# Overview
The Sharp Analog Snap-In, or SASI (pronounced "sassy"), adds analog functionality to the pre-existing Sanwa JLF lever. By measuring the position of the bottom of the lever, it outputs an analog voltage that can connect to most controller boards (boards that have 3.3V logic). To do this, the mod mounts magnets that move with the lever, and measures their location through a linear hall-effect sensor. This sensor outputs a voltage, which is amplified to match the 0V-3.3V range that most controllers use. *This does not use a microcontroller, and cannot be programmed.* A lack of programmability is desireable for cases such as tournament use or for simple implementations. By having no programming, the output is a direct relationship to the lever position and cannot "correct" itself automatically.
*For it's main purpose, this is just a lever that can replace a thumbstick/analog input.*

# Analog vs. Digital

The SASI mod snaps onto a Sanwa JLF lever. The Sanwa JLF is a very widespread and easily obtainable lever. However, this lever, like most others on the market, has only digital inputs. A digital input has only on or off states, nothing in between. In practice, this means that you can press up, down, left, and right, but you can't lightly move in one direction. This works well for most fighting games, as there is no change in movement speed depending on how far you press in a direction.

An analog system, on the other hand, does not have only discreet on/off states. Rather, you are able to be somewhere in the middle, maybe at 70% the maximum, or 22%, or whatever resolution your device gives you. For gaming, the SASI mod would allow you to gently move into a direction, or move at a specific angle.
You would want this light movement functionality in games such as Super Smash Brothers, where analog inputs are needed for different inputs and actions, or Mario Kart, where adjustments might be made with very slight movements.

What this is NOT is an analog-to-digital system like the programmable Magenta lever by Paradise Arcade. The Magenta lever acts by measuring an analog distance and setting a threshold upon which to count as a "button press". This mod, though it does not remove button press functionality, does not output any button press commands.


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

### PCB:
The PCB (printed circuit board) mounts and connects all the electronics. It is shaped after the Sanwa JLF's PCB that mounts the digital switches. On the PCB are the hall-effect sensors that measure the lever position, as well as potentiometers that determine the offset and voltage swing of the individual X and Y axes. All references to the **"front"** of the PCB refer to the side with arrows and values printed on, and is the side that most components solder to. The **"rear"** is the opposite side, with only the op-amp soldered on it. Inspect the PCB for any manufacturing errors that affect the copper traces near the outer edges and inner ring. Note that the PCB has SMD solder connections on both its front and rear.
> insert image of two PCBs

Left: Front side of PCB; Right: Rear side of PCB

### Hall-Effect Sensors:
This modification uses DRV5053CAQLPG Linear Hall Effect Sensors to measure position of the lever. 

The purpose of the hall effect sensor is to measure the strength of the magnetic field and output a signal. The "hall effect" described makes use of the property of flowing electrons to have an induced force in the presence of a magnetic field, otherwise known as the Lorentz Force. The hall effect is an extrapolation of this force, wherein a current within a magnetic field (measured in Tesla) will "bend" as a funcion of the Lorentz force and accumulate charges in a conductor or semiconductor.

There are primarily two types of hall effect sensors seen in use today- the Hall Switch, and the Linear Hall Sensor. The SASI mod uses a Linear Hall Effect sensor, which outputs a voltage relative to the strength of the magnetic field. The sensor used is the DRV5053 whose pins when viewed from the front, from left to right, are: Vcc, GND, and Vout. The "CA" designation indicates that the sensor outputs a voltage of +23mV/mT. The "Q" designation denotes that the temperature range of the sensor is from -40 C to 125 C. The "LPG" designation indicates the TO-92 package type.

The DRV5053 sensors used are in a TO-92  package (through hole), ***not*** the SOT-23 package (surface mount). These sensors must be soldered on facing the arrows on the PCB. Once soldered, the outstanding legs on the opposite side of the PCB must be trimmed flush. 

As the magnet moves along the arrows in front of the sensor, the magnetic field either grows or lessens, depending on which pole is approaching the sensor. This means that, as the magnets are moved by the stick, the sensor will output a voltage depending on the position of the magnet. In testing, the sensor outputs a range from ~1.2V to ~2.2V. [^PCBTest]


### Op-Amp:
The build is tested on and utilizes the TLC2254 Op-Amp (SMD). This is a rail-to-rail operational amplifier and is the recommended Op-Amp to use for this mod. 

The op-amp serves the purpose of amplifying the voltage from the hall effect sensor and applying an offset through the trimpots as outlined below. Other op-amps *may* work, but are not guaranteed to. 

The op-amp is capable of applying a "gain" to an input voltage, which can be summarized as a direct multiplication. A gain of 2 multiplies the input voltage by 2, and a gain of 4.3 multiplies the input voltage by 4.3. The SASI uses the op-amp to multiply the sensor voltage (range of ~1V) to match the voltage range expected by most controllers and controller boards (3.3V). This gain is altered by the relationship of resistors between the op-amps voltage output, voltage input, and ground. On the SASI mod, this can be tuned by turning the GAIN potetionmeters.

The op-amp is also capable of applying an "offset" to an input voltage, or an addition/subtraction of voltage level. As the hall-effect sensors will not output voltages starting at 0V, a "negative offset" must be applied to the sensor's voltage such that the final output voltage is reduced with the lowest output voltage of the mod being 0V. This is tuned by the OFFSET/OFF potentiometers.

<img src="https://user-images.githubusercontent.com/86936750/213602997-d2bbb199-a96c-480d-9b60-aace56eddf23.png" width=50% height=50%>

What the op-amp ***does not do*** is read the input voltage and determine an output voltage or signal like a microcontroller would. Op-amps are not "programmable" in the traditional sense that microcontrollers are. Microcontrollers are capable of more complex interpretations of data, and can perform operations that allow for perfect inputs and timing. Because the op-amp works purely off the analog voltages and circuit design, it cannot be exploited in this manner.

### Trimpots:
The trimmer potentiometers, or trimpots, are a type of potentiometer that often come with multi-turn capability at varying levels of precision. Potentiometers are used as a variable resistor, or as a way to connect in the "middle" of a resistor. These properties are utilized in the op-amp circuit shown above.

<img src="https://user-images.githubusercontent.com/86936750/213603990-a4ba95ef-5618-4205-b9c7-d5fd71642baf.jpg" width=30% height=30%>

These trimpots are used to alter the gain (YPOTGAIN, XPOTGAIN) and the offset (YPOTOFF, XPOTOFF) of the output voltage, and are labeled as such. The gain potentiometers adjust how much movement is required to register as a certain position. **This potentiometer requires a value of 50k**. Adjust this potentiometer if the controller cannot register full motions across the X or the Y axis. The offest potentiometers adjust the center point of the output voltage. **This potentiometer requires a value of 10k*. If the joystick center drifts off center *or* if the controller can register full motion in one direction but not the opposite (example: 100% left to 80% right), adjust this potentiometer for the required axis. Once soldered, trim the legs below flush to the PCB.

### Resistor Network:
All resistors used are 0603 SMD resistors (6mil x 3mil Surface Mount Device). Most of the resistors serve the purpose of setting baselines for the offset and gain on the circuit shown above. You will need 22k, 47k, and 100 ohm resistors.

### Snapback Filtering:
"Snapback" is a mechanical issue of the spring returning the lever *past* the centerpoint enough for a controller or game to register a return to neutral as an opposite direction input. This can be remedied through installation of a capacitor to ground, or low pass filter, which can reduce the signal of a sharp signal present in snapback. 

There are two locations (top and bottom) dedicated to a "snapback filtering" circuit. The 100 ohm resistor is integrated into this circuit. The remaining component is a capacitor *whose value is specific to your setup*. Most sticks will not need filtering on their SASI.


### Connector:
The JST PH connector ***is a 2.0mm pitch, not the US standard 2.54mm pitch***. This connector *must* be a 90 degree connector and must face out and away from the center of the PCB. From the front of the PCB, with the connector oriented to the right, the connector pins are as follows: [V+ (top), GND, Signal Y, Signal X (bottom)]. Once soldered in, trim the legs of the connector flush to the PCB.

<img src="https://user-images.githubusercontent.com/86936750/213604788-693374d8-303b-455c-b8dd-0f8a2db869b8.png" width=30% height=30%>


---

  
### <sub>Notes:</sub>


[^PCBTest]:

<sub>
The PCB assembly can be tested independent of the full assembly with only a magnet. Orient the magnet's north and south poles along the arrow outlined in front of the sensor under testing. The output voltage can be measured and compared to the expected range (typically 0V - 3.3V).
</sub>


## Mechanical Components and 3D Printing
The mechanical housing and components are designed for and around additive manufacturing processes, most specifically to consumer grade FDM 3D printers. Designs for machined components for low friction polyamide and acetate materials are planned for the future.

### Components: 

- Restrictor Gate Replacement (printed)
- Slider Arms (x2, printed)
- Slider Guide/"Hat" (printed)
- VALUE x VALUE bar magnet (x2)
- LENGTH M3 screws (x4)

### Printed Part Material:
All printed parts are recommended to be printed in Nylon. All parts will undergo a sliding/rubbing motion, and any friction will result in less ideal movements of the lever. If resin printing is available, it is a good alternative. The assembly works fine with PLA/ABS as well, but may require more post processing and frequent application of a dry lubricant.

### Restrictor Gate Replacement:
The restrictor gate replacement is the base of the SASI. It houses the PCB, mounts onto the JLF, and acts as it's own restrictor gate. The restrictor gate's shape alters the movement of the stick and limits the shape that it can move along. For example, Gamecube Controllers have an *octagonal gate*, whereas the Pro Controller and Xbox Controllers have a *circle gate*. 

<img src="https://user-images.githubusercontent.com/86936750/213606522-1337063e-4ab2-4454-8238-59c7060a8ca8.png" width=30% height=30%>

Which you use is simply a matter of preference. The files contain multiple gate shapes to be used. There are no notches in the available files [^notches] 

### Slider Arms:
The Slider Arms serve the function of holding the magnets that the hall effect sensors read and, at the same time, wrap around the Sanwa JLF lever such that motions in the lever result in motions of the magnets. They feature a slot in the center into which the ***actuator*** of the lever fits into.

> picture of one slider arm on lever ; gif of sliding single arm

The lever may slide along the axis the slot opens, but the lever moves the whole part in the axis of the arms.



Two slider arms must be printed ***as mirrors of one another***. This allows them to overlap in the center. 

These sliders may require post processing, as any imperfections and bumps on the surface can lead to friction and binding in the slider guide. This should be done with sandpaper or careful filing to flatten the sides of the slider arms.

In ***only one side of each arm***, insert a magnet and push it until the magnet cannot go any further. When testing, you may find that the magnet direction must be flipped. Keep this in mind before pushing in too tight or if no tools are available to extract the magnet from the arm (i.e. another stronger magnet). ***TEST THIS BEFORE ASSEMBLY***
If printing in Nylon or another warp-prone material, use the Slider Arm with Brim file, which limits the warping on the small arms.

------

### <sub>Note:</sub>

[^notches]:

<sub>
Notches are a controller modification seen in the Super Smash Brothers Melee community that allows for more specific angles to be placed in along the gate. For those interested in implementing controller notches, it may be more difficult to let the stick "lock" into a notch, as the shaft is wide and has a long area that it can slide along. 
</sub>



## Assembly and Installation

Assembly and installation of the SASI mod is fairly straightforward. Very little modification to the JLF lever is required. Components stack on top of one another and do not require precise placement of any parts.

#### Steps:
1. Soldering and Electronics
2. Restrictor Gate
3. Trimming
4. Arm and Guide Hat Setup
5. Arm and Guide Hat Installation
6. Tuning and Testing

### Step 1- Soldering and Electronics
#### 1.1- Soldering Front Face
This section is on soldering the front face of the PCB.

The front of the PCB has multiple surface mount device pads (SMDs) for resistors. Start by "tinning" every **square** pad. This is done by heating the pad with an iron and then applying a very small amount of solder to the pad. To solder a resistor in place, first identify the two solder pads that correspond to a single resistor placement. Prepare an 0603 SMD resistor of the proper value with metal tweezers onto the PCB, near but not on the pads, with the dark/labeled side facing up. Re-melt the solder on the set of pads you are soldering to by placing the iron's tip in-between them. Gently push the resistor into the melted solder until the resistor is in place.




## Problems and Troubleshooting
