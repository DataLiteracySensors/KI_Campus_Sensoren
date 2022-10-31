HTML Datei für den Vertiefungskurs der Umweltsensoren für den KI Campus

# Data Literacy - Daten bereitstellen mit Sensoren
Willkommen!

Um Umweltdaten mit Sensoren erfassen und dokumentieren zu können, benötigen wir Hardware und Software. Mit diesem Reposotiry soll das Programmieren der Software als auch das Zusammensetzen der Hardware erleichtert werden. Hierfür besteht die Wahl zwischen zwei Anbieter. Sensebox und Grove Kit. 

##   Welches Kit ist das Richtige für mich?

![Spinnendiagram_Vergleich_Hardware_2@300x](https://user-images.githubusercontent.com/100515435/199057365-67ea04a7-ceb1-4e77-8f58-3876eeb12f09.png)


## Grove Kit
#### Microcontroller

Bild von Mainboard. 

Das Grove Kit besteht aus 10 Modulen und dem Microcontroller Seeeduino Lotus. Bei dem Microcontroller handelt es sich genauergesagt um ein ATMEGA328 Mikrocontroller Entwicklungsboard. Seeeduino Lotus hat 14 digitale Ein-/Ausgänge (6 davon können PWM ausgeben) und 7 analoge Ein-/Ausgänge, einen Micro-USB-Anschluss, einen ICSP-Header, 12 Grove-Anschlüsse, einen Reset-Knopf.


#### Sensoren

| Modul  | Interface |
| ------------- | ------------- |
| LED | Digital  |
| Buzzer| Digital  |
| Button | Digital  |
| OLED Display 0.96"| I2C  |
| Rotary Potentiometer | Analog  |
| Light| Analog  |
| Sound | Analog  |
| Temperature & Humidity Sensor| Digital  |
| Air Pressure Sensor|  	I2C  |
| 3-Axis Accelerator |  	I2C  |

#### Von uns genutze Module

| Modul  | Interface |
| ------------- | ------------- |
| Light| Analog  |
| Sound | Analog  |
| Temperature & Humidity Sensor| Digital  |
| Air Pressure Sensor|  	I2C  |

#### Zusätzliche Module

| Modul  | Interface |
| ------------- | ------------- |
| Fine Dust Sensor| UART  |
| SD Modul | UART |

#### Einkaufsliste

Das Grove Kit ist bei diversen Online-Anbietern zum Verkauf und kann bei folgenden Websites bestellt werden:

[Seeedstudio.com](https://www.seeedstudio.com/Grove-Beginner-Kit-for-Arduino-p-4549.html)

[Amazon.de](https://www.amazon.de/seeed-studio-Beginner-Arduino-Starter/dp/B088GY8JLG)

Zusätzliche Module

[Feinstaubsensor](https://www.conrad.de/de/p/joy-it-sen-sds011-sensor-modul-1-st-1884873.html)

[SD Karten Modul](https://www.conrad.de/de/p/micro-sd-card-reader-modul-mit-spi-schnittstelle-838242778.html)

#### Verkabelung

Das Grove Beginner Kit hat den Vorteil, dass alle mitgelieferten Module bereits verkabelt sind. Jediglich der Feinstaub Sensor sowie das SD Modul müssen manuell angeschlossen werden. Aus debugging Gründen wurde im beigelegten Arduino Code das Mikrofon auf pin A2 verlegt. 

| Modul  | Pin |
| ------------- | ------------- |
| Fine Dust Sensor| UART  |
| SD Modul RX | 18 |
| SD Modul TX | 19 |
| Sound | A2  |

#### Libaries

```
#include "Arduino_SensorKit.h"
#include <Wire.h>
#include <SPI.h>
#include <SD.h>
#include <SDS011.h>
#include <SparkFun_SCD30_Arduino_Library.h>
```

#### Code
Den Code für das Grove Kit findest du in der ZIP Datei "Grove_Kit_Code.zip" oben zum Herunterladen.
```
/*
   SD Card Wiring:
   MOSI - pin 11
   MISO - pin 12
   CLK - pin 13
   CS - pin 10
   !DHT pin 3 
   SDSrx 18
   SDStx 19
*/

#include "Arduino_SensorKit.h"
#include <Wire.h>
#include <SPI.h>
#include <SD.h>
#include <SDS011.h>
#include <SparkFun_SCD30_Arduino_Library.h>

SDS011 my_sds;
SCD30 airSensor;

int chipSelectSD = 10;
int micPin = A2;
int lightPin = A3;
int SDSrx = 18;
int SDStx = 19;
float p10,p25;
int error;

int micValue;
int lightValue;
int tempValue;
int humidValue;
int pressureValue;
int co2Value;

String dataString = "";

void setup() {
  Serial.begin(9600);
  Wire.begin();

  pinMode(micPin , INPUT);
  pinMode(lightPin , INPUT);
  my_sds.begin(SDSrx,SDStx);
  Environment.begin();
  Pressure.begin();
  airSensor.begin();

  Serial.print("Initializing SD card...");
  if (!SD.begin(chipSelectSD)) {
    Serial.println("Card failed, or not present");
  }
  Serial.println("card initialized.");
}

void loop() {
  // reading sensors:
  micValue = analogRead(micPin);
  lightValue = analogRead(lightPin);
  tempValue = Environment.readTemperature();
  humidValue = Environment.readHumidity();
  pressureValue = Pressure.readPressure();
  co2Value = airSensor.getCO2();
  error = my_sds.read(&p25,&p10);

  // formatting output:
  dataString = String(micValue) + "," +
               String(lightValue) + "," +
               String(tempValue) + "," +
               String(humidValue) + "," +
               String(pressureValue) + "," + 
               String(co2Value) + "," + 
               String(p10) + "," + 
               String(p25)
               ;

  // writing to SD and Serial
  File dataFile = SD.open("datalog.txt", FILE_WRITE);
  if (dataFile) {
    dataFile.println(dataString);
    dataFile.close();
    Serial.println(dataString);
  }
  else {
    Serial.println("error opening datalog.txt");
  }
  delay(100);
}
```

#### Sonstiges

Für eine noch detailiertere Beschreibung des Grove Beginner Kits ist folgender Lesson Guide zu empfehlen. 

[wiki Seed Studio](https://wiki.seeedstudio.com/Grove-Beginner-Kit-For-Arduino/#breakout-instruction)

## Senesebox

#### Microcontroller

Bild von Mainboard.

Der Microcontroller der Sensebox basiert auf dem ARM Cortex-M0+ Prozessor aus der SAM D21 Familie von Microchip. Dieser hat 4 digitale, 2 UART/serial und 5 I2C Schnittstellen. Außerdem verfügt die Sensebox über zwei weitere Schnittstellen, sogenannte BEEs, für das Speichern von Daten über die Cloud via Wifi und über eine SD Karte. Hierbei handelt es sich um MOSI/MISO und RX/TX Schnittstellen. 

#### Sensoren

| Modul  | Interface |
| ------------- | ------------- |
| Light| I2C  |
| Humidity Sensor| I2C  |
| Temperature & Air Pressure Sensor|  	I2C  |
| Feinstaub|  	UART/serial  |
| Wifi |  	Bee1  |
| SD Modul |  	Bee2  |



#### Einkaufsliste

Es ist zu empfehlen das Kit als Gesamtes und keine Einzelteile zu erwerben. Dieses kann auf der [Website](https://sensebox.kaufen/product/sensebox-edu) der Sensebox im Shop erworben werden. 

#### Verkabelung

#### Libaries

```
#include <senseBoxIO.h>
#include <WiFi101.h>
#include <SPI.h>
#include <Wire.h>

#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_HDC1000.h>
#include <Adafruit_BMP280.h>
#include <Adafruit_BME680.h>
#include <VEML6070.h>
#include <SDS011-select-serial.h>
#include <SparkFun_SCD30_Arduino_Library.h>
#include <LTR329.h>
```

Das [Board Support Package](https://sensebox.github.io/books-v2/edu/en/erste-schritte/board-support-packages-installieren.html) ist essentiell und muss vorher heruntergeladen werden.

#### Code


#### Sonstiges

Online ist eine hilfreiche [Dokumentation](https://sensebox.github.io/books-v2/edu/en/) der Sensebox zu finden. Hier werden auch Beispiele als auch detailiertere Beschreibungen zur Hardware geliefert. 
