# Software
Original Code von: <br> 
 * Autor: Jörg Bernhardt<br>
 * Datum: 11/2020<br>
 * Source: https://github.com/Joerg-66/ESP8266-WebMonitor<br>
<br>
 Änderungen by zeroTM<br>
 Datum: 06/2024<br>
 <br> 
   Änderungen:  <br>
   -- Adafruit ILI9341<br>
   ++ TFT_eSPI Bibliothek (mehrere Displays unterstützt!)<br>
   -- ILI9341_Graphic.h (class komplett entfernt)<br>
   -- ILI9341_Graphic.cpp (void-Funktionen in WebMonitor_1.ino eingefügt)<br>
   <br>
   <br>
   In planung:<br>
   ** auf Platformio wechseln<br>
   ** ESP32 unterstützung<br>
   ** Konfiguration erweitern(Einstellungen editierbar machen, Einstellungen erweitern)<br>
   ** Touchscreen unterstützung<br>
   ** Router Statistik<br>
   ** Call-Monitor<br>
   <br>

## Die Entwicklungsumgebung
Lade und installiere von der Seite https://www.arduino.cc die Software Arduino (Version 1.8.15) <br>
 <br>
Istalliere die folgenden Arduino Bibliotheken: <br>
* Adafruit GFX Library	(Version 1.10.10) <br>
* Adafruit BusIO			(Version 1.9.0) <br>
* Adafruit STMPE610		(Version 1.1.3) <br>
 <br>
Lade und installiere die TR-064 Bibliotheken von: <br>
* https://github.com/Aypac/Arduino-TR-064-SOAP-Library   (Version: 1.1.0 - Feb 2020) <br>
Diese Bibliothek ist eine großartige Arbeit von René Vollmer und übernimmt die TR-064 Kommunikation zum Router. <br>
Um diese Bibliothek nicht zu modifizieren, wurden die TR064_Query.h und TR064_Query.cpp als Zwischenschicht geschrieben. <br>
 <br>
Lade und installiere die TFT_eSPI Bibliothek von: <br>
* https://github.com/Bodmer/TFT_eSPI (Version: master - Aktuell Jun 2024) <br>
Umfangreiche Bibliothek zum einfachen einbinden von vielen TFT-Displays - geschrieben von Bodmer <br>
** unter seine Github Repositories sind einige interessante und nützliche Bibliotheken zu finden <br>
** https://github.com/Bodmer?tab=repositories <br>
 <br>
In der Arduino IDE unter "Voreinstellungen" im Feld "Zusätzliche Boardverwalter-URLs den folgenden Eintrag hinzufügen: <br>
* https://arduino.esp8266.com/stable/package_esp8266com_index.json <br>
 <br>
Nun kann in der Arduino IDE über den Boardverwalter das "ESP Community" Packet installiert weden: <br>
ESP8266 Community		(Version 2.7.4) <br>
***ACHTUNG! Aktuell muss das etwas ältere Paket wählen. Die Pakete Version 3.x.x verursachen einen Konflikt mit der TR-064-SOAP-Library.*** <br>
 <br>
Jetzt ist in der Arduino IDE das Board "LOLIN(WEMOS) D1 R2 & mini" verfügbar und kann ausgewählt werden. <br>
Alle Werte behalten die Default Werte. Die Flash Size ist "4MB (FS:2MB OTA:~1019KB)" <br>
 <br>
Jetzt kann das Verzeichnis "WebMonitor_1" (siehe oben auf der Website) inklusive aller enthaltenen Dateien auf den lokalen Rechner kopiert werden. <br>
Verbindet man nun den PC über ein Micro-USB Kabel mit dem ESP8266, kann der Quellcode kompiliert und in den Mikrocontroller geschrieben werden. <br>
 <br>
<br>

## Quellcode
Das Hauptprogramm befindet sich in der Arduino Datei "WebMonitor_1.ino" <br>
Die Dateien "ESP_Settings.h" und "ESP_Settings.cpp" stellen die ESP8266 Website dar und steuern die Konfiguration im ESP8266 internen EEPROM. <br>
Die Dateien "TR064_Query.h" und "TR064_Query.cpp" beinhalten die Kommunikationsroutinen zur Steuerung der Bibliothek "TR-064-SOAP-Library". <br>
 <br>
Im Quellcode gibt es die Schwierigkeit, dass im Arduino Compiler die TR-064 Instanz erstellt werden muss bevor die Einstellungen aus dem EEPROM ausgelesen werden können. <br>
Deshalb wird zu Beginn eine Default-Instanz gebildet: <br>
* TR064_Query TR_064 = TR064_Query(49000, "192.168.178.254", "admin", ""); <br>
 <br>
Zur Laufzeit wird die Instanz gelöscht...  <br>
* TR_064.~TR064_Query(); <br>
 <br>
... und mit den EEPROM Daten wieder neu instanziert: <br>
* new(&TR_064) TR064_Query(49000, sRouterIP, sTR064_User, sTR064_Password); <br>
 <br>
Dies funktioniert leider nicht unter VS-Code unter PlatformIO. Hier ist mir noch keine Lösung gelungen. <br>
 <br>
<br>

## Funktion <br>
Der LCD Monitor zeigt die Verbindung zum WLAN vom Router und die Internet Verbindung an. <br>
Ein wandernder Punkt zeigt dabei an, dass die Kommunikation zum Router läuft und sich nicht aufgehängt hat. <br>
Bei Problemen wird der Teil der nicht erreichbar ist grau und ein Blitz-Symbol zeigt den vermuteten Ort des Problems an. <br>
Wenn ein Gastzugang geöffnet ist, wird neben dem Router ein Symbol mit zwei symbolisierten Personen angezeigt. <br>
Es gibt zwei Gitternetze, die den Upload (oben - Cyan) und Download (unten - Grün) grafisch über den Zeitverlauf (nicht justiert) anzeigen. <br>
Die Werte rechts neben den Gitternetze zeigen je nach Konfiguration die maximale eingestellte oder maximale reale Bandbreite. <br>
Zusätzlich wird die aktuelle Up- bzw. Download- Geschwindigkeit angezeigt. <br>
 <br>
Die Funtion wurde mit den Routermodellen Fritz!Box 7490, Fritz!Box 7530, Fritz!Box 7560 und Fritz!Box 7590 der Firma AVM getestet. <br>
Es sollten aber auch weitere Modelle des Herstellers funktionieren. <br>
 <br>
<br>

![beschreibung](images/display_beschreibung.png) <br>
<br>
 <br>
### *Zu den Einstellungen der Nutzerdaten und in der Fritz!Box siehe Verzeichnis "Quick and Easy"* <br>

<br>
<br>
=======================================================================================
<br>
<br>

## The development environment
Download and install the Arduino software (version 1.8.15) from https://www.arduino.cc. <br>
 <br>
Install the following Arduino libraries: <br>
* Adafruit GFX Library	(Version 1.10.10) <br>
* Adafruit BusIO			(Version 1.9.0) <br>
* Adafruit STMPE610		(Version 1.1.3) <br>
 <br>
Download and install the TR-064 libraries from: <br>
* https://github.com/Aypac/Arduino-TR-064-SOAP-Library (version: 1.1.0 - Feb 2020). <br>
This library is a great work by René Vollmer and handles the TR-064 communication to the router. <br>
To avoid modifying this library, TR064_Query.h and TR064_Query.cpp were written as an intermediate layer. <br>
 <br>
Download and install the TFT_eSPI libraries from: <br>
* https://github.com/Bodmer/TFT_eSPI (version: master - Jun 2024) <br>
Comprehensive library for easy integration of many TFT displays - written by Bodmer <br>
** some interesting and useful libraries can be found in his Github repositories <br>
** https://github.com/Bodmer?tab=repositories <br>
 <br>
In the Arduino IDE under "Preferences" in the field "Additional board manager URLs add the following entry: <br>
* https://arduino.esp8266.com/stable/package_esp8266com_index.json <br>
 <br>
Now you can install the "ESP Community" package in the Arduino IDE via the board manager: <br>
ESP8266 Community (Version 2.7.4) <br>
***ATTENTION: Currently you have to choose the older package. The packages version 3.x.x cause a conflict with the TR-064-SOAP-Library.*** <br>
 <br>
Now the board "LOLIN(WEMOS) D1 R2 & mini" is available in the Arduino IDE and can be selected. <br>
All values keep the default values. The Flash Size is "4MB (FS:2MB OTA:~1019KB)". <br>
 <br>
Now the directory "WebMonitor_1" (see above on the website) including all contained files can be copied to the local computer. <br>
If you now connect the PC to the ESP8266 via a micro USB cable, the source code can be compiled and written to the microcontroller. <br>
 <br>
<br>

## Source code
The main program is located in the Arduino file "WebMonitor_1.ino". <br>
The files "ESP_Settings.h" and "ESP_Settings.cpp" represent the ESP8266 website and control the configuration in the ESP8266 internal EEPROM. <br>
The files "TR064_Query.h" and "TR064_Query.cpp" contain the communication routines to control the library "TR-064-SOAP-Library". <br>
 <br>
In the source code there is the difficulty that in the Arduino compiler the TR-064 instance must be created before the settings can be read from the EEPROM. <br>
Therefore a default instance is created at the beginning: <br>
* TR064_Query TR_064 = TR064_Query(49000, "192.168.178.254", "admin", ""); <br>
 <br>
At runtime, the instance is deleted.... <br>
* TR_064.~TR064_Query(); <br>
 <br>
... and re-instantiated with the EEPROM data: <br>
* new(&TR_064) TR064_Query(49000, sRouterIP, sTR064_User, sTR064_Password); <br>
 <br>
Unfortunately this does not work under VS-Code under PlatformIO. I have not yet managed to find a solution here. <br>
 <br>
<br>

## Function
The LCD monitor shows the connection to the wifi of the router and the Internet connection. <br>
A moving dot indicates that the communication to the router is running and has not hung up. <br>
In case of problems, the part that is unreachable turns gray and a lightning icon indicates the suspected location of the problem. <br>
When a guest access is open, an icon with two symbolized people is displayed next to the router. <br>
There are two grids showing upload (top - cyan) and download (bottom - green) graphically over time (not adjusted). <br>
The values to the right of the grids show the maximum adjusted or maximum real bandwidth, depending on the configuration. <br>
In addition, the current upload or download speed is displayed. <br>
 <br>
The function was tested with the router models Fritz!Box 7490, Fritz!Box 7530, Fritz!Box 7560 and Fritz!Box 7590 from the company AVM. <br>
However, other models from the manufacturer should also work. <br>
 <br>
<br>

![description](images/display_beschreibung.png)
<br>

### *For the settings of the user data and in the Fritz!Box, see directory "Quick and Easy"* <br>
