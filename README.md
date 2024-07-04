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

## Generierung des Jupyter Password/token für den ersten Log-in

	Sudo apt install jupyter



![](/pictures/jupyter%20landing%20page.png "Image")