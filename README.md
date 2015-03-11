#include <Servo.h>

Servo motorleft;
Servo motorright;
Servo motorarm;

void setup()
{
  motorleft.attach(8);
  motorright.attach(9);
  motorarm.attach(11);
}
  

#define MOTOR_LEFT  251
#define MOTOR_RIGHT 252
#define ARM         253
 
while(1) {
    int opcode;
    // Try to get an opcode. Keep trying until we actually see an opcode.
    do {
        opcode = Serial.read();
    } while (opcode < 251);
 
    // Get value byte.
    int val = Serial.read();
 
    // Control
    switch (opcode) {
    case MOTOR_LEFT:
        motorleft.write(180);
        break;
    case MOTOR_RIGHT:
        motorright.write(180);
        break;
    case ARM:
        motorarm.write(180);
        break;
    default:
        break;
    }
    delay(1);   // Without this you'll exhaust your serial buffer and the servo won't spin for very long.
}
