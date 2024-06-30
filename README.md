# WebMonitor
Original Code von: <br> 
 * Autor: Jörg Bernhardt<br>
 * Datum: 11/2020<br>
 * Source: https://github.com/Joerg-66/ESP8266-WebMonitor<br>
<br>
 Änderungen by zeroTM<br>
 
# Version: 1.3+z1.1
 Datum: 30/06/2024<br>
 <br>
   Änderungen
   ++ FastLED Library (3.7.0) <br>
   ++ 8 WS2812b Leds<br>
      Pin4[SD_CS] genutzt (leitung getrennt und Jumper hinzugefügt)<br>
   ++ Grüne LED als Power/Boot Indicator (Boot: blinkend, Internet erkannt: on, Internet getrennt: blinkend)<br>
      Pin0[T_CS] genutzt (leitung getrennt und Jumper hinzugefügt)<br>
   ++ Rote LED als TR064-Kommunikations Indicator (bei TR064 aufrufen blinkend)<br>
      Pin16[T_IRQ] genutzt (leitung getrennt und Jumper hinzugefügt)<br>
 <br>   

# Version: 1.3+z1 
 Datum: 06/2024<br>
 <br> 
   Änderungen: <br> 
   -- Adafruit ILI9341<br>
   ++ TFT_eSPI Bibliothek (mehrere Displays unterstützt!)<br>
   -- ILI9341_Graphic.h (class komplett entfernt)<br>
   -- ILI9341_Graphic.cpp (void-Funktionen in WebMonitor_1.ino eingefügt)<br>
   <br>

## Die Entwicklungsumgebung
Lade und installiere von der Seite https://www.arduino.cc die Software Arduino (Version 1.8.15) <br>
 <br>
Istalliere die folgenden Arduino Bibliotheken: <br>
* Adafruit GFX Library	(Version 1.10.10) <br>
* Adafruit BusIO	(Version 1.9.0) <br>
* Adafruit STMPE610	(Version 1.1.3) <br>
* FastLED Library 	(Version 3.7.0) <br>
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
* ESP8266 Community		(Version 2.7.4) <br>
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
*Hinweis: "Fritz!Box" ist ein Markenname der Firma AVM GmbH in Berlin*
<br>
 <br>
![beschreibung](images/IMG_20240630_201146.jpg) <br>
<br>
 <br>
### *Zu den Einstellungen der Nutzerdaten und in der Fritz!Box siehe Verzeichnis "Quick and Easy"* <br>

## Ziele

* Überprüfung ob die Internetverbindung steht
* WLAN Verfügbarkeit
* Erkennung ob ein Gastzugang aktiv ist
* max. Upload Bandbreite
* aktuelle Upload Rate
* Upload Überblick der letzten Minuten
* max. Download Bandbreite
* aktuelle Download Rate
* Download Überblick der letzten Minuten

# todo...

* auf Platformio wechseln<br>
* ESP32 unterstützung<br>
* Konfiguration erweitern(Einstellungen editierbar machen, Einstellungen erweitern)<br>
* Touchscreen unterstützung (Pins derzeit genutzt für LEDs)<br>
* Router Statistik<br>
* Call-Monitor<br>
<br>

![MINI-PC_01](images/IMG_20240630_201604.jpg)<br>
![MINI-PC_02](images/IMG_20240630_201218.jpg)<br>


