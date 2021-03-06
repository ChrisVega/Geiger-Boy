# Geiger-Boy
Half GameBoy, half Geiger counter. It's the Geiger Boy!

## About
The Geiger Boy started as a personal project with a simple goal, make a Geiger counter using an Arduino to use when I go to Chernobyl. It later split into two monsters, a project for my electronics II class and the Geiger Boy. Initially, I was going to design a circuit from scratch and use the kit for comparison. Due to concerns about brining multiple homemade electronics onboard a flight, I ended up only bringing the circuit built from the kit to Chernobyl.

## What is a Geiger Counter?
A Geiger counter is a device which is capable of detecting radioactive particles. This detection is done through the use of a Geiger Muller tube's ionization effect. Inside the tube is a gas and a pair of electrodes with high voltage applied to the anode. This gas ionizes when the tube is struck by a radioactive particle and allows a current to pass through, generating an electrical pulse. These pulses can be counted to determine the number of radioactive particles passing through the tube. This is used to calculate the counts per minute (CPM), which is the measure of radioactive pulses that occur in one minute. Once you have the CPM you can then use that to estimate your dose rate. CPM can be converted to estimate the dose rate using a conversion factor specific to the Geiger tube you are using.

# Electronics II Project
![x](https://i.imgur.com/9vHRrGx.png)

My Electronics II instructor allowed us to work on a class project using the concepts taught in real-world implementations. My task was to design and build a DC-DC boost converter, which was used to power a Geiger counter. The circuit consists mainly of a DC-DC boost converter to provide the voltage needed to supply a Geiger Muller tube. The Geiger Muller tube then produces an electronic signal when detecting a radioactive particle. This signal can be used as an interrupt for a digital circuit. 

## Project description
The circuit uses a DC-DC boost converter to achieve the 400V needed across the Geiger Muller tube an Arduino Uno to generate the PWM signal, supply power, and process the results. Once the voltage is applied across the tube it will begin producing electrical pulses when struck by a radioactive particle. When a particle is detected, the count is incremented for getting the CPM. A pin on the Arduino then sends out a quick pulse to blink an LED produce a "click" through a piezo buzzer.

## DC-DC boost converter Circuit
![x](http://www.learnabout-electronics.org/PSU/images/boost-converter-basic-cct.gif)

The DC-DC boost converted is a circuit that steps up an input voltage to a higher output voltage. This is done by taking advantage of an inductor's property to resist a change in current, which results in a kickback current. It is composed of an inductor, capacitor, diode, and a switch, which in this case is a transistor. When the switch is turned off and off quickly, the inductor produces a kickback current that can be used to charge the capacitor. The switch is toggled fast enough to not allow either to discharge fully. When combined with the diode, only allowing for current to flow in one direction, the result is the two components building off each other and producing a higher voltage than the one supplied. The voltage across the capacitor would be equal to Vin + VL. When the switch is closed, the inductor stores energy. The capacitor supplies power to the load. When the switch is opened, the inductor produces its kickback returning energy to the circuit. The output voltage can be controlled through the duty cycle of the PWM signal used to control the switch

## Circuit Specifications
![x](https://i.imgur.com/jqXMIok.png)

A PWM signal with a duty cycle of 75% was produced by an Arduino Uno and used to control the switch for the DC-DC boost converter. The input voltage was 5V, and 400V was expected at the output. 

An SBM-20 surplus Soviet Geiger Muller tube was used in this circuit, which requires a working voltage between 350V-500V. The tube is capable of detecting beta and gamma particles. When the tube produces a pulse, this applies a current to the base, which activates a transistor. This also produces the pulse that is connected to the microcontroller. This signal is used as an interrupt for getting the CPM and triggering the buzzer and LED. CPM and does rate were read out through the console on a laptop.

### Parts
- 1 SBM-20 Geiger Muller tube
- 1 10mH inductor 
- 1 4.7nF 1000V capacitor
- 1 of each MPSA44 and 2n2222 transistors
- 1  1n4007 or 1n4004
- 1 piezo buzzer
- 1 LED
- Various resistors

## Results
A voltage of about 393V was produced by the DC-DC boost converter, suitable for the SBM-20. When turned on, one can begin to hear the clicking resulting from the background radiation always present in our environment. Uranium glass plates were used to test the circuit. When place near the circuit, the frequency of click began to increase. Similar behavior was monitored on the comparison circuit used as a control indicating desirable functionality. 

# Geiger Boy v.1
![x](https://i.imgur.com/Exo1IyNr.jpg)

The Geiger boy was built using this circuit from [RH electronics](http://www.rhelectronics.net/store/radiation-detector-geiger-counter-diy-kit-second-edition.html), which I highly recommend if the size isn't an issue. The circuit handles the tube's voltage, the buzzer, and the pulse generated by the tube, which can be used to get the CPM. This circuit, along with an ATtiny85, is used to calculate the CPM and dose rate. The ATtiny also controlled an ssd1306 OLED display for viewing dosage and CPM. This was used as my Geiger counter when I went into the Chernobyl exclusion zone. Since I did not get radiation poisoning, I think it worked perfectly. 

[The code for the initial Arduino Uno version can be found here.](https://github.com/ChrisVega/Geiger-Counter)

[The code used in the Geiger Boy v.1 and the previous version using an LCD screen can be found here.](https://github.com/ChrisVega/Geiger-Counter-ATtiny85)

## Design procedure and process
I tried to apply all the information about designing devices and products taught to us in class since this was my first large project. Not everything went perfectly, but that was to be expected. It gave me a great hands-on learning experience with programming and a design process that I can apply for future projects.

First, the Arduino Uno code was written, which used the pulse from the circuit to trigger an interrupt and increment the count for the CPM. Once this was done, the LCD display was added and programmed. Then the general layout in the housing was planned out.

The initial design used an Arduino Uno and LCD screen powered by a 9V battery in a black plastic housing. This idea was short-lived as it was not only big and bulky, but the Arduino Uno is a power hog, resulting in a ~2-hour life span. This was not all a waste as it provided the code that would be used for the next stage. An ATtiny85 was chosen to replace the Uno due to its small compact size and low power consumption. An LCD screen with an I2C backpack was also used due to the ATTiny85's small number of available pins. A battery pack that held 3 AA batteries was then used as the power supply. An estimated 200+ hours of battery life was calculated base off of measured power consumption and battery capacity. A shield was constructed for the ATtiny to connect and power everything easily. This was housed into a clear plastic case. 

![x](https://i.imgur.com/yaHKMPNr.jpg)

While this worked, I was not happy with the outcome. It was not aesthetically pleasing. I decided to redesign it to look better. This was a mistake. I had the great idea to use a GameBoy housing as the housing for my circuit. It was designed to be compact, portable, and hold batteries internally and have a window for a screen and holes for the switches. It seemed perfect and would have been if my components were GameBoy sized and shaped. 

The first issue was that the circuit was too large with the Geiger tube for the top of the housing to close due to small plastic protrusions that held the GameBoy buttons in place. The battery well was cut out for the circuit to sit lower in the housing, meaning another method for holding the batteries had to be found, leading to the second issue. The third was that the LCD screen was too large for the window; a lot of cutting would have to be done to have it fit. As finals week was approaching quickly, I had to rush. The battery well was cut out for the circuit, the battery pack attached to the exterior of the housing on the back, and the screen switched to an ssd1306 OLED display. It was reprogrammed for the display, whit a new library having to be written to save space, and assembled. The end product, the Geiger Boy v.1.

The device was then tested using uranium glass to ensure it was actually detecting radiation. To make sure it wasn't too fragile, it was thrown in a backpack for a week to determine if any housing points were too weak. 

## Circuit
![x](https://i.imgur.com/rjDOTEW.png)

Above is the circuit diagram for the ATtiny shield, which serves as the connection point input, output, and power for the display, Geiger counter, and ATtiny85. The OLED display's SDA and SCL should be connected to the shield's. The Geiger counter output pin should go to INT.

## Parts, procedure, and specifications
The Geiger Boy v.1 can be powered by a 5V power supply, a battery pack with 3 AA batteries was chosen in this implementation. The battery pack was attached to the housing's rear exterior with the wires entering through the slot where a game cartridge would normally be inserted. The positive lead connects to a switch to turn the device off and on.

The operation of the device is effortless; it's either on or off. Once powered up, it will display a startup message until the initial reading is taken.

Readings are taken in 10-second intervals. The count for this period is then multiplied by 6 to estimate a 60 second period for the CPM. This is then used to estimate the dose rate, which is displayed on the screen. 

The Geiger counter circuit can be held in place without attaching it to the housing permanently, allowing for easy removal. This is done by using a GameBoy advance cartridge to hold one end of the circuit with the other held against the housing's edge. 

### Parts 
- GameBoy housing
- RH electronics Geiger counter kit
- SBM-20 Geiger tube
- Ssd1306 OLED
- ATtiny85
- Perf board for ATtiny shield
- Battery pack for 3 AA batteries
- Switch for power
- Various resistors
- Jumper cables

## Results
The tour provided terra-p Geiger counters, which I used to compare with my device. When compared to my Geiger counter, it was observed that my device behaved more erratically and had slightly higher readings at low CPM and dose rates (essentially only at background radiation). The terra-p would read a steady 0.12 - 0.13uSv/h where mine would fluctuate between 0 - 0.26uSv/h. At background radiation, this is not an issue and is well within typical dose rates. The difference at low dose rates can be due to the terra-p being able to individually measure beta and gamma. In contrast, the tube I used is only capable of measuring both. This could also be a result of how the terra-p calculates dosages. At high does rate, my Geiger counter produced nearly the same results as the terra-p. Slight variations are always normal as particle counts will naturally be slightly different at different positions and times. Overall I am confident that my Geiger counter was reliable and produced accurate results and can call the Geiger Boy v.1 a success.

## Improvements
Compared to the terra-p, my Geiger counter seemed very primitive. The terra-p seemed to produce readings more quickly, which varied less at low dose rates and displayed the total accumulated dose. I decided to redesign the device to better fit the housing adding in the functionality for storing and displaying the total accumulated dose allowing it to function as a dosimeter.

# Geiger Boy v.2
This version will attempt to solve the issues that I could not address in the first version of the Geiger Boy outlined in the improvements section. A smaller Geiger counter circuit is also provided by [RH electronics](http://www.rhelectronics.net/store/high-voltage-geiger-probe-driver-power-supply-module-420v-550v-with-ttl-digitized-pulse-output.html) will be utilized. For storing and displaying the total accumulated dose, and FRAM chip will be used due to its large amount, read-write cycles. A high write cycle is needed as the total accumulated dose must be read, updated, and written onto the FRAM every 10 seconds when reading is completed. [Adafruit supplies a breakout board](https://www.adafruit.com/product/1895) for an FRAM chip allowing for more accessible connections.

## Progress
The housing issue has been solved since the size of the circuit was reduced. Because the GameBoy's batter well holds 4 AA batteries but my device only requires 3, a hole was cut out of the wall for the battery well allowing the Geiger tube to sit inside safely next to the batteries. 

The new Geiger counter circuit works as intended; a 1kΩ pull-up resistor is needed to prevent the interrupt pin from floating.

The FRAM module has a library supplied by Adafruit as well but is not compatible with the ATtiny85 due to its use of the Wire library. [The I2C FRAM library was modified](https://github.com/ChrisVega/ATtiny-I2C-FRAM-Driver) to use the TinywireM library allowing for compatibility with the ATtiny85 as well as cleaning up some code which would be unnecessary on the ATtiny85.

The library, which was used for the sd1306 OLED, was found to be incompatible with the TinywireM library. [The ssd1306xled library was modified](https://github.com/ChrisVega/ssd1306xled-I2C) to utilize TinywireM for I2C transmission instead as well as cleaning up the code. 

The total accumulated dose can be stored on the FRAM and read to be displayed on the screen. The circuit was tested on a breadboard currently working as intended, although the image previously shown on startup had to be removed as it took up too much space.

Unfortunately, I ran out of money, and the circuit is currently half-built. Although I have greatly improved the code used for radiation detection. 
