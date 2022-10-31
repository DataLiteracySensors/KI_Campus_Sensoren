HTML Datei für den Vertiefungskurs der Umweltsensoren für den KI Campus

# Data Literacy - Daten bereitstellen mit Sensoren
Willkommen!

Um Umweltdaten mit Sensoren erfassen und dokumentieren zu können, benötigen wir Hardware und Software. Mit diesem Reposotiry soll das Programmieren der Software als auch das Zusammensetzen der Hardware erleichtert werden. Hierfür besteht die Wahl zwischen zwei Anbieter. Sensebox und Grove Kit. 

###   Welches Kit ist das Richtige für mich?

![Spinnendiagram_Vergleich_Hardware_2@300x](https://user-images.githubusercontent.com/100515435/199057365-67ea04a7-ceb1-4e77-8f58-3876eeb12f09.png)


### Grove Kit
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
- Seeedstudio.com: https://www.seeedstudio.com/Grove-Beginner-Kit-for-Arduino-p-4549.html
- Amazon.de: https://www.amazon.de/seeed-studio-Beginner-Arduino-Starter/dp/B088GY8JLG

Zusätzliche Module
- Feinstaubsensor https://www.conrad.de/de/p/joy-it-sen-sds011-sensor-modul-1-st-1884873.html
- SD Karten Modul https://www.conrad.de/de/p/micro-sd-card-reader-modul-mit-spi-schnittstelle-838242778.html

#### Verkabelung

Das Grove Beginner Kit hat den Vorteil, dass alle mitgelieferten Module bereits verkabelt sind. Jediglich der Feinstaub Sensor sowie das SD Modul müssen manuel angeschlossen werden. 

| Modul  | Pin |
| ------------- | ------------- |
| Fine Dust Sensor| UART  |
| SD Modul RX | 18 |
| SD Modul TX | 19 |
| Sound | A2  |
| Light| A3 |


#### Code
Den Code für das Grove Kit findest du in der ZIP Datei "Grove_Kit_Code.zip" oben zum Herunterladen.

#### Sonstiges

Für eine noch detailiertere Beschreibung des Grove Beginner Kits ist folgender Lesson Guide zu empfehlen. 
https://wiki.seeedstudio.com/Grove-Beginner-Kit-For-Arduino/#breakout-instruction

### Senesebox
##### Mainboard
##### Sensoren
##### Einkaufsliste
##### Verkabelung
##### Code
