# DataGlove_project
**Data Glove using Flex Sensors**

**Introduction**
- The use of hand gestures as a control input in Human-Machine Interaction (HMI) is an ongoing topic of research. Hand movements are a means of non-verbal communication, and can take the form of either simple actions or more complex ones. Therefore, it stands to reason that using the hands can be an intuitive method for controlling the machines. Apart from just being a method for controlling, transmitting the data of motion, to the machine, over a network can prove to be risk-free and controlling of machines can be less prone to injuries, when working in a hazardous environment.
What is a Data Glove? 
A data glove is an input device that is essentially a glove worn on the hand that contains various electronic sensors that monitor the hand's movements and transform them into a form of input for applications such as virtual reality and robotics. Some data gloves enable tactile sensing, allowing the user to seemingly feel a virtual object and to apply fine-motion control. The glove can be wired or wireless, when transmitting of data is concerned. Various sensor technologies are used to capture physical data like bending of fingers, orientation of wrist and hand. 

**Working**
- Starting from, what is a Flex Sensor? The flex sensor is basically a VARIABLE RESISTOR which changes its terminal resistance upon bending the flex sensor. Its resistance increases linearly with the degree of bending. 
Now, we can’t measure resistance directly using an Arduino or any MCU. So to overcome this, we measure the voltage across the sensor and convert this voltage into corresponding resistance.
To get the value of its resistance and voltage across its terminal, we use the flex sensor in a voltage-divider arrangement. As shown in the Schematic diagram., flex sensor is connected to GND and a 10 kΩ resistor. The voltage across sensor is given as input to Analog Inputs A0, A1, A2, A3 respt.
We get the resistance with the help of modifying the formula -     **vflex=RflexRflex+Rvin** And finding the value of Rflex , where Vin = Arduino 5V and R = 10 kΩ
Then you MAP the values of resistance to suitable outputs like Degree of bend  of Fingers.
Essentially, this whole project is implemented on a wearable glove which can be worn on hand. 

**Applications**
- Robotics
- Gaming (Virtual Motion)
- Medical Devices
- Computer Peripherals
- Musical Instruments
- Physical Therapy


