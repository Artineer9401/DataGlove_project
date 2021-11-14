// Example 5 - Receive with start- and end-markers combined with parsing

#include<Servo.h>
#include<SoftwareSerial.h>
SoftwareSerial BTSerial(10,11);
Servo s1,s2,s3,s4;

const byte numChars = 32;
char receivedChars[numChars];
char tempChars[numChars];        // temporary array for use when parsing

      // variables to hold the parsed data
char messageFromPC[numChars] = {0};
int integerFromPC1 = 0;
int integerFromPC2 = 0;
int integerFromPC3 = 0;
int integerFromPC4 = 0;
char messageFromPC5[numChars] = {0};
float floatFromPC = 0.0;

boolean newData = false;

//============

void setup() {
    Serial.begin(9600);
    BTSerial.begin(38400); 
    
    s1.attach(4); //declaring and defining the servo pins
    s2.attach(5);
    s3.attach(6);
    s4.attach(7);
    
    s1.write(0); //initializing all the servos to 0 degrees
    s2.write(0);
    s3.write(0);
    s4.write(0);
}

//============

void loop() {
    recvWithStartEndMarkers();
    if (newData == true) {
        strcpy(tempChars, receivedChars);
            // this temporary copy is necessary to protect the original data
            //   because strtok() used in parseData() replaces the commas with \0
        parseData();
        showParsedData();
        newData = false;
    }
    s1.write(integerFromPC1);
    s2.write(integerFromPC2);
    s3.write(integerFromPC3);
    s4.write(integerFromPC4);
}

//============

void recvWithStartEndMarkers() {
    static boolean recvInProgress = false;
    static byte ndx = 0;
    char startMarker = '<';
    char endMarker = '>';
    char rc;

    while (BTSerial.available() > 0 && newData == false) {
        rc = BTSerial.read();

        if (recvInProgress == true) {
            if (rc != endMarker) {
                receivedChars[ndx] = rc;
                ndx++;
                if (ndx >= numChars) {
                    ndx = numChars - 1;
                }
            }
            else {
                receivedChars[ndx] = '\0'; // terminate the string
                recvInProgress = false;
                ndx = 0;
                newData = true;
            }
        }

        else if (rc == startMarker) {
            recvInProgress = true;
        }
    }
}

//============

void parseData() {      // split the data into its parts

    char * strtokIndx; // this is used by strtok() as an index

    //strtokIndx = strtok(tempChars,",");      // get the first part - the string
    //strcpy(messageFromPC, strtokIndx); // copy it to messageFromPC
 
    strtokIndx = strtok(tempChars, ","); // this continues where the previous call left off
    integerFromPC1 = atoi(strtokIndx);     // convert this part to an integer
    
    strtokIndx = strtok(NULL, ","); // this continues where the previous call left off
    integerFromPC2 = atoi(strtokIndx);     // convert this part to an integer

    strtokIndx = strtok(NULL, ","); // this continues where the previous call left off
    integerFromPC3 = atoi(strtokIndx);     // convert this part to an integer

    strtokIndx = strtok(NULL, ","); // this continues where the previous call left off
    integerFromPC4 = atoi(strtokIndx);     // convert this part to an integer

    //strtokIndx = strtok(NULL, ","); // this continues where the previous call left off
    //integerFromPC5 = strtokIndx;

    strtokIndx = strtok(NULL ,",");      // get the first part - the string
    strcpy(messageFromPC5, strtokIndx);
    //strtokIndx = strtok(NULL, ",");
    //floatFromPC = atof(strtokIndx);     // convert this part to a float

}

//============

void showParsedData() {
    //Serial.print("Message ");
    //Serial.println(messageFromPC);
    
    Serial.print("Integer///////// ");
    Serial.println(integerFromPC1);

    Serial.print("Integer ");
    Serial.println(integerFromPC2);

    Serial.print("Integer ");
    Serial.println(integerFromPC3);

    Serial.print("Integer ");
    Serial.println(integerFromPC4);

    Serial.print("Message//////////// ");
    Serial.println(messageFromPC5);
    
    //Serial.print("Float ");
    //Serial.println(floatFromPC);
  delay(1000);
}
