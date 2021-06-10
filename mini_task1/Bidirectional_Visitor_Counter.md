## Bidirectional Visitor Counter
#### Aim 
To design a system wherein the number of persons entering or leaving a room is kept track of and displayed on a screen.   
The counter will increase by 1 if the person enters the room and decrease by one if the person leaves the room.   
#### Implementation
The project is implemented using IR sensing mechanism and microcontroller. Two IR senors placed one after the other are used.
- when a person enters, one sensor goes to logic HIGH before the next sensor.
- when a person leaves, the other sensor goes to HIGH first.    

Based on which sensor goes to HIGH first, the counter counts up or down.
