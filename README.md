# Arduino-Simon-Says-Project

This is a physical memory game based on the classic **Simon Says** game, built using Arduino UNO. The game lights up a sequence of LEDs that the player has to remember and repeat using push button inputs. The sequence gets longer with each round. The game also includes an LCD display that provides the player with instructions as well as a buzzer for sound feedback. A dual player option as well, where players go one after another. At the end, the individual scores are displayed as well as the winner. 

---

## Tinkercad Simulation
[Click here to view the simulation](https://www.tinkercad.com/things/9QhDBLZ3X4b-simon-says-final?sharecode=ZoL7l3RGfnsuFzS5m910p0wC_b0-Om4zPBkRMCpe7Gk)

---

## Components Used
- Arduino Uno
- 4 LEDs (Red, Yellow, Green, Blue)
- 4 Push Buttons
- Resistors
- Breadboard and jumper wires
- Buzzer (for sound feedback)
- LCD display and i2c module

---

## How It Works - single player mode
- The game starts by blinking one LED.
- The player presses the corresponding button.
- If correct, the next round adds one more LED to the sequence.
- If the player presses a wrong button, the game ends and the score is displayed.

---

## Contrubutions
This project was collaboratively developed by 
Sukeerthi Kattamuri
Chandralekhya
For Electronic Workshop 1 – 1-1  
