# Bidirectional Visitor Counter - Troubleshooting   
The general components that come together in this project are as follows,   
IR sensors -> Microcontroller 8051 -> LCD 16x2 display   
## Testing the Hardware:
#### IR sensors  
The counter might never work if the IR sensor circuitry is burnt out or if the receiver or the transmitter LED of the sensor is burnt or faulty.   
![image](http://www.playembedded.org/blog/wp-content/uploads/2016/04/art_019_IR_sensor.png)   
to check the proper functioning of the IR sensor, we just need to connect sensors pin to an arduino or any microcontroller and implement a simple code as follows:   
```
#define IR 2   
int detection = LOW;    // no obstacle
void setup() {
  Serial.begin(9600);   
  pinMode(IR, INPUT); 
}
void loop() {  
  detection = digitalRead(IR);
  if(detection == HIGH){
    Serial.print("There is an obstacle!\n");
  }
  else{ 
    Serial.print("No obstacle!\n");
  }
  delay(500);    // in ms
}
```
#### LCD display
Checking the LCD display can be done by just connecting the basic pins like ground, power, contrast. When there is no code in the microcontroller, all the 32 boxes will be light 
up on the LCD screen. Sometimes the light up boxes might not be seen. This can be resolved just by adjusting the contrast input using a potentiometer.   
#### Microcontroller
Sometimes the IR sensors and the LCD display will be working but the counter might malfunction or once all the devices are connected to the microcontroller they might not work. 
Microcontrollers/boards have inbuilt systems that prevent them from getting burnt even when the IC is hot. So mostly the error might reside in the code or the logic of the 
problem.   
There is also a possibility of loose connection between the pins. Rechecking all the connections can sometimes make the system work fine.

## Code:   
The project uses some functions in the implementation to make debugging easier. In larger projects, integrating and debugging is made easy when the code is divided into blocks 
and specific functions are assigned to do repetitive actions in the code.
