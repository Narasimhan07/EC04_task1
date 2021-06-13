# Webcam Privacy     
The timeout feature is implemented using a Real time clock device that can be adjusted using a potentiometer.    
```
#include <Servo.h>

// Date and time functions using a DS3231 RTC connected via I2C and Wire lib
#include "RTClib.h"

// Variables will change:
int ledState = HIGH;         // the current state of the output pin
int buttonState;             // the current reading from the input pin
int lastButtonState = LOW;   // the previous reading from the input pin
bool covered = 1;

// the following variables are unsigned longs because the time, measured in
// milliseconds, will quickly become a bigger number than can be stored in an int.
unsigned long lastDebounceTime = 0;  // the last time the output pin was toggled
unsigned long debounceDelay = 50;    // the debounce time; increase if the output flickers

const int buttonPin = 1;    // the number of the pushbutton pin
const int analogInPin = A4;  // Analog input pin that the potentiometer is attached to
int sensorValue = 0;        // value read from the pot

RTC_DS3231 rtc;
char daysOfTheWeek[7][12] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

Servo myservo;  // create servo object to control a servo
// twelve servo objects can be created on most boards

int pos = 0;    // variable to store the servo position
int timeOpen = 60;
const int closedpos = 170;
const int openpos = 60;
DateTime timerExpires (DateTime(F(__DATE__), F(__TIME__)));

void setup() {
  // initialize serial communications:
  Serial.begin(57600);
  
  myservo.attach(3);  // attaches the servo on pin 9 to the servo object
  //configure pin 2 as an input and enable the internal pull-up resistor
  pinMode(buttonPin, INPUT_PULLUP);

  for (pos = openpos; pos <= closedpos; pos += 1) { // goes from 0 degrees to 180 degrees
    // in steps of 1 degree
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
  if (! rtc.begin()) {
    Serial.println("Couldn't find RTC");
    Serial.flush();
    abort();
  }

  if (rtc.lostPower()) {
    Serial.println("RTC lost power, let's set the time!");
    // When time needs to be set on a new device, or after a power loss, the
    // following line sets the RTC to the date & time this sketch was compiled
    rtc.adjust(DateTime(F(__DATE__), F(__TIME__))+ TimeSpan(0,timeOpen,0,0));
    // This line sets the RTC with an explicit date & time, for example to set
    // January 21, 2014 at 3am you would call:
    // rtc.adjust(DateTime(2014, 1, 21, 3, 0, 0));
  }

  // When time needs to be re-set on a previously configured device, the
  // following line sets the RTC to the date & time this sketch was compiled
  // rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
  // This line sets the RTC with an explicit date & time, for example to set
  // January 21, 2014 at 3am you would call:
  // rtc.adjust(DateTime(2014, 1, 21, 3, 0, 0));
  
}
void loop() {
  DateTime now = rtc.now();
  time_t currenttime = now.unixtime();
  time_t expires = timerExpires.unixtime();
  
  if (currenttime >= expires && covered == 0){
    
      Serial.println("timer expired! closing...");
      for (pos = openpos; pos <= closedpos; pos += 1) { // goes from open to closed
        // in steps of 1 degree
        myservo.write(pos);              // tell servo to go to position in variable 'pos'
        delay(15);                       // waits 15ms for the servo to reach the position
        covered = 1;
      }
  }
  

  // read the state of the switch into a local variable:
  int reading = digitalRead(buttonPin);

  

  // check to see if you just pressed the button
  // (i.e. the input went from LOW to HIGH), and you've waited long enough
  // since the last press to ignore any noise:

  // If the switch changed, due to noise or pressing:
  if (reading != lastButtonState) {
    // reset the debouncing timer
    lastDebounceTime = millis();
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    // whatever the reading is at, it's been there for longer than the debounce
    // delay, so take it as the actual current state:

    // if the button state has changed:
    if (reading != buttonState) {
      buttonState = reading;
      

if(buttonState = HIGH){
  
  if(covered == 1){
    
    // read the analog in value:
    sensorValue = analogRead(analogInPin);
    Serial.print("sensor = ");
    Serial.println(sensorValue);
    
    if (sensorValue < 400){
      timeOpen=2;
    }else if (sensorValue >= 400 && sensorValue < 1000){
      timeOpen=120;
    }else if (sensorValue >= 1000){
      timeOpen=360;
    }
    
    timerExpires = (rtc.now() + TimeSpan(0,0,timeOpen,0));
    currenttime = now.unixtime();
    expires = timerExpires.unixtime();
    Serial.print("It is now ");
    Serial.print(now.year(), DEC);
    Serial.print('/');
    Serial.print(now.month(), DEC);
    Serial.print('/');
    Serial.print(now.day(), DEC);
    Serial.print(" (");
    Serial.print(daysOfTheWeek[now.dayOfTheWeek()]);
    Serial.print(") ");
    Serial.print(now.hour(), DEC);
    Serial.print(':');
    Serial.print(now.minute(), DEC);
    Serial.print(':');
    Serial.print(now.second(), DEC);
    Serial.print(" in unix time = ");
    Serial.print(currenttime);
    Serial.println();
    Serial.print("The timer will expire: ");
    Serial.print(timerExpires.year(), DEC);
    Serial.print('/');
    Serial.print(timerExpires.month(), DEC);
    Serial.print('/');
    Serial.print(timerExpires.day(), DEC);
    Serial.print(" (");
    Serial.print(daysOfTheWeek[now.dayOfTheWeek()]);
    Serial.print(") ");
    Serial.print(timerExpires.hour(), DEC);
    Serial.print(':');
    Serial.print(timerExpires.minute(), DEC);
    Serial.print(':');
    Serial.print(timerExpires.second(), DEC);
    Serial.print(" in unix time = ");
    Serial.println(expires);
    Serial.println();
    Serial.println("opening...");
    for (pos = closedpos; pos >= openpos; pos -= 1) { // goes from closed to open
    
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
    covered = 0;
    
  }
  }else{
    
  Serial.println("closing...");
  for (pos = openpos; pos <= closedpos; pos += 1) { // goes from open to closed
    // in steps of 1 degree
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
    covered = 1;
  }
  
    }
  }
 }
}


  // save the reading. Next time through the loop, it'll be the lastButtonState:
  lastButtonState = reading;
  delay(20);
  ```
  
  The servo is controlled based on the time that is kept track of by the clock.
