## Bidirectional Visitor Counter
#### Aim 
To design a system wherein the number of persons entering or leaving a room is kept track of and displayed on a screen.   
The counter will increase by 1 if the person enters the room and decrease by one if the person leaves the room.   
#### Hardware    
- 8051 based microcontroller
- 16x2 LCD display
- 2 reflective type IR sensors
- 8051 programmer
#### Implementation
The project is implemented using IR sensing mechanism and microcontroller. Two IR senors placed one after the other are used.
- when a person enters, one sensor goes to logic HIGH before the next sensor.
- when a person leaves, the other sensor goes to HIGH first. 
- the count in displayed on a 16x2 LCD screen   

Based on which sensor goes to HIGH first, the counter counts up or down.  
<img src="https://www.electronicshub.org/wp-content/uploads/2015/09/Bidirectional-Visitor-Counter-using-8051-Image-4-760x440.jpg" width=55% height=55%>

IR sensors are very good for short range sensing.  
Having 2 consecutive sensors helps distinguish between incoming and outgoing people. Hence, the LOW to HIGH and HIGH to LOW tansitions are somewhat similar to the positive and negative edges of a clock pulse.   

##### comments
A disadvantage with this model is that the count becomes incorrect when 2 or possibly more people cross the pair of sensors at the same time. It could be in the same direction or in opposite directions as well.  

