# Netzwerk-Audio mit Raspberry Pi als Retrofit Lösung

## Dokumentlinks

- die [Entscheidung zwischen Buildroot und Raspberry Pi OS](./docs/buildroot-vs-rpios.md)
- die [Testspezifikation](docs/test-specs.md)

## Produkt-Backlog

| ID | Priorität | User Story | Schätzung Zeitaufwand \[h\] |
|---|---|---|---|
| 0 | 1 | Ich als Anwender möchte über das eingebettete System ein analoges Tonsignal ausgeben, um über ein angeschlossenes analoges Wiedergabegerät das Tonsignal abspielen zu können. | 2 |
| 1 | 2 | Ich als Anwender möchte eine Bluetooth-Verbindung zum eingebetteten System herstellen, um Bluetooth als Audio-Quelle zu verwenden. | 3 |
| 2 | 1 | Ich als Anwender möchte eine Spotify-Connect-Verbindung zum eingebetteten System herstellen, um Spotify Connect als Audio-Quelle zu verwenden. | 2 |
| 3 | 2 | Ich als Anwender möchte eine UPnP-Verbindung zum eingebetteten System herstellen, um mit Hilfe von UPnP MP3-Dateien wiederzugeben. | 3 |
| 4 | 8 | Ich als Anwender möchte das eingebettete System schnell über ein angepasstes Betriebssystem-Image auf die microSD-Karte des eingebetteten Systems bereitstellen können, um es leicht vervielfältigen zu können. | 8 |
| 5 | 4 | Ich als Anwender möchte das eingebettete System durch eine LAN- oder WLAN-Verbindung in ein Netzwerk integrieren, um über UPnP und Spotify Connect Audio wiederzugeben. | 8 |
| 6 | 7 | Ich als Bastler möchte zwischen dem HiFiBerry DAC 2 Pro und dem internen DAC wechseln können, um das System auf meine individuellen Bedürfnisse anzupassen. | 8 |
| 7 | 6 | Ich als Anwender möchte Software-Updates von Betriebssystem und verwendeten Software-Bibliotheken automatisch erhalten, um von den neuesten Software-Versionen zu profitieren. | 3 |
| 8 | 3 | Ich als Anwender möchte eine Schnellstartanleitung erhalten, um über die erforderlichen Einstellungen informiert zu sein. | 4 |
| 9 | 8 | Als Anwender möchte ich die Lautstärke über eine App auf meinem Android-Telefon steuern können, um nicht auf die Steuerung der Musik-Anlage und der Kommandozeile der Lösung angewiesen zu sein. | 20 |

## Technische Spezifikationen zu Produkt-Backlog

### Wiedergabe eines analogen Tonsignals

Referenz zu User-Story-ID: 0

- es erfolgt eine Ausgabe eines analogen Tonsignals über die auf dem DAC vorhandenen Ausgabeports
  - für das HiFiBerry DAC2 Pro: Stereo 3,5 mm Klinkenanschluss, Stereo Cinch
  - für den Raspberry Pi integrierten DAC: Stereo 3,5 mm Klinkenanschluss
- Die Linux-Komponente [ALSA](https://de.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture) steuert den Treiber des DACs an, um ein digitales Tonsignal daran zu senden

### Herstellen einer Bluetooth-Verbindung

Referenz zu User-Story-ID: 1

- mit Hilfe von Bluetooth-fähigen Android-, IOS-, Linux- und Windows-Endgeräten soll ein digitales Tonsignal an das eingebettete System gesendet werden können
- das eingebettete System kann in den Kopplungsmodus wechseln, um neue Geräte zu koppeln
- das eingebettete System speichert bereits gekoppelte Geräte ab, um diese erneut zu verbinden
- es sollte nur maximal ein Gerät gleichzeitig mit dem eingebetteten System verbunden sein
- das eingehende digitale Audiosignal wird mit Hilfe des PulseAudio Bluetooth Moduls verabeitet

### Herstellen einer Spotify-Connect-Verbindung

Referenz zu User-Story-ID: 2

- Wiedergabequelle und das eingebettete System befinden sich im gleichen Subnetz ohne Netzwerkrestriktionen des LAN-zu-LAN-Verkehrs
- Verbindung zwischen Wiedergabequelle und dem eingebetteten System wird aufgebaut
- für die Verwendung von Spotify Connect ist eine Internet-Verbindung notwendig, um zu den Spotify-Servern zu verbinden und Musik zu streamen

### Herstellen einer UPnP-Verbindung

Referenz zu User-Story-ID: 3

- Wiedergabequelle und das eingebettete System befinden sich im gleichen Subnetz ohne Netzwerkrestriktionen des LAN-zu-LAN-Verkehrs
- Verbindung zwischen Wiedergabequelle und dem eingebetteten System wird aufgebaut

### Bereitstellung des angepassten Betriebssystem-Images

Referenz zu User-Story-ID: 4

- das eingebettete System soll über ein Image bereitgestellt werden können
- das Image soll als IMG-Datei abliegen
- das Image enthält alle Partitionen und den Bootsektor, der für den Betrieb nötig ist
- das Image wird mit Hilfe des Tools ``dd`` erzeugt
- das Image soll sowohl mit Hilfe von Linux oder Windows auf die microSD-Karte geflasht werden können

### Netzwerkverbindung des eingebetteten Systems

Referenz zu User-Story-ID: 5

- das eingebettete System soll per LAN oder WLAN mit einem IP-Netzwerk verbunden werden können
- das eingebettete System soll eine automatische IP-Konfiguration per DHCP erhalten

### Wechsel des DACs

Referenz zu User-Story-ID: 6

neuer Absatz

### Update-Installation des eingebetetteten Systems

Referenz zu User-Story-ID: 7

neuer Absatz

### Lautstärkeregelung mit Hilfe einer Android-App

Referenz zu User-Story-ID: 8

neuer Absatz

## Meilensteine

Wir benutzen die Github Milestones Funktion [hier](https://github.com/importPI19fromDHGE/emb3-gulla-kerst/milestones?with_issues=no).

## Bestellliste

| ID | Artikel | Menge | Quelle | Einzelpreis | Händler |
| -: | ------- | ----- | ------ | ----------- | ------- |
| 0 | Raspberry Pi 4B 4GB Elementary Kit | 1 | https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/kits/raspberry-pi-4-computer-modell-b-4gb-elementary-kit | 69,50€ | BerryBase |
| 1 | SanDisk MicroSD-Karte 32GB | 1 | https://www.berrybase.de/raspberry-pi/raspberry-pi-computer/speicherkarten/sandisk-extreme-micro-sdhc-a1-uhs-i-u3-speicherkarte-43-adapter-32gb?c=183 | 8,85€ | BerryBase |
| 2 | HiFiBerry DAC2 Pro | 1 | https://www.hifiberry.com/shop/boards/hifiberry-dac2-pro/ | 39,90€ | HiFiBerry |
| 3 | Gehäuse für Raspberry Pi 4 mit HiFiBerry DAC | 1 | Yannis | *nach Vereinbarung*<!--1 Kasten Bier--> | Yannis |

## Orga: Git-Submodule

Dieses Projekt enthält Git Submodule.
Diese erfordern ein gesondertes Vorgehen verglichen mit den restlichen Inhalten dieses Repos:

- sollen beim Auschecken gleich alle Submodule mit ausgecheckt werden, muss rekursiv geklont werden: ``git clone --recurse-submodules <repo-url>``
- Um lustige Konflikte in Git zu vermeiden, sind alle Änderungen an den Submodulen bitte in ihren jeweiligen Haupt-Repos durchzuführen und hier zu pullen

Wenn Git Submodule bisher gänzlich unbekannt sind, ist ein Blick auf die [Dokumentation](https://git-scm.com/book/en/v2/Git-Tools-Submodules) empfehlenswert.
