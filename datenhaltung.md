# Datenhaltung und Strukturen
Im folgenden soll auf die Datenhaltung in der Valo+ App eingegangen werden.

## Datenstrukturen
Neben den eigentlichen Devices (Ein Device = 1 Hardware Controller) können auf dem Client einzelne Deviceübergreifende Gruppen erstellt werden. Diese Gruppen werden nicht mit den Controllern Syncronisiert.

- Device
	- Channel
		- Status
		- (LED)
- Gruppe
	- Device
	- Channel

## Datenbank
Als Datenbanksystem wird die noSQL Datenbank **pouchdb** genutzt. Die Persistierung erfolgt lokal.
Eine Persistierung erfolgt für folgende Objekte:

- Device
- Channel
- Connection

##Datenaktualisierung

In verschiedenen Zuständen der App erfolgt eine Aktualisierung der lokalen Daten. Dabei wird ein lokaler Zeitstempel der letzten Änderung mit dem auf dem Controller abgeglichen, um zu ermitteln, ob es geänderte Daten gibt. Nur falls ja wird auch wirklich eine Aktualisierung durchgeführt.

1. **Start der App** (platform.ready()): Für alle lokalen Devices wird eine Abfrage nach der letzten Datenänderung auf dem Controller gestartet. Controller, welche nicht antworten, sollen an dieser Stelle als nicht aktiv/erreichbar markiert werden und sind nicht aufrufbar. Controller, an denen die authorisierung Fehschlägt, sollen eine möglichkeit zur neuen Authorisierung oder zur Löschung bieten. Bei anderen Fehlern ist ein erneuter Versuch oder das Löschen möglich.

2. **Aufruf eines Channels** (DetailChannelPage.onPageWillEnter()): Nur für dieses Device findet eine Überprüfung statt. Falls eine Änderung vorliegt werden alle Channel neu abgerufen. Zudem wird der Channel nicht geöffnet, sondern eine Nachricht erscheint.

3. **Manuelle Aktualisierung der Stati**: Auf der Startseite kann der Status aller Devices manuell erneut abgerufen werden. Hierbei soll die Prozedur aus 1. erneut erfolgen.

### Fehlerfälle
Falls eine Aktualisierung eines Channels oder dessen Status von dem Device nicht verarbeitet werden kann (Weil der Channel geändert oder nicht mehr vorhanden ist), muss entsprechend eine Aktualisierung des Devices durchgeführt werden und eine Nachricht angezeigt.

### Syncronisierung zwischen Clients
Eine solche Syncronisierung ist im ersten Schritt nicht vorgesehen.

## Nicht Persistierte Daten
Daten, die sich häufig ändern, werden nicht persistiert. Dazu gehört der aktuelle Status aller Channel der Devices, die Einstellungen für jeden Channel sowie die WLAN Einstellungen der Devices.

### Datenaktualisierung
1. **Start der App** (platform.ready()): Der Status aller Devices werden abgerufen.
2. **Aufruf eines Channels** (DetailChannelPage.onPageWillEnter()): Für den Channel werden die Einstellungen abgerufen.
3. **Manuelle Aktualisierung der Stati**: Auf der Startseite kann der Status aller Devices manuell erneut abgerufen werden. Hierbei soll die Prozedur aus 1. erneut erfolgen.