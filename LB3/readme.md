# **LB2** **Docker**  <!-- omit in toc -->

## Inhalt <!-- omit in toc -->
- [Einleitung](#einleitung)
- [Service](#service)
- [Technische Angaben](#technische-angaben)
  - [Netzwerkplan](#netzwerkplan)
  - [Code](#code)
  - [Anleitung für den Betrieb](#anleitung-f%C3%BCr-den-betrieb)
- [Testing](#testing)


# Einleitung

In der Lernberuteilung geht es um das Ausetzten und betreiben von einem Service mit Docker. Docker ist eine Open-Source Containervirtualisierungsplatfform. Dank dem Docker Hub können viele Images von Anwendungen oder Betriebssystemen heruntergeladen werden.


# Service

Als Service wurde Wordpress installiert. Bei WordPress wird im Hintergrund MySWL verwendet. Zusätzlich ist es möglich per PHPMyAdmin die Datenbanken zu verwalten.

Per Interner Verlinkung zwischen MySQL und PHPMyAdmin und MySQL und Wordpress kann dies ermöglicht werden.


# Technische Angaben

Der Service wird mit 3 Docker Container realisiert. Bei ersten wird MySQL, beim zweiten PHPMyAdmin und beim dritte Wordpress installiert. Durch das virtualnet "Net1" können die Container kommunizieren.

| **Info**       | **Container** 1 |   **Container** 2 |  **Container** 3 |
| :------------- | :-------------: | ----------------: | ---------------: |
| Container Name |      MySQL      |        PHPMyAdmin |        Wordpress |
| Docker Image   |    mysql:5.7    | phpmyadmin:latest | wordpress:latest |
| Netzwerk       |      Net1       |              Net1 |             Net1 |
| IP             |      DHCP       |              DHCP |             DHCP |

## Netzwerkplan


Die Container werden innerhalb von der Docker VM aufgesetzt. Das Net1 wird auf den Modus "Bridge" konfiguriert, sodass die Container vom Host erreichbar sind. Dabei ist der Host auch der Gateway zum Internet.

Die drei Container werden am Net1 angehängt und bekommen per DHCP eine IP im Range 127.0.0.x/24. Der Gateway erhält immer die IP 172.0.0.1.

Mit einem Link kann der PHPMyAdmin und Wordpress auf den MySQL Container zugreifen. Wie dies Funktioniert, wird im Abschnitt **Code** eingegangen.

Damit der Host auf das Webinterface des PHPMyAdmin zugreifen kann, muss der Container Port 80 auf den Host Port 8080 gemapt werden. Bei Wordpress wird das gleiche auf den Host Port 8081 gemacht.

## Code
Das Projekt wurde mit einem Docker Compose File realisiert. In diesem File werden alle Container und Netzwerk Parameter definiert. Mit diesem Befehl wird dann die Struktur aufgesetzt:
```Shell
docker-compose -f ʺPfad\zum\File\docker-compose.ymlʺ up -d --build
 ```
"-d" definiert, dass die Container im Hintergrund aufgesetzt wird.

"-f" setzt den den Pfad zum docker-compose.yml File


Auf Zeile 4-16 wird der MySQL Container erstellt und konfiguriert

Auf Zeile 18-29 wird der PHPMyAdmin Container erstellt. Dabei wird auf Zeile 29 die Verlinkung zwischen PHPMyAdmin und MySQL realisiert(Datenbank = MySQL Container).

Auf Zeile 32-46 wird der Wordpress COntainer erstellt. Auf Zeile 42 wird die Verlinkung zu MySQL gesetzt.

Auf Zeile 47-48 wird das Volume gesetzt.

Auf der Zeile 49-50 wird das Netzwerk erstellt


## Anleitung für den Betrieb

### 1. Installation <!-- omit in toc -->
Wie oben beim Code erklärt wird per Befehel das Docker-Compose.yml ausgeführt und somit die Container aufgesetzt:
```Shell
docker-compose -f ʺPfad\zum\File\docker-compose.ymlʺ up -d --build
 ```

 ### 2. Zugriff auf MySQL Webinterface <!-- omit in toc -->

- Um auf PHPMyAdmin zuzugreifen, muss ein Browser geöffnet werden.

- Es wird die URL http://localhost:8080 eigegeben


### 3. PHPMyAdmin Login <!-- omit in toc -->
Als Benutzer wird **User** genommen

Das Passwort ist **1234**

Die Anmeldung erflogt beim drücken der Enter-taste



### 4. Los arbeiten mit PHPMyAmdin <!-- omit in toc -->

AB jetzt kann mit PHPMyAdmin gearbeitet werden. Es können Datenbanken erstellt und administriert werden.

Wenn benötigt können neue Benutzer im Phpmyadmin angelegt werden.


### 5. Zugriff auf Wordpress <!-- omit in toc -->

- Um auf Wordpress zuzugreifen, muss ein Browser geöffnet werden.

- Es wird die URL http://localhost:8081 eigegeben


Jetzt kann die Sprache ausgewählt werden. Anschliessend wird die erste Seite erstellt.

# Testing

Das Testing wir mit einem Testing Protokoll durchgeführt. Dabei wird er SOLL / IST Zustand Verglichen und erläutert wie getestet wurde.

| SOLL-Zustand                                                             |                                      IST-Zustand                                      |                                                                                                            Test |
| :----------------------------------------------------------------------- | :-----------------------------------------------------------------------------------: | --------------------------------------------------------------------------------------------------------------: |
| 3 Container wurden per Befehl installiert                                |                 Die 3 Container wurden erstellt und werden ausgeführt                 | In Powershell wurde der Befehl docker-compose -f "C:\myrep\my_M300\Docker\LB2\docker-compose.yml" up -d --build |
| Das Netzwerk "Net1" wurde erstellt                                       |             Das Netzwerk wurde während dem Ausführen des Befehls erstellt             |                                        Mit dem Befehl: Docker Network ls werden alle Docker Netzwerke angezeigt |
| Die Portverlinkung von PHPMyAdmin von Port 80 auf 8080 ist gewährleistet | Mit http://localhost:8080 kann auf das Webinterface von PHPMyAdmin zugegriffen werden |                                                             Im Browser die Adresse http://localhost:8080 öffnen |
| Mit dem Gesetzten User Login kann man sich anmelden                      |           Mit dem Benutzername User und Passwort 1234 kann eingelogt werden           |                                            In der Anmeldemaske von PHPMyAdmin werden die Login Daten eingegeben |
| Die Portverlinkung von Wordpress von Port 80 auf 8081 ist gewährleistet | Mit http://localhost:8081 kann auf Wordpress zugegriffen werden |                                                             Im Browser die Adresse http://localhost:8081 öffnen |

