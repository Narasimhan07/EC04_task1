## Smart Wristband
#### Aim 
Constantly touching the face with hands can tranfer harmful bacteria into our body. The wristband alerts when the hand is in contact with the mouth, nose or eyes. The watch
vibrates upon sensing this action.
#### Requirements      
- Arduino IDE
#### Approach     
- The wristband uses an accelerometer to identify its slope. Since it is attached to the user's wrist, the degree of tilt on the 3 axes (X, Y and Z) can be used to indicate whether the user's hand is close to their face or not. If a sequence of angles detected by the bracelet matches a hand-to-face movement, it will vibrate. Therefore, the mere fact that it is close to the user's face does not trigger the vibrating motor.   
- False outputs/vibrations can be adjusted by fixing the level of sensivity of the device.   
