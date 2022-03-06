# Vergleich von Buildroot und Raspberry Pi OS

Zu Beginn des Projekts muss die Software-Plattform festgelegt werden.
Dabei stehen Buildroot und Raspberry Pi OS zur Wahl.
Buildroot ist ein Bereitstellungstool für eingebettete Systeme.
Es stehen vordefinierte Software-Pakete zur Auswahl, welche installiert und parametriert werden können.
Es ist für einen minimalen Betriebssystem-Overhead optimiert.
Nicht nativ unterstützte Software muss unter erhöhtem Aufwand manuell hinzugefügt werden.

Raspberry Pi OS ist das von der Raspberry Foundation offiziell herausgegebene Betriebssystem für nach heutigem Stand alle Versionen des Raspberry Pi.
Es zeichnet sich durch im Gegensatz zu Buildroot höhere Flexibilität aus, kommt allerdings auch mit einem deutlich erhöhten Overhead daher, da viele Software-Komponenten für das Projekt nicht benötigt werden.
Der Overhead bezieht sich sowohl auf die Image-Größe, als auch auf die Ressourcenbelegung während des Betriebs.
Raspberry Pi OS bietet die Möglichkeit, Updates zu installieren.
Bei der Verwendung von Buildroot ist dies nur möglich, sofern das Image neu gebaut und geflasht wird.

Auf Grund des begrenzten zeitlichen Rahmens und der hohen Komplexität des Projekts, wird als Basis das Raspberry Pi OS verwendet.
Dieses weist eine höhere Kompatibilität zu Dritthersteller-Komponenten wie das verwendete HiFiBerry DAC 2 Pro auf.
Der Fokus des Projekts liegt auf der Bereitstellung einer vielseitig einsetzbaren Audiolösung statt auf geringem Ressourcenbedarf.