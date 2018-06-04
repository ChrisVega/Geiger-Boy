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

## Geiger Boy v.1
![x](https://i.imgur.com/Exo1IyNr.jpg)

The Geiger boy was built using this circuit from [RH electronics](http://www.rhelectronics.net/store/radiation-detector-geiger-counter-diy-kit-second-edition.html) which I highly recommend if size isn't an issue. The circuit handles the voltage for the tube, the buzzer and the pulse generated by the tube which can be used to get the CPM. This circuit, along with an ATtiny85 and ssd1306 oled display, were tossed into the housing of a custom GameBoy original housing to create a device which can estimate and display dose rate. This was used as my Geiger counter when I went into the Chernobyl exclusion zone and, since I did not get radiation posioning, worked perfectly. 

The tour provided terra-p Geiger counters which I used to compared with my device. The result was that my Geiger counter was a little more erratic and had slightly higher readings at low CPM and dose rates (essentially only at background radiation). Theirs would read a steady 0.12 - 0.13uSv/h where mine would fluctuate between 0.12 - 0.26uSv/h. At background radiation this is not an issue and is well within typical dose rates. At high does rate my Geiger counter produced nearly the same results as th terra-p, whith a difference of a few decimal places. The difference at low dose rates can be due to the terra-p being able to measure alpha and gamma individually where as the tube I used is only capable of measuring both. Over all I am confident that my Geiger counter was reliable and prodced accurate results throughout it's use and can call the Geiger Boy v.1 a success.

[The code for the initial Arduino Uno version can be found here.](https://github.com/ChrisVega/Geiger-Counter)
[The code used in the Geiger Boy v.1 as well as the previous version using an LCD screen can be found here.](https://github.com/ChrisVega/Geiger-Counter-ATtiny85)

### Design procedure and process
I tried to apply all the information about designing devices and products that was taught to us in class since this was my first "large" project that had it's own housing. This turned out poorly, but that was to be expected. It gave me a great hands on learning experience with programming and a design process which I will apply to v.2 to make things move along smoother and other projects.

Firs the code for the Arduino Uno was written which used the pulse from the circuit to trigger and interrupt and increment the count for the CPM. Once this was done the LCD display was added and programmed and the general layout in the housing was planned out.

The initial design was to use an Arduino Uno and LCD screen powered by a 9V battery in a black platic housing. This idea was short lived as it was not only big and bulky but the Arduino Uno is a power hog, resulting in a ~2 hour life span. This was not all a waste as it provided the code that I would essentially use for the next stage. Changes were made, and ATtiny85 was cosen to replace the Uno due to it's small compact size and low power consumption. An LCD screen with an I2C back pack was also used doue to the ATTiny85's small number of avaliable pins. A battery pack that held 3 AA batteries was then used as the power supply resulting in 200+ hours of battery life. A sheild was constructed for the ATtiny to connect and power evenything easily and tossed this into a clear platic case. While this was adiquit I was not happy with the outcome as I thought it looked ugly as well as the comments made about it being confscaed by the TSA. I decided to redesign it to look better. This was a mistake.

At some point I had the great idea to use a GameBoy housing as the housing for my circuit. It was designed to be compact, portable and hold batteries internally and have a window for a screen and holes for the switches. It seemed perfect, and would have been if my components were GameBoy sized and shaped. First issue, the circuit was too large with the Geiger tube for the top of the housing to close due to small plaric protusions which held the GameBoy buttons in place. This meant I had to cut out the battery well for the circuit to sit lower in the housing meaning I would have to find another way to store batteries, the second issue. Third was the LCD screen was too large for the window, I would have to do a lot of cuttig to have it fit. As finals weeks was approaching quickly, and the housing being smashed in the mail, I would not have enough time to properly laythings out or wait for the replacement housing to start designing and had to rush. This resulted in some parts, mainly the battery pack, being done at at level which I consider sub-par. As I did not have time to choose a smaller circuit or do major redesigns. The battery well was cut out for the circuit, the battery pack was attached to the exterior of the housing on the back, and I switch to using an ssd1306 OLED display instead which also greatly increased the battery life. It was reporogrammed for the display and assembled. The end prodcut, Geiger Boy v.1.

### Circuit
![x](https://i.imgur.com/rjDOTEW.png)

Above is the circuit diagram for the ATtiny shield whcih serves as the connection point input, output and power for the display, Geiger counter and ATtiny85.

### Parts, procedure and specifications
The Geiger Boy v.1 can be powered by a 5V power supply, a battery pack with 3 AA batteries was chosen in this implementation. The battery pack was attached to the rear exterior of the housing with the wires entering through the slot where a game cartige would nomally be inserted. The positive lead was connected to a switch to turn the devce off and on which connected to the ATtiny's shield, along with the negative lead, to power the other components of the device. 

Operation of the device is very simple, it's either on or off. Once powered up it will display a start up message until the initial reading is taken.

Readings are taken in 10 second intervals, the count for this period is then multipled by 6 to estimate a 60 second period for the CPM. This is then used to estimate the dose rate which is displayed on the screen. 

The Geiger counter circuit can be held in place without ataching it to the housing permenatly allowing for easy removal. This is done by using a GameBoy advance cartridge to hold one end of the circuit with the other held against the edge of the housing. 

Parts 

- GameBoy housing
- RH electronics Geiger counter kit
- SBM-20 Geiger tube
- Ssd1306 OLED
- ATtiny85
- Perf board for ATtiny sheild
- Batery pack for 3 AA batteries
- Switch for power
- Various resistors
- Jumper cables

### Results
As mentioned above the Geiger counter had slighly higer readings which fluctuaed at low dose rates but performed on-par with the terra-p at higer dose rates. While the final housing was adiquite there is room for improvement and will be redesinged to better fit in the housing. 

### Improvements
Compared to the terra-p my Geiger counter seemed very primative. The terra-p seemed to produce readings more quickly which varried less and low dose rated as well as displaying the total accumulated dose. Along with redesigning the device to better fit the the housing adding in the functionality for storing and displaying the total accumulated dose allowing it to also function as a dosimeter.

## Geiger Boy v.2
This version will attempt to solve the issues that I was not able to address in the first version of the Geiger Boy outlined in the improvements seciton. To acomplish this a smaller Geiger counter circuit, also provided by [RH electronics](http://www.rhelectronics.net/store/high-voltage-geiger-probe-driver-power-supply-module-420v-550v-with-ttl-digitized-pulse-output.html) will be utilized. For storing and displaying the total accumulated dose and FRAM chip will be utilized due to it's large amount read write cycles. A high write cycle is needed as the total accumulated dose must be read, upadated, and wirrten onto the FRAM every 10 seconds when a reading is completed. [Adafruit supplies a break out board](https://www.adafruit.com/product/1895) for an FRAM chip allowing for easier connecitons.

### Progress
The housing issue has been solved since the size of the circuit was reduced. Because the batter well of the GameBoy holds 4 AA batteries but my device only requires 3 a hole was cut out of the wall for the battery well allowing the Geiger tube to sit inside safely next to the batteries. 

The new Geiger counter circuit is working as intended, a 1kΩ pull up resistor is however needed to prevent the interrupt pin from floating.

The FRAM module has a library supplied by Adafruit as well but is not compatable with the ATtiny85 due to it's use of the Wire library. [The I2C FRAM library was modified](https://github.com/ChrisVega/ATtiny-I2C-FRAM-Driver) to instead use the TinywireM library allowing for compatability with the ATtiny85 as well as cleaning up some code wich would be unnesesary on the ATtiny85.

The library which was used for the sd1306 OLED was found to be incompatable with the TinywireM library. [The ssd1306xled library was modified](https://github.com/ChrisVega/ssd1306xled-I2C) to utilize TinywireM for I2C transmission instead as well as cleaning up the code. 

Total accumulated does is able to be stored on the FRAM and read to be displayed on the screen. The circuit was tested on a bread board as is currently working as intended, although the image previously displayed on start up had to be removed as it took up too much space.
