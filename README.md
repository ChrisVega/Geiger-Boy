# Geiger-Boy
Half GameBoy, half Geiger counter. It's the Geiger Boy!

## About
The Geiger Boy stated as a poersonal project with a simple goal, make a Geiger counter using an arduino. It later split into two monsters, a project for my electronics II class and the Geiger Boy. 

## Electronics II project
The Electronics II project to design and build a DC-DC boost converter to provide the voltage needed for a Geiger counter. 

### What is a Geiger counter?
A Geiger counter is essentially a device which is capable of detecting radioactive particles. This detection is done through the use of a Geiger Muler tubes ionization effect. The tube is filled with a gas and has a high voltage apllied to it's annode. This gas ionizes when the tube is struck by a radioactive particle and, to keep things short, essentially "completes the circuit" resulting in an electical pulse to be generated. This pulse is what is used as a count event which is then used to get the counts per minuet(CPM) or counts per second(CPS). Once you have the CPM you can then use that to estimate your dose rate. CPM can be converted to dose rate by a conversion factor which is specific to the Geiger tube you are using.

### Project description
My circuit uses a DC-DC boost converter to achive the 400V needd across the Geiger Muller tube I am using and an Arduino Uno to generate the PWM signal, supply power and process the results. Once the voltage is applied across the tube it 

### Parts List
