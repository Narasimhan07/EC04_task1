# Webcam Privacy - Troubleshooting    
The variuos components involved in this project are the servo motor, the microcontroller, potentiometer and clock module.
## Hardware   
#### Servo Motor   
The functioning of the servo motor can be tested using this simple piece of code in the arduino IDE. The servo need to connected to the arduino and the code has to be executed   
```
#include <Servo.h>

Servo Myservo;
int servoPin=9;
int servoPos;
String msg="What is the servo angle?:";
void setup()
{
  pinMode(servoPin,OUTPUT);
  Serial.begin(9600);
  Myservo.attach(servoPin);
}

void loop()
{
  Serial.println(msg);
  while(Serial.available()==0){
    
  }
  servoPos=Serial.parseInt();
  Myservo.write(servoPos); 
}
```
<img src="https://www.makerguides.com/wp-content/uploads/2020/08/servo-motor-with-arduino-uno-wiring-diagram-schematic-circuit-tutorial.png" width=60% height=60%>         

#### Potentiometer
The potentiometer knob must be handled slowly. If the potentiometer is faulty or not can also be checked by using an analog pin of the arduino.      

```
// code in arduino IDE	
int voltPin=A3;
int readVal;
float v2;
int waittime=1000;
void setup()
{
  pinMode(voltPin,INPUT);
  Serial.begin(9600);
}

void loop()
{
  readVal=analogRead(voltPin);
  v2=(5./1023.)*readVal;
  Serial.println(v2);
  delay(waittime);
 
}
```    
The output value of this code must vary between 0 and 5 volts as we rotate the knob of the potentiometer.      

## the Arduino/microcontroller    
If the devices attached to the arduino are working fine, and if the code is not having any issues but still the code doesn't upload, then there might be an issue with 
the microcontroller. However, micorcontrollers have inbuilt systems to prevent burning of the ICs. So it is always better to check the connections in the hardware before 
concluding that the microcontroller is damaged.
