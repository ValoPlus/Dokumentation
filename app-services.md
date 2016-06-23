# Valo+ App Services
Dieses Dokument beschreibt den allgemeinen Aufbau der App. Eine Dokumentation der Klassen ist unter [App-Doku](http://valoplus.de/appdoku) zu finden.

## i18n

i18n Support wird mittels ng2-translate umgesetzt. Die Sprachdateien liegen in `www/assets/i18n`. Dabei nutzen die Dateien einen jeweils Namensräume. Jeder Namensraum entspricht dabei einer *Component*. Die im Folgenden abgebildete Datei definiert die beiden Strings *TITLE* und *ADD_DEVICE* für die Component *start*.

```
{
  "START": {
    "TITLE" : "VALO+",
    "ADD_DEVICE" : "Gerät hinzufügen"
  }
}
```

Zum übersetzen von Texten in der App kann die Direktive **VpTranslateComponent** verwendet werden.

```
<vp-translate key="START.TITLE"></vp-translate>
```

## Zugriffe auf ein Device
Operationen auf Devices sollten nur über Services erfolgen.

- **StoreService**