# Status API

## Zustand
Der Zustand eines einzelnen Channels kann entweder an oder aus sein. Zum Abfragen des Zustandes *(active)* soll der Endpunkt `GET /state/{channelName}` dienen. Eine Zustandsänderung kann über `POST /state/{channelName}` vorgenommen werden. Dabei kann der neue Zustand nicht näher definiert werden. Es findet lediglich ein Toggle statt, der zu einer Zustandsänderung auf *!active* führt.

Zudem sollte ein Endpunkt `POST /state` dafür sorgen, dass alle LEDs ausgehen, sollte mindestens eine aktiv sein oder alle angehen, sollte keine aktiv sein.

## Zustandsdetails
Neben dem eigentlichen 