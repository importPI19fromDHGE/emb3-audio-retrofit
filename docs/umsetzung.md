# Projekt-Umsetzung

## Betriebssysteminstallation

Zu Beginn des Projekts wird die neueste Version des Raspberry Pi OS Lite in der 64-Bit-Version (Version 11 vom 28.01.2022) von [Raspberry Pi](https://www.raspberrypi.com/software/operating-systems/) heruntergeladen.
Das heruntergeladene Image wird mit Hilfe von Balena Etcher auf die SD-Karte geflasht. Die Software kann unter [Balena Etcher](https://www.balena.io/etcher/) heruntergeladen werden.

Anschließend sind weitere Schritte erforderlich, um den Raspberry Pi automatisch einem WLAN-Netzwerk hinzuzufügen und den SSH-Server zu aktivieren.
Dazu wird mit einer beliebigen Dateiverwaltung zu der Boot-Partition navigiert.
Für die Aktivierung des SSH-Servers wird die Datei ``ssh`` erstellt.
Zur Konfiguration des WLAN-Clients wird die Datei ``wpa_supplicant.conf`` erstellt und anschließend konfiguriert.

```txt
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="[SSID des WLAN-Netzwerks]"
    psk="[Kennwort des WLAN-Netzwerks]"
}
```

Vgl. [Raspberry Foundation](https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi)

Daraufhin erfolgt Konfiguration des zusätzlichen DAC-Hats. Innerhalb der Datei ``config.txt`` wird die Zeile ``dtparam=audio=on`` auskommentiert und die Zeile ``dtoverlay=hifiberry-dacplus`` ergänzt.

Vgl. [HiFiBerry](https://www.hifiberry.com/docs/data-sheets/datasheet-dac2-pro/)

Somit sind alle erforderlichen Einstellungen konfiguriert. Die SD-Karte kann nun in den Raspberry Pi eingebaut werden.

Auf dem WLAN-Router ist ein neues DHCP-Lease ersichtlich. Per SSH kann unter Angabe der IP-Adresse erfolgreich eine Verbindung zu dem Raspberry Pi aufgebaut werden.

## Basiskonfiguration Raspberry Pi

Nach erfolgreicher Verbindung per SSH werden grundlegende Konfigurationen getätigt.
Die Änderung des Kennworts erfolgt mit Hilfe des Befehls ``passwd``.
Dabei muss zunächst das aktuelle Kennwort und anschließend zwei mal das neue Kennwort eingegeben werden.
Anschließend wird unter Angabe des Befehls ``sudo raspi-config`` der textbasierte Editor zur Änderung des Hostnames geöffnet. Unter dem Menüpunkt ``1 System Options / S4 Hostname`` wird der neue Hostname ``audio-retrofit`` vergeben.
Daraufhin ist ein Neustart erforderlich.

## Audiotest

Nach erfolgreicher Basiskonfiguration wird ein erster Audiotest durchgeführt.
Mit Hilfe des Befehls ``alsamixer`` wird der AlsaMixer geöffnet.
Darin wird die zur Zeit aktive Soundkarte angezeigt.
Momentan ist die Standard-Soundkarte ``vc4-hdmi-0`` in Verwendung.
Das Menü zur Auswahl der Soundkarte wird durch das Drücken der Taste ``F6`` ausgewählt.
Darin wird die zusätzliche Soundkarte ``snd_rpi_hifiberry_dacplus`` des DAC-Hats dargestellt.
Die Soundkarte wird somit erfolgreich erkannt.
Daraufhin wird ein Audiotest unter Angabe des nachfolgenden Befehls gestartet. Dabei erscheint die nachfolgende Fehlermeldung.

```txt
pi@audio-retrofit:~ $ speaker-test

speaker-test 1.2.4

Playback device is default
Stream parameters are 48000Hz, S16_LE, 1 channels
Using 16 octaves of pink noise
Playback open error: -19,No such device
```

Zur Analyse des Fehlers ``No such device`` werden zunächst Updates installiert. Nach Recherche wird die Datei ``asound.conf`` unter ``/etc`` erstellt und wie nachfolgend angegeben konfiguriert.

```conf
pcm.!default {
  type hw card 2
}
ctl.!default {
  type hw card 2
}
```

Vgl. [HiFiBerry](https://www.hifiberry.com/docs/software/configuring-linux-3-18-x/)

Die ID der Soundkarte wird mit ``aplay -l`` ermittelt:

```txt
pi@audio-retrofit:~ $ aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: vc4hdmi0 [vc4-hdmi-0], device 0: MAI PCM i2s-hifi-0 [MAI PCM i2s-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: vc4hdmi1 [vc4-hdmi-1], device 0: MAI PCM i2s-hifi-0 [MAI PCM i2s-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: sndrpihifiberry [snd_rpi_hifiberry_dacplus], device 0: HiFiBerry DAC+ Pro HiFi pcm512x-hifi-0 [HiFiBerry DAC+ Pro HiFi pcm512x-hifi-0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

Somit stimmt die ID der Soundkarte in der Konfigurationsdatei ``asound.conf`` mit der vorhandenen ID überein. Die Einstellung ist korrekt.

Der Speaker-Test wird unter Angabe des Befehls ``speaker-test`` erneut durchgeführt und schlägt mit der sleben Fehlermeldung fehl.
Eine Internet-Recherche ergibt, dass der Befehl wie folgt aufgerufen werden soll: ``speaker-test -D default -c 2``.
Daraufhin kann erfolgreich ein Audiosignal über die angeschlossenen Kopfhörer wiedergegeben werden.

Vgl. [HiFiBerry Forum](https://support.hifiberry.com/hc/en-us/community/posts/201495392-It-used-to-work-)

Um zu verifizieren, dass tatsächlich Audio-Dateien abgespielt werden können, wurde eine geeignete M4A-Datei mittels SFTP auf das Gerät übertragen.
Anschließend wurde der VLC-Media-Player unter Angabe des Befehls ``sudo apt install vlc`` installiert. Mit dem Befehl ``cvlc audio.m4a`` wurde die Datei ``audio.m4a`` erfolgreich auf den angeschlossenen Kopfhörern wiedergegeben.

## Installlation von PulseAudio

Das Kernel-Modul ALSA-Sound ist standardmäßig auf dem Raspberry Pi aktiv.
Dieses bietet die Möglichkeit, eine Audioquelle auf einem Wiedergabegerät auszugeben.
Eine gleichzeitige Wiedergabe mehrerer Audioquellen ist nicht möglich.
Möchte man beispielsweise die Wiedergabequelle von Spotifiy-Connect auf Bluetooth-Audio wechseln, ist gegebenenfalls das Wiedergabegerät noch von Spotify-Connect belegt, während Bluetooth-Audio den Zugriff auf das Wiedergabegerät anfordert.
In diesem Szenario kommt es bei der Nutzung von ALSA-Sound zu einem Fehler.
Durch die Verwendung von PulseAudio können mehrere Audioquellen gleichzeitig auf ein Wiedergabegerät zugreifen.
Somit werden Fehler durch den gleichzeitigen Zugriff auf das Wiedergabegerät vermieden und die Verfügbarkeit der Audio-Retrofit-Lösung erhöht.

Die Installation erfolgt nach einem Skript von Nico Kaiser, welches sich vor der Projektumsetzung bewährt hat: [Quelle](https://github.com/nicokaiser/rpi-audio-receiver/blob/main/install.sh)
Zunächst wird PulseAudio über den Paketmanager installiert: ``sudo apt install pulseaudio``.
Anschließend werden die Nutzer ``root`` und ``pi`` in die Gruppe ``pulse-access`` hinzugefügt.
Geschieht das nicht, wird PulseAudio die Wiedergabe von Audioquellen nicht erlauben.
``root`` muss hinzugefügt werden, da später Dienste im Kontext dieses Nutzers laufen werden.$

```bash
# usermod: Rechteverwaltung
# -a : append (zusätzlich zu existierenden Gruppen hinzufügen)
# -G : Group (das Ziel ist eine Gruppe identifiziert durch ihren Namen)
# fuege den Benutzer 'root' der Gruppe 'pulse-access' hinzu
sudo usermod -aG pulse-access root
# fuege den Benutzer 'pi' der Gruppe 'pulse-access' hinzu
sudo usermod -aG pulse-access pi 
```

Um später die Wiedergabe von Bluetooth-Quellen durch PulseAudio zu ermöglichen, benötigt analog dazu der PulseAudio-Nutzer die Zugehörigkeit zur Bluetooth-Gruppe: ``sudo usermod -aG bluetooth pulse``.

Anschließend erfolgt die Konfiguration von PulseAudio für Bluetooth. Dazu wird der initiale Stand der Konfigurationsdatei unter ``/etc/pulse`` durch einen Kopiervorgang gesichert: `` sudo cp client.conf client.conf.orig``.
Daraufhin wird mit einem Editor die ``client.conf`` bearbeitet ``sudo nano client.conf``.
Der Einstellungen ``default-server`` wird das Parameter ``/run/pulse/native`` zugewiesen

 [Quelle](https://gist.github.com/Earnestly/4acc782087c0a9d9db58).
Dadurch wird der PulseAudio-Daemon in einem dedizierten Socket ausgeführt, der systemweit verwendet wird.
Des weiteren wird die Einstellungen ``autospawn = no`` getroffen.
Das Deaktivieren der ``autospawn`` Funktionalität verhindert, dass mehrere PulseAudio-Server auf dem Raspberry Pi gestartet werden [Quelle](https://gavv.github.io/articles/pulseaudio-under-the-hood/).

PulseAudio verwendet Cookies, um Clients gegenüber dem Server zu authentifizieren. Das soll auf einem Mehrbenutzersystem verhindern, dass Anwendungen Audio-Streams an den falschen PulseAudio-Server übermitteln.
Da das Kopieren von jenen Cookie-Dateien in die jeweiligen Anwendungs-Konfigurationen nicht erwünscht ist, wird diese Funktionalität deaktiviert. Somit können Anwendungen Audio-Streams ohne Authentifizierung übermitteln. Dies ist unproblematisch, da durch die bereits durchgeführte Konfiguration ohnehin nur ein PulseAudio-Server auf dem System aktiv ist.
Die Anpassung wird durch das Anfügen von ``auth-cookie-enabled=0 auth-anonymous=1`` an die Zeile ``load-module module-native-protocol-unix`` der Datei ``/etc/pulse/system.pa`` realisiert [Quelle](https://wiki.archlinux.org/title/PulseAudio#Networked_audio).

Nach Abschluss der Konfiguration muss PulseAudio als systemweiter SystemD-Dienst registriert werden.
Dazu wird unter ``/etc/systemd/system/pulseaudio.service`` nachfolgende Konfiguration getätigt:

```conf
[Unit]
Description=Sound Service
[Install]
WantedBy=multi-user.target
[Service]
Type=notify
PrivateTmp=true
ExecStart=/usr/bin/pulseaudio --daemonize=no --system --disallow-exit --disable-shm --exit-idle-time=-1 --log-target=journal --realtime --no-cpu-limit
Restart=on-failure
```
