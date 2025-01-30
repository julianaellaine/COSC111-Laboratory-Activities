# LED Fading Effect

This Arduino project gradually fades LEDs in and out using PWM (Pulse Width Modulation). It cycles through a set of LEDs, increasing and decreasing brightness smoothly.

## Components Required
- Arduino board (Uno, Mega, etc.)
- 5 LEDs
- 5 Resistors (220Ω - 330Ω)
- Jumper wires
- Breadboard

## Circuit Diagram
Connect the LEDs to the following PWM-supported pins on your Arduino:

| LED | Pin |
|-----|-----|
| 1   | 3   |
| 2   | 5   |
| 3   | 6   |
| 4   | 9   |
| 5   | 10  |

Each LED's cathode should be connected to the ground via a resistor.

## Code Explanation
- The `ledPins[]` array holds the pin numbers where LEDs are connected.
- The `fadeLED()` function is responsible for increasing or decreasing the brightness of each LED using `analogWrite()`.
- The `loop()` function iterates over the LEDs, making them fade in and out sequentially.
- The brightness is modified by `fadeAmount` to create a smooth transition.

## Arduino Code
```cpp
int ledPins[] = {3, 5, 6, 9, 10};
int brightness = 0;
int fadeAmount = 5;

void setup() {
  for (int i = 0; i < 5; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  for (int i = 0; i < 5; i++) {
    fadeLED(ledPins[i], true);
  }
  for (int i = 0; i < 5; i++) {
    fadeLED(ledPins[i], false);
  }
}

void fadeLED(int pin, bool fadeIn) {
  int brightness = fadeIn ? 0 : 255;
  int fadeAmount = fadeIn ? 5 : -5;
  
  while ((fadeIn && brightness <= 255) || (!fadeIn && brightness >= 0)) {
    analogWrite(pin, brightness);
    brightness += fadeAmount;
    delay(30);
  }
}
```

## How to Use
1. Upload the code to your Arduino board using the Arduino IDE.
2. Connect the circuit as described above.
3. Observe the LEDs gradually fade in and out in sequence.

## Customization
- Modify the `fadeAmount` variable to change the speed of fading.
- Adjust the `delay(30)` inside `fadeLED()` to speed up or slow down the transition effect.