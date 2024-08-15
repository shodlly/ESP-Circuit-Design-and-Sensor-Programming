
# Designing and Programming an ESP32 Circuit with an Ultrasonic Sensor (HC-SR04)

## Overview

This task involves designing an electronic circuit using an ESP32 development board with an HC-SR04 ultrasonic distance sensor. The circuit measures the distance between the sensor and an object and displays the measurement on the serial monitor.

## Components

- ESP32 Development Board
- HC-SR04 Ultrasonic Distance Sensor
- Jumper Wires
- Breadboard (optional)

## Circuit Diagram

![image](https://github.com/user-attachments/assets/ed868b40-c77f-444c-be23-441d67a61dac)
- **Trig Pin** (Trigger) of the HC-SR04 is connected to **GPIO5** on the ESP32.
- **Echo Pin** of the HC-SR04 is connected to **GPIO18** on the ESP32.

## Code Explanation

```cpp
int Trig_pin = 5;         // Pin connected to the HC-SR04 Trigger
int Echo_pin = 18;        // Pin connected to the HC-SR04 Echo
long duration;           // Duration of the echo pulse
float speed_of_sound = 0.034; // Speed of sound in cm/µs
float dist_in_cm;        // Distance in centimeters

void setup() {
  Serial.begin(115200);  // Start serial communication at 115200 baud
  pinMode(Trig_pin, OUTPUT); // Set Trigger pin as output
  pinMode(Echo_pin, INPUT);  // Set Echo pin as input
}

void loop() {
  // Send a pulse to trigger the sensor
  digitalWrite(Trig_pin, LOW);
  delayMicroseconds(2); // Short delay to ensure a stable low signal
  digitalWrite(Trig_pin, HIGH);
  delayMicroseconds(10); // Send pulse for 10µs
  digitalWrite(Trig_pin, LOW);

  // Measure the duration of the echo pulse
  duration = pulseIn(Echo_pin, HIGH);

  // Calculate the distance in centimeters and handle errors
  if (duration > 0) {
    dist_in_cm = duration * speed_of_sound / 2; // Divide by 2 for round-trip distance
    Serial.print("Distance: ");
    Serial.print(dist_in_cm);
    Serial.println(" cm");
  } else {
    Serial.println("Error: No echo detected");
  }

  delay(100); // Wait 100 milliseconds before the next measurement
}
```

## Usage

1. Connect the ESP32 board and the HC-SR04 sensor according to the circuit diagram.
2. Upload the provided code to the ESP32 board.
3. Open the Serial Monitor to view the distance measurements displayed in centimeters.

## Customization

You can modify the code to change the behavior of the sensor, such as adjusting the measurement interval or integrating additional features.

## References

- [HC-SR04 Datasheet](https://www.electronicwings.com/nodemcu/hc-sr04-ultrasonic-sensor)
- [ESP32 Documentation](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/)

