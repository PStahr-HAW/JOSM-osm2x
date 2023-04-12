# Shared Guide Dog 4.0 Map Creator Plugin for [JOSM](https://josm.openstreetmap.de)

[![license: GPLv2 or later](https://img.shields.io/badge/license-GPLv2_or_later-blue.svg?style=flat-square&maxAge=7200)](/GPL-v2.0.txt)

A plugin that prepares and exports OSM data for use on the [Shared Guide Dog 4.0](https://www.haw-hamburg.de/forschung/forschungsprojekte-detail/project/project/show/shared-guide-dog-40/).


* Maintainers:
  * Pascal Stahr <pascal.stahr@haw-hamburg.de>
* License: [GPL v2 or later](./LICENSE.md)


# Einleitung

Das JOSM Plugin *Shared Guide Dog 4.0 Map Creator* unterst�tzt bei der Verarbeitung von OpenStreetMap Karten f�r den Shared Guide Dog 4.0 (SGD4.0). Das Plugin erm�glicht den Export von Hinderniskarten und bei der Generierung und dem Export von Wegenetzen. Die exportierten Daten k�nnen direkt auf dem SGD4.0 genutzt werden.

Nach dem Laden einer OSM-Karte kann das Plugin aus der linken Toolbar aufgerufen werden. Auf der rechten Seite erscheint das Hauptfenster des SGD4.0 Map Creator Plugins. Das Fenster teilt sich in eine Anzeigefl�che und drei Buttons. In der Anzeigefl�che werden Daten zur geladenen Karte angezeigt. Mit den Buttons k�nnen die Funktionen des Plugins aufgerufen werden.

![Main window of the Shared Guide Dog 4.0 Map Creator plugin](/doc/main_window.png)

Funktionen der Buttons:
- Count Nodes: Berechnet die angezeigten Statistiken neu
- Split: Teilt die Karte in eine Hinderniskarte und eine Highway-Karte
- Mesh: Vernetzt die Highwaykarte (siehe [Meshing](Readme.md#generierung-und-export-eines-wegenetzes))

# Export von Hinderniskarten

## Vorbereitungen

Durch einen Klick auf den Split-Button wird eine Hinderniskarte und eine Wegkarte erstellt. Die Hinderniskarte enth�lt alle Hindernisse, wie beispielsweise Geb�ude, Poller, Schranken, W�nde und vieles mehr. Grundlage f�r die Aufteilung in Hindernis und Wege sind Filter, die �ber die Einstellungen angepasst werden k�nnen. 

![Preferences window](/doc/preferences_barrier.png)

Der Standard-Filter f�r die Hinderniskarte lautet: `barrier=* | natural=* | building=*`
Der Filter kann je nach Bed�rfnis angepasst werden. Es wird die gleiche Syntax wie f�r den JOSM Filter verwendet.
Die Checkbox _Copy address to node_ erm�glicht, dass die Attribute der Geb�ude zu den Entrance-Nodes kopiert werden. Im Normalfall ist dieses Verhalten erw�nscht, da die Adressen f�r die Wegplanung ben�tigt werden und dann einzelnen Knoten zugeordnet sein m�ssen.

## Export

Die folgende Grafik zeigt die Hinderniskarte in JOSM nach dem Splitting. Vor dem Export muss die Karte in den meisten F�llen noch angepasst werden. Zu beachten ist, dass zum Beispiel Baumreihen, die durch einen Weg in OSM dargestellt werden, als Wand exportiert werden w�rden. Hier m�ssen demnach der Weg entfernt und einzelne Nodes gesetzt werden.

![Barrier map in JOSM](/doc/barrier_map.png)

Ist die Karte fertig bearbeitet, erfolgt der Export als Scalable Vector Graphic (SVG). Damit geht keine Genauigkeit durch eine Rasterisierung verloren und das Bild kann mit jedem �blichen Vektoreditor bearbeitet werden. Die Karte nach dem Export ist in der folgenden Grafik dargestellt. Zu beachten ist die Baumreihe auf der rechten Seite, die nun durch einen Strich dargestellt ist.

![Barrier map after exporting to svg](/doc/barrier_map_svg.png)


## Datenformat

Als Datenformat f�r den Export wird das Scalable Vector Graphics (SVG) Format verwendet. Es erm�glicht die effiziente Speicherung von gro�en Karten und die einfache Bearbeitung und Anzeige durch verschiedenste Programme.

Die Karte f�r den Shared Guide Dog 4.0 besteht aus den svg Elementen _circle_ und _path_. Neben den Positionsinformationen erh�lt jedes Objekt eine Klasse zugewiesen. Die Klasse leitet sich aus den OSM-Attributen ab. So wird beispielsweise aus einem Baum mit dem Attribut _natural=tree_ die Klasse _natural-tree_. Diese Klassen werden vom Shared Guide Dog 4.0 genutzt, um die Objekte zu klassifizieren. Zus�tzlich wird �ber CSS Styles die Darstellung im Editor gesetzt. Dabei handelt es sich lediglich um eine graphische Hilfe, die Styles werden nicht vom Shared Guide Dog 4.0 verwendet.

![SVG export format](/doc/svg_export.png)

Zus�tzlich zur Bilddatei wird eine yaml-Datei erstellt, die weitere Daten �ber das Bild enth�lt. Diese Daten werden vom Map Server des SGD4.0 verwendet.

# Generierung und Export eines Wegenetzes


# Known limitations and bugs
