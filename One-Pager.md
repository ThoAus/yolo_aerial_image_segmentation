# One-Pager

## Ziel
In der Flugaufnahme sollen die folgenden Objekte lokalisiert werden:

- Autos
- Solaranlagen
- Bäume

Soll als Objekterkennung und auch Segmentierung erfolgen. Ergänzend zur Aufgabenstellung soll das trainierte Modell in QGIS verwendet werden um entsprechende Lagepläne zu erstellen.

## Datensatz
Bilder werden vom WMS-Diesnst der Provinz BZ heruntergeladen. Abmessung der Bilder soll 640x640 betragen wie für YOLO... durch die Auflösung von 20 cm pro Pixel ergibt sich dadurch eine reale Größe von XXX x XXX Meter. Werden Bilder von verschiedenen Jahren verwendet. Herunterladen der Daten mit

## Annotation
wird mit der Software XXX durchgeführt.

## Anwendung in QGIS
Modell wird als ONNX exportiert. Objekterkennung durchgeführt und Lageplan von relevanten Bereichen für verschiedenen Jahre erstellt und Ergebnis verglichen (besonders für Solaranlagen).

## Zusatz
Segmentierung der Bilder mit klassischem U-Net und vergleich der Ergebnisse; es handelt sich hierbei um semantische segmentierung und nicht objekterkennung. Sollte für die Aufgabe der Erkennung Solaranlagen ausreichen.

## Ergebnis

Bei 'RUN_6' werden viele Obstplantagen als 'Solar' erkannt. Vermutlich weil ein ähnliches Streifenmuster oder Raster erkannt wird. Bei der Auswahl der Trainingsdaten mit Ausreichend Beispielen und Negativbeispielen zu berücksichtigen.

<img src="images/image_test_1.png" alt="drawing" width="400"/>



## Probleme
Teilweise nicht perfekt von oben, auch fassaden ersichtlich > was wird markiert? nur die dachfläche oder generell das Gebäude? Im vorliegenden Fall das Gebäude
Grundsätzlich sehr verschiedene Oberflächen und strukturen, Satteldach mit Ziegeln bis hin zu begrünten falchdach. Letzteres schwierig von wiese zu unterscheiden. Bei Solaranlagen ist struktur grundsötzlich ähnlicher, kommt weniger oft vor.

## Links
- [Webseite zur Lehrveranstaltung](https://mciwing.github.io/)
- [Arbeiten mit virtuellen Umgebung](https://mciwing.github.io/python/packages/)
- [MapView - Darstellung und Download der Orthofotos](https://mapview.civis.bz.it/)
- [owslib - Bibliothek zum Arbeiten mit WMS](https://owslib.readthedocs.io/en/latest/usage.html#wms)

## Arbeitsschritte und Notizen

#### 11. April
- GitHub Repo erstellt
- Konzept und Struktur für Projekt erarbeitet
- Erste Versuche zum Downloaden der Bilder vom WMS-Dienst

#### 14. April
- Label-image installieren und Projekt erstellen

#### 15. April
- Download Bilder von WMS-Dienst im Raster um angegebenen Mittelpunkt
- Bilder in Lable-image importieren und erste Versuche damit
- Erster Datensatz mit 25 Bilder:
    - Lana, Boznerstraße - CFG.RASTER_CENTER = (1242660, 5878955), CFG.RASTER_SIZE = (5, 5)
- Segmentierungsmaske für 25 Bilder erstellen (Solar, Roof, Pool)

#### 16. April
- Training mit kleinem Datensatz (20 + 5 Bilder)
    - Modell 'yolo11m-seg.pt'
    - 50 Epochen
    - Segmentierung funktioniert prinzipiell, Ergebnis besser als erwartet
- Installation XXX Plugin für QGIS
    - Problem beim Laden des ONNX-Modell, Fehlermeldung zu prüfen

#### 17. April
- Download weiterer Bilder:



