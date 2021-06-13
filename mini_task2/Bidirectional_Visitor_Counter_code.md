## Code for the Visitor Counter   
The project has been implemented using a 8051 microcontroller. However, this sample code is written using arduino IDE. 
The logic is similar, only the syntax might be slightly different.   
![image](https://circuitdigest.com/sites/default/files/circuitdiagram_mic/Visitor-Counter-Circuit1.gif)    
The below code is written for arduino IDE. In loop function we read sensors input and increment or decrement the counting depending upon enter or exit operation.      
```
#include<LiquidCrystal.h>
LiquidCrystal lcd(13,12,11,10,9,8);

#define in 14
#define out 19

int count=0;

void IN()
{
    count++;
    lcd.clear();
    lcd.print("Person In Room:");
    lcd.setCursor(0,1);
    lcd.print(count);
    delay(1000);
}

void OUT()
{
  count--;
    lcd.clear();
    lcd.print("Person In Room:");
    lcd.setCursor(0,1);
    lcd.print(count);
    delay(1000);
}

void setup()
{
  lcd.begin(16,2);
  lcd.print("Visitor Counter");
  delay(2000);
  pinMode(in, INPUT);
  pinMode(out, INPUT);
  lcd.clear();
  lcd.print("Person In Room:");
  lcd.setCursor(0,1);
  lcd.print(count);
}

void loop()
{  
  
  if(digitalRead(in))
  IN();
  if(digitalRead(out))
  OUT();
  
}
```
