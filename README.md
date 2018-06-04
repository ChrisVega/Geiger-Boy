# Geiger-Boy
Half GameBoy, half Geiger counter. It's the Geiger Boy!

## About
The Geiger Boy stated as a poersonal project with a simple goal, make a Geiger counter using an arduino. It later split into two monsters, a project for my electronics II class and the Geiger Boy. 

## Electronics II project
The Electronics II project to design and build a DC-DC boost converter to provide the voltage needed for a Geiger counter. 

### Project description
My circuit uses a DC-DC boost converter to achive the 400V needd across the Geiger Muller tube I am using and an Arduino Uno to generate the PWM signal, supply power and process the results. Once the voltage is applied across the tube it will begin producing electical pulses when struck by a radioactive particle. When a particle is detected the count is incremented, for getting the CPM, and a pin on the arduino sends out a quick pulse to blink an LED produce a "click" through a piezo buzzer.

### What is a Geiger counter?
A Geiger counter is essentially a device which is capable of detecting radioactive particles. This detection is done through the use of a Geiger Muler tubes ionization effect. The tube is filled with a gas and has a high voltage apllied to it's annode. This gas ionizes when the tube is struck by a radioactive particle and, to keep things short, essentially "completes the circuit" resulting in an electical pulse to be generated. This pulse is what is used as a count event which is then used to get the counts per minuet(CPM) or counts per second(CPS). Once you have the CPM you can then use that to estimate your dose rate. CPM can be converted to estimate dose rate by a conversion factor which is specific to the Geiger tube you are using.

### DC-DC boost converter
![x](http://www.learnabout-electronics.org/PSU/images/boost-converter-basic-cct.gif)
The DC-DC boost converted is a circuit which steps up an input voltage to a higher output voltage. This is done by taking advantage of the property of an inductor to resist a change in current which results in a kickback current. It is usually composed of an inductor, capacitor, diode and a switch whcih in this case is a transistor. When th switch is turned off and off quickly this causes the inductor to produce a kickback current which can be used to charge the capacitor. The switch is toggled fast enough to not allow either to dischrge fully. When combined with the diode only allowing for current to flow in one direction the result is the two building off eachother and producing a higher voltage then the once supplied. The voltage across the capacitor would be equal to Vin + VL. When the switch is closed the inductor stores energery and the capacitor supplies power to the load. When the switch is opened the inductor produces it's kickback returning energy to the circuit. 

### Circuit
![x](https://i.imgur.com/jqXMIok.png)

### Parts List
