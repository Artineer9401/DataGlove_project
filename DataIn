// sending numbers 
#include<SoftwareSerial.h>
SoftwareSerial BTSerial(8,9);//RX,TX


const char startOfNumberDelimiter = '<'; //starting character
const char endOfNumberDelimiter   = '>'; //ending character

int f[4]; //array to store the values of flex sensors

const int FLEX_PIN = A0;
const int FLEX_PIN1 = A1;
const int FLEX_PIN2 = A2;
const int FLEX_PIN3 = A3;

const float VCC = 4.98; // Measured voltage of Ardunio 5V line
const float R_DIV = 11930.0; // Measured resistance of 12k resistor
const float R_DIV1 = 9800.0;


// resistance of flex sensors when straight
const float STRAIGHT_RESISTANCE4 = 173500.00;
const float STRAIGHT_RESISTANCE3 = 70100.00;
const float STRAIGHT_RESISTANCE2 = 47400.00;
const float STRAIGHT_RESISTANCE1 = 84000.00;

// resistance of flex sensors at 90 deg
const float BEND_RESISTANCE4 = 302000.00;
const float BEND_RESISTANCE3 = 210000.00;
const float BEND_RESISTANCE2 = 120000.00;
const float BEND_RESISTANCE1 = 130000.00;

const int numReadings = 5;

int readings[numReadings];      // the readings from the analog input
int readIndex = 0;              // the index of the current reading
int total = 0;                  // the running total
int average = 0;


void setup ()
  { 
  srand (42);
  Serial.begin (9600);
  BTSerial.begin(38400);

  pinMode(FLEX_PIN, INPUT);
  pinMode(FLEX_PIN1,INPUT);
  pinMode(FLEX_PIN2,INPUT);
  pinMode(FLEX_PIN3,INPUT);
     
 // initialize all the readings to 0:
  //for (int thisReading = 0; thisReading < numReadings; thisReading++) {
    //readings[thisReading] = 0;
  //} 
  }
void loop (){
  Serial.println ("Starting ...");

 // Read the ADC, and calculate voltage and resistance from it
  int flexADC = analogRead(FLEX_PIN);
  int flexADC1 = analogRead(FLEX_PIN1);
  int flexADC2 = analogRead(FLEX_PIN2);
  int flexADC3 = analogRead(FLEX_PIN3);

   Serial.println(flexADC);
   Serial.println(flexADC1);
   Serial.println(flexADC2);
   Serial.println(flexADC3);

  // Filter to smooth the readings
  flexADC = flexADC * 0.9 + float(analogRead(FLEX_PIN)) * 0.1; 
  flexADC1 = flexADC1 * 0.9 + float(analogRead(FLEX_PIN1)) * 0.1;
  flexADC2 = flexADC2 * 0.9 + float(analogRead(FLEX_PIN2)) * 0.1;
  flexADC3 = flexADC3 * 0.9 + float(analogRead(FLEX_PIN3)) * 0.1;

  
  float flexV = flexADC * VCC / 1023.0;
  float flexV1 = flexADC1 * VCC / 1023.0;
  float flexV2 = flexADC2 * VCC / 1023.0;
  float flexV3 = flexADC3 * VCC / 1023.0;
 
  float flexR = (R_DIV1 * flexV)/(VCC - flexV);
 /*for(int readindex = 0; readindex >= numReadings; readindex++){
  //Performing a running average to eliminate the noise...
   total = total - readings[readIndex];
  readings[readIndex] = flexR;//analogRead(FLEX_PIN);
  // add the reading to the total:
  total = total + readings[readIndex];
 }
  flexR = total / numReadings; // calculate the average:*/ 

  float flexR1 = (R_DIV * flexV1)/(VCC - flexV1);
  
  float flexR2 = (R_DIV * flexV2)/(VCC - flexV2);
   
  float flexR3 = (R_DIV1 * flexV3)/(VCC - flexV3);
 


  // bend angle:
   f[0] = map(flexR, STRAIGHT_RESISTANCE1, BEND_RESISTANCE1, 0, 90.0);
   f[1] = map(flexR1, STRAIGHT_RESISTANCE2, BEND_RESISTANCE2, 0, 90.0);
   f[2] = map(flexR2, STRAIGHT_RESISTANCE3, BEND_RESISTANCE3, 0, 90.0);
   f[3] = map(flexR3, STRAIGHT_RESISTANCE4, BEND_RESISTANCE4, 0, 90.0);

   f[0] = constrain(f[0], 0, 90.0);
   f[1] = constrain(f[1], 0, 90.0);
   f[2] = constrain(f[2], 0, 90.0);
   f[3] = constrain(f[3], 0, 90.0);

    Serial.println(flexR);
    Serial.println(flexR1);
    Serial.println(flexR2);
    Serial.println(flexR3);
////////////////////////////////////////////////////

    if (f[0]<= 5 && f[1]<= 5 && f[2]<= 5 && f[3]<= 5 )
      Serial.println("low");
    else if (f[0]>= 80 && f[1]>= 80 && f[2]>= 80 && f[3]>= 80 ) 
        Serial.println("high");
    else if (f[0]<= 5 && f[1]<= 5 && f[2]>= 80 && f[3]>= 80 )
        Serial.println('2');
     else if (f[0]<= 5 && f[1]>= 80 && f[2]>= 80 && f[3]>= 80 )
        Serial.println('1');
     else if (f[0]<= 5 && f[1]<= 5 && f[2]<= 5 && f[3]<= 5 )
        Serial.println('3');



    
///////////////////////////////////////////////////
  BTSerial.write (startOfNumberDelimiter);
  for (int i = 0; i < 4; i++)
   {
       
    //BTSerial.write("hello");
    BTSerial.write(",");
    for(i = 0; i < 4; i++){
     BTSerial.print (f[i]);    // send the number
     BTSerial.write(",");
     Serial.println(f[i]);
     delay(1);
     
    }

    if (f[0]<= 15 && f[1]<= 15 && f[2]<= 15 && f[3]<= 15 )
     {
      BTSerial.write("low");
      BTSerial.write(",");}
    else if (f[0]>= 50 && f[1]>= 50 && f[2]>= 50 && f[3]>= 50 )
    { 
        BTSerial.write("high");
        BTSerial.write(",");}
    else if (f[0]<= 5 && f[1]<= 5 && f[2]>= 50 && f[3]>= 50 )
    {
        BTSerial.write('2');
        BTSerial.write(",");}
     else if (f[0]<= 5 && f[1]>= 50 && f[2]>= 50 && f[3]>=50 )
     {
        BTSerial.write('1');
        BTSerial.write(",");}
     else //(f[0]<= 5 && f[1]<= 5 && f[2]<= 5 && f[3]<= 5 )
     {
        BTSerial.write('3');
        BTSerial.write(",");}
    //BTSerial.print (rand());
    //BTSerial.println ();
   }  // end of for
  BTSerial.write (endOfNumberDelimiter);
  delay(1000);
}  // end of loop
