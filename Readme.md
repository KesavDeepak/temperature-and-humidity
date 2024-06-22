## Project on Temperature and Humidity identification using DHT22 sensor and Arduino
This project aims to identify the temperature and humidity in the surrounding environment using the DHT22 sensor.
The DHT22 sensor is a digital temperature and humidity sensor that provides accurate and reliable data.

### Components required:-
1. Arduino Board (e.g. Arduino Uno)
2. LCD (16x2) I2C display
3. DHT22 Sensor
4. Connecting wires

### Procedure:-
1. Connect the VCC of the DHT22 sensor to the 5v pin of the Arduino.
Similarly, Connect the VCC of the LCD (16x2) I2C display to the 5v pin of the Arduino.
2. Connect the GND of the DHT22 sensor to the GND pin of the Arduino.
Similarly, Connect the GND of the LCD (16x2) I2C display to the GND pin of the Arduino.
3. Connect the SDA of the DHT22 sensor to the digital pin 2 of the Arduino.
4. Connect the SDA and SCL to the A4 and A5 of the analog pin of Arduino respectively.

### Circuit Diagram:-
![circuit](<WhatsApp Image 2024-06-22 at 23.55.04_645988d1.jpg>)

### Program:-
```c++
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

#define DHTPIN 2       // Define the pin where the DHT22 sensor is connected
#define DHTTYPE DHT22  // Define the type of DHT sensor

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();                      
  lcd.backlight();
  
  lcd.setCursor(0, 0);
  lcd.print("Weather Station");
  
  lcd.setCursor(0, 1);
  lcd.print("Kalyan & Kesav");
  delay(3000); // Display the intro message for 3 seconds

  lcd.clear(); // Clear the screen for the sensor data
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.setCursor(0, 1);
  lcd.print("Humidity: ");
  
  dht.begin();  // Initialize the DHT sensor
}

void loop() {
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();

  if (isnan(temperature) || isnan(humidity)) {
    lcd.setCursor(0, 0);
    lcd.print("Error reading");
    lcd.setCursor(0, 1);
    lcd.print("sensor data");
  } else {
    lcd.setCursor(6, 0);
    lcd.print(temperature, 1);  // Display temperature with one decimal place
    lcd.print(" C");

    lcd.setCursor(10, 1);
    lcd.print(humidity, 1);  // Display humidity with one decimal place
    lcd.print(" %");
  }

  delay(2000); // Wait for 2 seconds before updating the values
}
```
