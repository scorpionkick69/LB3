![](https://owncloud.org/wp-content/uploads/2018/09/ownCloud-docker-1.png)
# LB3 Dokumentation
## Container

| Autor | Amirthalingam |
| ------ | ------ |
| Klasse | ST17c|
| Projekt | Apache Webserver |
| Lehrperson | Marco Berger|
| Version | 1.0 |

## Inhaltsverzeichnis

- Einleitung
  - Übersicht des Projektes
  - Vorbereitung
  - Reflexion
  - Quellenverzeichnis


***
## Einleitung

Bei dieser Projektarbeit muss eine Arbeit erstellen, welche auf der Docker Container-Technologie basiert.
Meine Arbeit ist ein Apache-Server, welcher meine eigene Webseite darstellt.

***
# Übersicht des Projektes
    +---------------------------------------------------------------+
    ! Notebook                                                      !                 
    ! Apache-Webserver Port: 8080 (127.0.0.1)                       !	
    !                                                               !	
    !    +-----------------------------------------+                !
    !    ! Virtuelle Maschine                      !                !
    !    ! Web Server (Port:80)                    !                !
    !    +-----------------------------------------+                !
    !                                                               !	
    +---------------------------------------------------------------+

    ***
## Vorbereitung

- Ich habe mein Arbeit auf einem Ubuntu-VM Version 18.04 entwickelt. Am besten benutzen sie auch diese Version, um meiner Anleitung zu folgen. Stellen Sie sicher, dass Docker installiert ist.

## Vorgehensweise
- Erster Schritt: Mein Repository auf die lokale Festplatte herunterladen und entpacken
```
https://github.com/scorpionkick69/LB3.git
```
- Zweiter Schritt: Starten sie im Apache-Ordner das Terminal und führen sie diesen Befehl aus, um den Docker Container zu builden:
```
docker build -t apache .
```
- Dritter Schritt: Docker Container starten:

```
docker run --rm -d -p 8080:80 -v `pwd`/web:/var/www/html --name apache apache
```

- Vierter Schritt: Im Browser "localhost:8080" eingeben
![Bild1](1.PNG)

***
## Erklärung Code
**Zeile 4:** Das Betriebssystem und die Version werden hier definiert.
**Zeile 5:** Mit der Zeile MAINTAINER kann man das Feld Autor festlegen.
```
4- FROM ubuntu:18.04
5- MAINTAINER Marcel mc-b Bernet <marcel.bernet@ch-open.ch>
```

**Zeile 7:** Dieser Befehl lädt die aktuellsten Pakete herunter, um die neusten Versionen von Paketen zu haben.
**Zeile 8:** Jetzt wird Apache heruntergeladen
```
7- RUN apt-get update
8- RUN apt-get -q -y install apache2
```

**Zeile11:** Der Benutzer www-data wird erstellt.
**Zeile12:** Die Gruppe www-date wird erstellt.
**Zeile13:** Hier wird definiert, dass Apache in diesem Ordner alle Sachen für die Darstellung der Seite findet.
```
11- ENV APACHE_RUN_USER www-data
12- ENV APACHE_RUN_GROUP www-data
13- ENV APACHE_LOG_DIR /web
```

**Zeile 15:** Die Ordner "/var/lock/apache2 /var/run/apache2" sollen erstellt werden
```
RUN mkdir -p /var/lock/apache2 /var/run/apache2
```

**Zeile 17:** Der Port 80 soll geöffnet werden. Dieser wird für den Zugriff auf die Webseite benötigt.
```
EXPOSE 80
```

**Zeile19:** Hier wird ein Volume definiert, welches der Container braucht, um zu laufen.
```
VOLUME /var/www/html
```

**Zeile21:** Mit CMD gibt man an das man etwas in der Shell ausführen möchte.Im Ordner "/usr/sbin/apache2" wird nach Befehlen gesucht, die ausgeführt werden können. Ausserdem wird dieser Befehl im Vordergrund ausgeführt.
```
CMD /bin/bash -c "source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOREGROUND"
```
***
## Reflexion
Dieses plattformübergreifende Dienstmodul war ein spezielles Modul. Vorher kam ich nie mit Container in Kontakt. Ich habe lediglich von Docker und Kubernetes gehört. Dieses Modul am Anfang zu verstehen war recht schwierig, aber nach und nach konnte ich das Modul besser 
verstehen. Leider hindert uns Corona daran, dass wir alle zusammen in einem Klassenraum zusammenlernen können. Für mich war es sehr speziell zuhause Unterricht zu haben. Diese offene Aufgabenstellung hatte für mich mehr Schattenseiten als Sonnenseite. Ich finde es gut, 
dass man sehr viele Projekte selber machen könnte, aber ich hätte viele Projekte gehabt, die ich mache möchte, aber die Entscheidung für ein Projekt war für mich schwierig. Ich habe schlussendlich Apache genommen und und es mit einer Webseite erweitert. Ich bedanke mich 
recht herzlich, dass sie uns dieses interessante Thema etwas näher gebracht haben.
***
## Testcase
Nachdem man den Teil "Vorgehensweise" durchgespielt hat, sollte die Webseite nach dem Neustart des PC trotzdem laufen, wenn man wieder "localhost:8080" im Browser eingibt.

## Quellenverzeichnis

https://github.com/mc-b/M300/tree/master/docker/apache


