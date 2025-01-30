LED Blinking Sequence

Description

This Arduino sketch controls five LEDs connected to digital pins 12, 11, 10, 9, and 8. The LEDs turn on sequentially, each with a delay of 1000 milliseconds, and then turn off in the same sequence with the same delay.

Hardware Requirements

Arduino board (Uno, Mega, etc.)

5 LEDs

5 Resistors (220Ω recommended)

Jumper wires

Breadboard (optional)

Circuit Diagram

Each LED should be connected as follows:

The anode (long leg) of the LED connects to an Arduino digital pin (12, 11, 10, 9, or 8).

The cathode (short leg) connects to one end of a 220Ω resistor.

The other end of the resistor connects to the ground (GND) of the Arduino.

Code Explanation

Constants and Setup

const int lightSpeed = 1000; // Delay time in milliseconds

void setup() {
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(8, OUTPUT);
}

lightSpeed is set to 1000 milliseconds (1 second) for LED transitions.

The setup() function sets pins 12, 11, 10, 9, and 8 as output.

Loop Function

void loop() {
  int pins[] = {12, 11, 10, 9, 8};

  // ON
  for (int i = 0; i < 5; i++) {
    digitalWrite(pins[i], HIGH);
    delay(lightSpeed);
  }

  // OFF
  for (int i = 0; i < 5; i++) {
    digitalWrite(pins[i], LOW);
    delay(lightSpeed);
  }
}

The loop() function first turns on each LED sequentially with a delay of lightSpeed (1 second) between each activation.

Once all LEDs are turned on, the loop then turns them off in the same sequence, again with a delay.

Usage

Upload the code to your Arduino board using the Arduino IDE.

Observe the LEDs turning on and off sequentially.

Modify lightSpeed to adjust the blinking speed.

Possible Enhancements

Modify the sequence of blinking.

Use a potentiometer to control the delay dynamically.

Implement PWM for brightness control.