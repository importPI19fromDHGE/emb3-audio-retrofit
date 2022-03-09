# Netzwerk-Audio mit Raspberry Pi als Retrofit Lösung

## Dokumentlinks

- die [Entscheidung zwischen Buildroot und Raspberry Pi OS](./docs/buildroot-vs-rpios.md)
- die [Testspezifikation](docs/test-specs.md)

## Produkt-Backlog

| Priorität | User Story | Schätzung Zeitaufwand \[h\] |
|---|---|---|
| 1 | Ich als Anwender möchte über das eingebettete System ein analoges Tonsignal ausgeben, um über ein angeschlossenes analoges Wiedergabegerät das Tonsignal abspielen zu können. | 2 |
| 2 | Ich als Anwender möchte eine Bluetooth-Verbindung zum eingebetteten System herstellen, um Bluetooth als Audio-Quelle zu verwenden. | 3 |
| 1 | Ich als Anwender möchte eine Spotify-Connect-Verbindung zum eingebetteten System herstellen, um Spotify Connect als Audio-Quelle zu verwenden. | 2 |
| 2 | Ich als Anwender möchte eine UPnP-Verbindung zum eingebetteten System herstellen, um mit Hilfe von UPnP MP3-Dateien wiederzugeben. | 3 |
| 8 | Ich als Anwender möchte das eingebettete System schnell über ein angepasstes Betriebssystem-Image auf die microSD-Karte des eingebetteten Systems bereitstellen können, um es leicht vervielfältigen zu können. | 8 |
| 4 | Ich als Anwender möchte das eingebettete System einfach mit Hilfe von LAN oder WLAN in mein eigenes Netzwerk integrieren können, um UPnP und Spotify Connect nutzen zu können. | 8 |
| 7 | Ich als Bastler möchte zwischen dem HiFiBerry DAC 2 Pro und dem internen DAC wechseln können, um das System auf meine individuellen Bedürfnisse anzupassen. | 8 |
| 6 | Ich als Anwender möchte Software-Updates von Betriebssystem und verwendeten Software-Bibliotheken automatisch erhalten, um von den neuesten Software-Versionen zu profitieren. | 3 |
| 3 | Ich als Anwender möchte eine Schnellstartanleitung erhalten, um über die erforderlichen Einstellungen informiert zu sein. | 4 |
| 8 | Als Anwender möchte ich die Lautstärke über eine App auf meinem Android-Telefon steuern können, um nicht auf die Steuerung der Musik-Anlage und der Kommandozeile der Lösung angewiesen zu sein. | 20 |

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
