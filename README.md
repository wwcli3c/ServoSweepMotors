# ServoSweepMotors

This is a simple Arduino project to control 4 servo motors.

The idea is easy:
- First, all 4 servos sweep back and forth for 2 seconds (like the Servo "Sweep" example).
- After that, they all **stay at 90 degrees**.


What You Need:

- Arduino Uno (or any compatible board)
- 4 servo motors
- Jumper wires
- External power supply (recommended for smooth servo movement)



Connections:

Servo to  Arduino Pin 
 1     to D10         
 2     to D11         
 3     to D12         
 4     to D13    
 And every servo take positive and negative from arduino : Positive = 5v pin / Negative =GND pin

How It Works:

- The servos move from 0° to 180° and back.
- After 2 seconds, they all stop at 90° and stay there.

```Code
#include <Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

unsigned long startTime;
bool sweepDone = false;

void setup() {
  servo1.attach(10);
  servo2.attach(11);
  servo3.attach(12);
  servo4.attach(13);

  startTime = millis();
}

void loop() {
  if (!sweepDone) {
    unsigned long currentTime = millis();

    for (int pos = 0; pos <= 180; pos++) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(10);
      if (millis() - startTime >= 2000) {
        sweepDone = true;
        break;
      }
    }

    for (int pos = 180; pos >= 0; pos--) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(10);
      if (millis() - startTime >= 2000) {
        sweepDone = true;
        break;
      }
    }
  } else {
    // Stop all at 90°
    servo1.write(90);
    servo2.write(90);
    servo3.write(90);
    servo4.write(90);
  }
}
