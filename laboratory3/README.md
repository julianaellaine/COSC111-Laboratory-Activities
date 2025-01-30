# Fire Detection System with Temperature and Brightness Sensors

## Overview
This project is an Arduino-based fire detection system that uses a thermistor (temperature sensor) and a photoresistor (light sensor) to detect fire. If both the temperature and brightness exceed predefined thresholds, the system blinks an LED to signal a fire alert.

## Components Used
- **Arduino Board**
- **Thermistor (NTC 10K)** - For temperature measurement
- **Photoresistor (LDR)** - For brightness detection
- **Resistors** - 10K Ohm (for thermistor circuit)
- **LED** - For visual alert
- **Jumper Wires**

## Circuit Connections
| Component          | Arduino Pin |
|-------------------|------------|
| Thermistor       | A0         |
| Photoresistor   | A2         |
| LED             | 12         |

## Working Principle
1. The thermistor reads the ambient temperature and converts it using the Beta parameter formula.
2. The photoresistor reads the ambient brightness level.
3. If both the temperature and brightness exceed the predefined thresholds:
   - The LED blinks to signal a fire alert.
4. If the conditions are normal:
   - The LED remains off.

## Threshold Values
- **Temperature Threshold:** 50°C
- **Brightness Threshold:** 220 (Analog value from sensor)

## Code Explanation
- **`readTemperature()`**: Reads and calculates the temperature from the thermistor.
- **`readBrightness()`**: Reads the brightness value from the photoresistor.
- **`setup()`**: Initializes serial communication and sets LED pin as output.
- **`loop()`**: Continuously checks temperature and brightness, controls LED accordingly.

## Code
```cpp
#include <math.h>

#define THERMISTOR_PIN A0   
#define PHOTORESISTOR_PIN A2
#define LED_PIN 12           

const int TEMP_THRESHOLD = 50;  
const int BRIGHTNESS_THRESHOLD = 220;

const float BETA = 3950;     
const float ROOM_TEMP_RESISTANCE = 10000;
const float SERIES_RESISTOR = 10000;  

float readTemperature() {
  int analogValue = analogRead(THERMISTOR_PIN);
  float resistance = SERIES_RESISTOR * (1023.0 / analogValue - 1);
  float temperature = 1 / (log(resistance / ROOM_TEMP_RESISTANCE) / BETA + 1 / 298.15) - 273.15;
  return temperature;
}

int readBrightness() {
  return analogRead(PHOTORESISTOR_PIN);
}

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  float temperature = readTemperature();
  int brightness = readBrightness();
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.print(" °C, Brightness: ");
  Serial.println(brightness);

  if (temperature >= TEMP_THRESHOLD && brightness >= BRIGHTNESS_THRESHOLD) {
    digitalWrite(LED_PIN, HIGH);
    delay(100);
    digitalWrite(LED_PIN, LOW);
    delay(100);
  } else {
    digitalWrite(LED_PIN, LOW);
  }
  delay(500);
}
```

## How to Use
1. Connect the components as per the circuit diagram.
2. Upload the code to the Arduino board using the Arduino IDE.
3. Open the Serial Monitor (`9600 baud rate`) to view temperature and brightness readings.
4. Observe the LED behavior:
   - Blinking = Fire detected.
   - OFF = No fire detected.

## Future Improvements
- Add a buzzer for an audible alarm.
- Use a relay module to trigger an external fire alarm system.
- Integrate with IoT for remote monitoring.