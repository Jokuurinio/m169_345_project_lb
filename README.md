# Project for m169-345

## Arbeitsplan
Das war mein grober Arbeitsplan.

## Arbeitsabschnitte:
	• Informationen zu den einzelnen Dockercontainer beschaffen.
	• Netzwerkplan zeichnen
	• Docker-Composefile erstellen
	• Alle Container konfigurieren/installieren
	• Testkonzept/Testplan erstellen
	• Tests durchführen und Testprotokolle ausfüllen
	• Dokumentation schreiben

## Wiederhohlende Arbeiten:
	• Arbeitsjournal führen
	• Commits auf Github pushen
	• Docker-Composefile anpassen

Es erschien mir wenig sinnvoll, den einzelnen Arbeitsabschnitten ein Erledigungsdatum zuzuweisen, da ich nicht abschätzen konnte, wie lange die einzelnen Schritte dauern würden. Stattdessen habe ich die Aufgaben Schritt für Schritt abgearbeitet.
Ich habe regelmässig meine Commits auf Github gepusht. Sodass der Lehrer auch meinen Fortschritt überprüfen konnte. Das Docker-Composefile wurde etwa 10mal mit neuen Sachen angepasst. Die Dokumentation hat sich nach und nach mit Inhalt gefüllt. Das Journal wurde nach jedem Arbeitsblock nachgetragen und dann am Schluss in die Dokumentation übertragen.

## Sicherheitskonzept
Eine Vorgabe des Projekts war, dass keine Passwörter im Docker-composefile stehen. Die Passwörter werden in einem eigenen Ordner gespeichert. Da dies ein Schulprojekt ist habe ich sehr einfache Passwörter gebraucht. In der realen Welt müssten diese Passwörter einem Passwortkonzept angepasst werden.
z.B.<br>

	• Passwortlänge = mind. 12
	• Grosskleinschreibung
	• Sonderzeichen
	• Keine ganzen Wörter
	• Passwörter müssen alle 3 Monate geändert werden


## Virtuelle Umgebung mit Docker vorbereiten:

	sudo apt update
	sudo apt install -y docker.io
	sudo systemctl start docker
	sudo systemctl enable docker

	sudo apt install -y docker-compose

## Netzwerk erstellen
Bevor die Docker Compose-Dateien ausgeführt wird: Sicherstellen, dass das externe Netzwerk net_project_lb erstellt wurde:

	docker network create net_project_lb
	
## Containerinformationen

### Jupyter
|Jupyter| |
|:------------- |:--------------- |
|Image |jupyter/scipy-notebook|
|Ports| 8888:8888|
|Volumes| jupyter_data:/home/jovyan/work|
|Environment| JUPYTER_ENABLE_LAB=yes|
|Network| net_project_lb |

### Drupal
|Drupal| |
|:------------- |:--------------- |
|Image |drupal:latest|
|Ports| 8080:80|
|Volumes| drupal_data:/var/www/html|
|Abhängigkeiten| drupal_db|
|Network| net_project_lb |

|drupal_db| |
|:------------- |:--------------- |
|Image |postgres:latest|
|Volumes| drupal_postgres_data:/var/lib/postgresql/data |
|Environment|- POSTGRES_DB: drupal <br> - POSTGRES_USER: drupal_user <br> - POSTGRES_PASSWORD: password|
|Network| net_project_lb |

### Gogs
|Drupal| |
|:------------- |:--------------- |
|Image |gogs/gogs|
|Ports| - 3000:3000 <br> - 2222:22|
|Volumes| gogs_data:/data|
|Abhängigkeiten| gogs_db|
|Network| net_project_lb |

|drupal_db| |
|:------------- |:--------------- |
|Image |postgres:latest|
|Volumes| gogs_postgres_data:/var/lib/postgresql/data |
|Environment|- POSTGRES_DB: gogs <br> - POSTGRES_USER: gogs_user <br> - POSTGRES_PASSWORD: password|
|Network| net_project_lb |

### Portainer

|Portainer | |
|:------------- |:--------------- |
|Image |portainer/portainer-ce |
|Ports| "9000:9000" |
|Volumes| - /var/run/docker.sock:/var/run/docker.sock <br> - portainer_data:/data |
|Network| net_project_lb |


<br>
<br>

## Testing

### Testkonzept

#### Was ist unser Ziel?

Wir wollen die Container auf Persistenz überprüfen. 
Wir wollen überprüfen ob alle Container Korrekt aufgesetzt sind.

#### Wie wird getest ?

Entfernen der Container und erneuter erstellen.

#### Benötigte Infrastruktur:
- Debian (Version 12.5)
- Docker (Version 20.10.24+ dfsg1)

#### Testdaten 
- Logindaten
- Screenshots

### Testplan Persistente Daten

| Persistente Daten |                 |
|:-------------             |:--------------- |
| ID / Bezeichnung          | T-01       |
| Beschreibung              | Es wird überprüft ob die Daten persistent gespeichert werden, auch wenn der Container gelöscht und neu aufgesetzt wird.| 
| Testvoraussetzung         | Der Nextcloudcontainer muss auf localhost:8080 ereichbar sein.<br> Die Installation des Nextcloudcontainer muss abgeschlossen sein.<br> Es muss Testinhalt hinzgefügt werden, sodass mann schnell erkennt ob die Daten persistent gespeichert wurden.        |
| Testschritte              | 1. Docke-compose file erstellt <br> 2. Container erstellen <br> 3. Überprüfen ob alle Container laufen und diese Einrichten <br> 4. Alle Container entfernen. <br> 5.  Alle Container wieder starten mit: docker-compose up -d <br> 7. Überprüfen ob die Daten noch vorhanden sind  | 
| Erwartetes Testergebnis   | Alle Testinhalte sind immer noch vorhanden.|

### Testprotokoll Nextcloud
|Persistente Daten |                 |
|:------------- |:--------------- |
| Tester | Fabian|            |
| Testdatum | 03.07.24 |
| Ergebnis | **Testinhalt** ![](/pictures/drupal%20website%20startpage.png "Image")  ![](/pictures/gogs%20landing%20page.png "Image")<br> <br>  **Testablauf**  ![](/pictures/docker%20rm%20container%20and%20redo.png "Image") |
| Kommentar vom Tester | Der Inhalt war nach dem löschen und neu erstellen des Containers immer noch vorhanden. Alles wie erwartet|

<br>
<br>


## Arbeitsablauf und Zusammenfassung

### Arbeitsblock 1

**Datum: 03.07.24**
<br>
Was wurde gemacht? <br>
- Der Auftrag wurde Überflogen und erste Informationen notiert.
- Ich habe auf dem Heimrechner die VM erstellt und Debian installiert.
- Nach erfolgreicher Installation wurde ebenfalls Docker installiert.
- Anschliessend habe ich mich darüber informiert was Jupyter und Drupal macht bzw. ist. Ich habe das Docker-Compose files mit informationen aus dem Docker-Hub, Youtube, Online-Foren und mithilfe von ChatGPT erstellt und organisiert.
- Die erste Installation lief aufgrund von Schreibfehlern falsch, nach anschliessender Korrektur wurden die Container erstellt und zum ersten Mal gestartet.
- Bei den ersten versuchen auf Jupyter via localhost:8888 zu zugreifen, wurde immer ein Token gewünscht. Da ich keine Ahnung davon hatte oder warum das so war ging es zurück an Youtube und ChatGPT. Dies half mir nur bedint weil er plötzlich Jupyter Notebook wollte und via Token... Bis heute keine Ahnung warum... habs dann vorerst bei Seite gelegt. ![](/pictures/jupyter%20landing%20page.png "Image")
- Derweilig habe ich Drupal und Gogs eingerichtet
- Zugriff auf Jupyter hat via Portainer funktiniert. Ich habe den gewünschten Token für Jupyter gefunden und anschliessend konnte ich korrekt darauf Zugreifen. ![](/pictures/jupyter%20logs%20token.png "Image")
- Persistente Datenspeicherung Überprüft. Funktioniert. Nach dem Entfernen und wieder erzeugen, waren die Daten noch immer vorhanden.

### Arbeitsblock 2

**Datum: 10.07.24**
<br>
Was wurde gemacht? <br>
- Ich habe gemerkt das die Abgabe bereits um 13:00 ist...  //Great Job Fabian Lese sött mer chöne
- Anpassung des README.md und Dokumentation fertigstellen



