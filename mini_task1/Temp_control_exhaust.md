### Temperature controlled Exhaust Fan
#### Project Aim
To design a circuit where a exhaust fan switches on when the temperature is above a certain threshold.     
#### Requirements
- 8051 microcontroller, LCD display
- temperature sensor, LM35  
- analog to digital converter
<img src="https://www.electronicshub.org/wp-content/uploads/2016/08/Temperature-Controlled-DC-Fan-Image-5-760x440.jpg" width=50% height=50%>   

#### Approach
- The project works on the principle of Analog to Digital Conversion. The Analog data from the LM35 temperature sensor is given to the analog to digital converter ADC0804.
- As per the changes in the temperature, the output of the ADC is generated. The digital output of the ADC is given to Microcontroller to calculate the temperature and
control the fan accordingly.
