# Geiger-Boy
Half GameBoy, half Geiger counter. It's the Geiger Boy!

## About
The Geiger Boy stated as a poersonal project with a simple goal, make a Geiger counter using an arduino which I would use when I went to Chernobyl. It later split into two monsters, a project for my electronics II class and the Geiger Boy. I was going to bring a circuit that I desinged and a circuit built from a kit to compare it to originaly. Due to concerns about brining multiple homemade electronics on board a flight I ended up only bringing the circuit built from the kit. I thought my circuit would attract too much attention and end up with everything being confiscated and leaving me without a Geiger counter in Chernobyl. This kit circuit was used as the circuit in the Geiger Boy v1. 

## Electronics II project
The Electronics II project to design and build a DC-DC boost converter to provide the voltage needed for a Geiger counter. 

### Project description
My circuit uses a DC-DC boost converter to achive the 400V needd across the Geiger Muller tube I am using and an Arduino Uno to generate the PWM signal, supply power and process the results. Once the voltage is applied across the tube it will begin producing electical pulses when struck by a radioactive particle. When a particle is detected the count is incremented, for getting the CPM, and a pin on the arduino sends out a quick pulse to blink an LED produce a "click" through a piezo buzzer.

### What is a Geiger counter?
A Geiger counter is essentially a device which is capable of detecting radioactive particles. This detection is done through the use of a Geiger Muler tubes ionization effect. The tube is filled with a gas and has a high voltage apllied to it's annode. This gas ionizes when the tube is struck by a radioactive particle and, to keep things short, essentially "completes the circuit" resulting in an electical pulse to be generated. This pulse is what is used as a count event which is then used to get the counts per minuet(CPM) or counts per second(CPS). Once you have the CPM you can then use that to estimate your dose rate. CPM can be converted to estimate dose rate by a conversion factor which is specific to the Geiger tube you are using.

### DC-DC boost converter
![x](http://www.learnabout-electronics.org/PSU/images/boost-converter-basic-cct.gif)

The DC-DC boost converted is a circuit which steps up an input voltage to a higher output voltage. This is done by taking advantage of the property of an inductor to resist a change in current which results in a kickback current. It is usually composed of an inductor, capacitor, diode and a switch whcih in this case is a transistor. When th switch is turned off and off quickly this causes the inductor to produce a kickback current which can be used to charge the capacitor. The switch is toggled fast enough to not allow either to dischrge fully. When combined with the diode only allowing for current to flow in one direction the result is the two building off eachother and producing a higher voltage then the once supplied. The voltage across the capacitor would be equal to Vin + VL. When the switch is closed the inductor stores energery and the capacitor supplies power to the load. When the switch is opened the inductor produces it's kickback returning energy to the circuit. The output voltage can be controled through the duty cycle of the PWM signal used to controll the switch

### Circuit
![x](https://i.imgur.com/jqXMIok.png)

Note that the buzzer and LED + 200Ω were put in parrallel in the final circit which produced a louder click. The two can also be controlled by a transistor used as a switch which produces slightly better results but was not needed for this in class demonstration. The base is connected to the arduino pin and a 5V source is connected to the collector and the LED and buzzer are connected to the emitter. 

### Parts, procedure and specifications
A duty cycle of 75% was produced by an Arduino Uno and used to contorl the switch for the DC-DC boost converter. The input voltage was 5V and 400V was expected at the output. 

An SBM-20 surplus Soviet Geiger Muller tube was used in this circuit which requires a working voltage between 350V-500V. The tube is capable of detecting alpha and gamma particles. When the tube produces a pulse this applies a current to the base which activates a transistor. This also produces a pluse but one which can be better used by a micro controller. This pulse is then used as the cont event for getting COM and triggering the buzzer and LED.

Parts
- 1 SBM-20 Geiger Muller tube
- 1 10mH inductor 
- 1 4.7nF 1000V capactitor
- 1 of each MPSA44 and 2n2222 transistors
- 1  1n4007 or 1n4004
- 1 piezo buzzer
- 1 LED
- Various resistors

### Results
A voltage of about 393V was produced by the DC-DC boost converter whcih was suitable for the SBM-20. This resulted in the desired effect of being able to detect radioactive particled which struck the tube.

## Geiger Boy
![x](https://i.imgur.com/Exo1IyNr.jpg)

The Geiger boy was built using this circuit from [RH electronics](http://www.rhelectronics.net/store/radiation-detector-geiger-counter-diy-kit-second-edition.html) which I highly recommend if size isn't an issue. The circuit handles the voltage for the tube, the buzzer and the pulse generated by the tube which can be used to get the CPM. This circuit, along with an ATtiny85 and ssd1306 oled display, were tossed into the housing of a custom GameBoy original housing to create a device which can estimate and display dose rate. This was used as my Geiger counter when I went into the Chernobyl exclusion zone and, since I did not get radiation posioning, worked perfectly. 

The tour provided terra-p Geiger counters which I used to compared with my device. The result was that my Geiger counter was a little more erratic and had slightly higher readings at low CPM and dose rates (essentially only at background radiation). Theirs would read a steady 0.12 - 0.13uSv/h where mine would fluctuate between 0.12 - 0.26uSv/h. At background radiation this is not an issue and is well within typical dose rates. At high does rate my Geiger counter produced nearly the same results as th terra-p, whith a difference of a few decimal places. Over all I am confident that my Geiger counter was reliable and prodced accurate results throughout it's use. The difference at low dose rates can be due to the terra-p being able to measure alpha and gamma individually where as the tube I used is only capable of measuring both.


