Sender Joystick:
the joystick provides analog values, we'll read the X-axis from one analog pin in this case GPIO 1 and send it via ESP-NOW to the receiver.

Receiver Code (Control Servo with Joystick X-axis):
This will map the joystick X-axis value to the servo angle.
servo on analog or in the case of ESP32 ADC pin

Analog Pin Range:
    The joystick typically outputs a range from 0 to 4095 on the ESP32 for analog readings.
    You can map this range to the servo's 0–180 degrees using:  
int servoAngle = map(incomingData.joyX, 0, 4095, 0, 180);

Joystick Y-axis (Optional):
    If you want to control additional servos or devices using the joystick's Y-axis, you can add logic for joyY.

Power Supply Considerations:

    Ensure that the servo and joystick are adequately powered, especially if using the same power source for both.

To use both the joystick X-axis and Y-axis to control two servos, you can map the X and Y values separately to different servo angles. see codes how you can modify the code to handle two servos, one for each axis.

Key Points:

    Two Servos: One servo (servoX) is controlled by the joystick's X-axis, and the other servo (servoY) is controlled by the joystick's Y-axis.
    Mapping:
        The X-axis joystick value is mapped using int servoAngleX = map(incomingData.joyX, 0, 4095, 0, 180); to control the angle of servoX.
        Similarly, the Y-axis joystick value is mapped using int servoAngleY = map(incomingData.joyY, 0, 4095, 0, 180); to control servoY.
    Pin Attachments:
        servoX.attach(1); attaches the first servo to GPIO 1 (which was working previously).
        servoY.attach(2); attaches the second servo to GPIO 2, but you can choose another available GPIO if needed.

Notes:

    Ensure both servos are properly powered. As before, using an external power supply for the servos might help if you're seeing instability.
    The joystick should provide values between 0 and 4095, which are then mapped to the range 0–180 to match the servo's angular movement.
