# Smart Irrigation System Using Arduino & IoT

## Overview
A real-world, IoT-enabled Smart Irrigation System developed using Arduino Uno, soil moisture and rain sensors, and a solenoid valve. Designed to optimize water usage and automate irrigation based on real-time feedback from the environment.

Built as part of a Computer Science Bachelor's Dissertation at the University of St. Thomas of Mozambique by **Cicero Narciso Castanheira**.


## System Overview

### Logic Flow
If it's not raining and the soil is dry, the valve opens.

| Rain Sensor | Soil Moisture | Valve |
|-------------|---------------|-------|
| 1 (Rain)    | 1 (Moist)     | OFF   |
| 1 (Rain)    | 0 (Dry)       | OFF *(ignored case)* |
| 0 (No Rain) | 1 (Moist)     | OFF   |
| 0 (No Rain) | 0 (Dry)       | ON ✅ |

---

##  Hardware Components
| Component              | Model / Type            |
|------------------------|-------------------------|
| Microcontroller        | Arduino Uno R3          |
| Soil Moisture Sensor   | HD-38 (analog)          |
| Rain Sensor            | MH-RD (digital)         |
| Actuator               | 12V DC Solenoid Valve   |
| Relay Module           | JQC-3FF-S-Z             |
| Wi-Fi Module           | ESP-01 (ESP8266)        |
| Power Supply           | 12V DC                  |
| Breadboard & Jumpers   | Standard prototyping kit|

---

##  IoT Features (Optional)
- WiFi-enabled via ESP-01
- Connects to Arduino IoT Cloud
- Remote monitoring & control via Arduino Cloud Remote App
- Create dashboards, get notifications, and adjust thresholds

---

## Arduino Code
```cpp
const int rainSensorPin = 4;
const int soilMoisturePin = A0;
const int pumpPin = 10;

const int dryValue = 946;
const int moistValue = 229;

void setup() {
  Serial.begin(9600);
  pinMode(rainSensorPin, INPUT);
  pinMode(soilMoisturePin, INPUT);
  pinMode(pumpPin, OUTPUT);
  Serial.println("Sensor monitoring initialized.");
}

void loop() {
  int rainSensorValue = digitalRead(rainSensorPin);
  int soilMoistureValue = analogRead(soilMoisturePin);

  int moisturePercent = map(soilMoistureValue, dryValue, moistValue, 0, 100);
  moisturePercent = constrain(moisturePercent, 0, 100);

  if (rainSensorValue == 1 && moisturePercent <= 51) {
    digitalWrite(pumpPin, HIGH);
    Serial.println("Pump ON: Dry soil, no rain");
  } else {
    digitalWrite(pumpPin, LOW);
    Serial.println("Pump OFF: Conditions not met");
  }

  delay(3000);
}
 Budget
 Prototype Cost (1-zone):

Component	Quantity	Cost (Mt)
Arduino Uno R3	1	2,500
Soil Moisture Sensor	1	1,100
Rain Sensor	1	250
Relay Module	1	450
ESP-01 WiFi Module	1	500
Solenoid Valve	1	1,300
Misc. (Wires, PSU…)	-	6,900
Total	—	13,000

 Future Improvements:

- Add capacitive sensors for durability
- Weather API integration
- Dashboard with historical data
- Solar-powered version
- AI-based irrigation prediction

License
MIT License (recommended for open-source projects)

Credits

Developed by Cicero Narciso Castanheira
Bachelor of Science in Computer Science
University of St. Thomas of Mozambique – July 2024
Supervisor: MSc. Hélio Augusto Muzamane