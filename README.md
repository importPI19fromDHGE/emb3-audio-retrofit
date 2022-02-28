# Netzwerk-Audio mit Raspberry Pi als Retrofit Lösung

## Produkt-Backlog

| Priorität | User Story | Schätzung Zeitaufwand \[h\] |
|---|---|---|
| 2 | Ich als Anwender möchte per Bluetooth auf meiner analogen HiFi-Anlage Musik abspielen, um über verschiedene Quellen drahtlos Musik abspielen zu können. | 3 |
| 1 | Ich als Anwender möchte eine Lösung, um mit Spotify Connect Musik auf meiner analogen HiFi-Anlage abspielen zu können. | 2 |
| 2 | Ich als Anwender möchte eine Lösung, um mit UPNP Musik auf meiner analogen HiFi-Anlage abspielen zu können. | 3 |
| 8 | Ich als Anwender möchte eine leicht vervielfältigbare Lösung, um diese beliebig oft neu in Betrieb nehmen zu können | 8 |
| 4 | Ich als Anwender möchte das eingebettete System einfach in mein eigenes Netzwerk integrieren können, um die Lösung mit wenig Zeitaufwand nutzen zu können. | 8 |
| 7 | Als Bastler möchte ich den DAC wechseln können, um das System auf meine individuellen Bedürfnisse anzupassen. | 8 |
| 6 | Ich als Anwender möchte SW-Updates erhalten, um die Lösung länger nutzen zu können und von den neuesten SW-Versionen zu profitieren. | 3 |
| 3 | Ich als Anwender möchte keine komplexen Einstellungen vornehmen müssen, um die Lösung in Betrieb zu nehmen. | 4 |
| 8 | Als Anwender möchte ich die Lautstärke über mein Android-Telefon steuern können, um nicht auf die Steuerung der Anlage und die Kommandozeile der Lösung angewiesen zu sein | 20 |

## Meilensteine

Wir benutzen die Github Milestones Funktion [hier](https://github.com/importPI19fromDHGE/emb3-gulla-kerst/milestones?with_issues=no).

## Orga: Git-Submodule

Dieses Projekt enthält Git Submodule.
Diese erfordern ein gesondertes Vorgehen verglichen mit den restlichen Inhalten dieses Repos:

- sollen beim Auschecken gleich alle Submodule mit ausgecheckt werden, muss rekursiv geklont werden: ``git clone --recurse-submodules <repo-url>``
- Um lustige Konflikte in Git zu vermeiden, sind alle Änderungen an den Submodulen bitte in ihren jeweiligen Haupt-Repos durchzuführen und hier zu pullen

Wenn Git Submodule bisher gänzlich unbekannt sind, ist ein Blick auf die [Dokumentation](https://git-scm.com/book/en/v2/Git-Tools-Submodules) empfehlenswert.
