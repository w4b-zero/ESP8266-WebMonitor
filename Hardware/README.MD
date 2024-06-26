# Schaltung und Layout / Circuit and layout
Die Schaltung und das Layout sind mit dem CAD-Programm Target3001! gezeichnet worden.
Das Programm kann in einer kostenlosen Version fürs Hobby bei https://ibfriedrich.com heruntergeladen werden.
<br>
<br>
The circuit and the layout have been drawn with the CAD program Target3001!
The program can be downloaded in a free version for hobby at https://ibfriedrich.com.
<br>
<br>

## Der Stromlaufplan / The schematic
Der Stromlaufplan ist sehr einfach gehalten. Im Grunde genommen ist nur eine Display Baugruppe "TJCTM24028-SPI" an das Board "Wemos ESP8266 D1 mini" angeschlossen.
<br>
Die Touch-Funktion vom Display ist zwar angeschlossen, wird aber für dieses Projekt nicht genutzt.
Der SD-Card Anschluss des Display Boards ist ebenfalls angeschlossen.
Er war ursprünglich zum Speichern der Konfigurationsdaten vorgesehen, wird aber in diesem Projekt ebenfalls nicht genutzt.
Die beiden LEDs inklusive ihrer Vorwiderstände wurden nur zum Debugging genutzt und haben keine richtige Funktion mehr. 
<br>
Die Schaltung besitzt vier USB Anschlüsse mit unterschiedlichen Steckerverbindern und Ausrichtungen.
Sie dienen zur Spannungsversorgung des Boards. Es wird aber in der Praxis nur eine Buchse benötigt. Der Rest ist optional verfügbar.
Sie dienen nur dazu für den jeweiligen Einbauort die beste Variante auswählen zu können.
Man kann natürlich auch auf alle USB-Buchsen verzichten und die Schaltung über die Mini-USB Buchse des "Wemos ESP8266 D1 mini" versorgen.
<br>
<br>

The schematic is very simple. Basically only a display module "TJCTM24028-SPI" is connected to the board "Wemos ESP8266 D1 mini".
<br>
The touch function from the display is connected but not used for this project.
The SD card connector of the display board is also connected.
It was originally intended for saving configuration data, but is also not used in this project.
The two LEDs including their series resistors were only used for debugging and have no real function anymore. 
<br>
The circuit has four USB ports with different connectors and orientations.
They are used to supply power to the board. However, only one connector is needed in practice. The rest is optional.
They serve only to be able to select the best variant for the respective installation place.
Of course, you can also do without all USB sockets and supply the circuit via the mini-USB socket of the "Wemos ESP8266 D1 mini".
<br>
<br>

![grafik](https://user-images.githubusercontent.com/88629497/132067967-2f39bc58-325b-4394-a611-8a7c63af4411.png)
<br>
<br>

## Das Board / The board

Die Datei "WebMonitor_1.T3001" ist mit der Software "Target 3001!" erstellt worden und beinhaltet das gesamte Hardware-Projekt, um es individuell modifizieren zu können.
Wer das Board einfach nur nachbauen möchte, kann die Datei "WebMonitor_1_Gerber_Files.zip" an einen Leiterplattenhersteller schicken, um sich Leiterplatten fertigen zu lassen. Dabei bitte beachten, dass die einzelnen Layer vom Hersteller richtig übernommen werden können. Die Zuordnung der Dateien zu Layern kann der Datei "WebMonitor_1.Info" (in der Zip-Datei enthalten) entnommen werden. Das Layout ist 10x10cm groß, weil die meisten Hersteller bis zu dieser Größe recht günstige Leiterplatten anbieten.
<br>

Die Stückliste kann den Dateien "WebMonitor_1_BOM.pdf" bzw. "WebMonitor_1_BOM.xlsx" entnommen werden. Alle Teile sowie Bezugsquellen sind als Vorscläge zu sehen. Es können natürlich auch kompatible Bauteile eingesetzt werden.
<br>
<br>

The file "WebMonitor_1.T3001" has been created with the software "Target 3001!" and contains the whole hardware project to modify it individually.
If you just want to rebuild the board, you can send the file "WebMonitor_1_Gerber_Files.zip" to a PCB manufacturer to have PCBs made. Please note that the individual layers can be taken over correctly by the manufacturer. The assignment of the files to layers can be taken from the file "WebMonitor_1.Info" (included in the zip file). The layout is 10x10cm because most manufacturers offer quite cheap PCBs up to this size.
<br>

The parts list can be found in the files "WebMonitor_1_BOM.pdf" or "WebMonitor_1_BOM.xlsx". All parts as well as sources of supply are to be seen as suggestions. Of course, compatible parts can also be used.

![grafik](https://user-images.githubusercontent.com/88629497/132068330-f04bb45b-dc5b-46f8-8620-b2b8d2f60e1a.png)



