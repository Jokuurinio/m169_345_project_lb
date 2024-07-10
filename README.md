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



![](/pictures/jupyter%20landing%20page.png "Image")
