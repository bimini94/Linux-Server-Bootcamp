Im Folgenden ist ein kleiner Kurs für Juniter Admins um sich Kenntnisse über die in Juniter verwendeten Technologien zu erlangen. Das ganze ist nicht als "Vorlesung" sondern eher als Hilfe zur selbst Hilfe zu aka "betreutes Googlen" zu verstehen. Solltet ihr Fragen haben könnt ihr euch jederzeit bei mir melden. Der Kurs wird noch um weiter Aufgaben erweitert. So das am Ende jeder die Komplette einrichtung eine virtuellen Maschine einmal durchgespielt hat. Im idealfall ist das Endergebniss das die virtuelle Maschine in genau dem Status ist in dem auch unser gemieteter V-Server sich befindet. 
Ihr braucht für den Kurs einen SSH-Client. Auf macOS und Linux ist das bereits vorinstalliert, auf Windows kann entweder Putty, GitBash oder die WSL Bash verwendet werden.
Desweiteren benötigt ihr einen Account auf unserem Login-Server Domino um einen Zugang zu unserem lokalen Netzwerk auch außerhalb des Towers zu bekommen. 
Um eine VM zu bekommen meldet euch bitte bei mir dann weise ich euch eine zu. 
# Aufgabe 0: How To Shell
Administration von Linux Servern findet fast ausschließlich über die Konsole statt. Falls ihr folgende Befehle nicht kennt macht euch mit der Funktionsweise davon vertraut:
* man
* cd
* ls
* pwd
* mkdir
* mv
* cp
* rm
* less
* nano
* sudo
* apt
* ssh
* scp
* grep
* cat
* top
* | (pipe)
Außerdem solltet ihr euch noch mit der Linux Verzeichnisstruktur vertraut machen. Dafür bietet sich folgender Artikel an : https://wiki.ubuntuusers.de/Verzeichnisstruktur/
# Aufgabe 1: Accounts
Als nächstes geht es darum das ihr auf einer der Test VMs einen Account erstellt.
Das Root Passwort ist ```Passwort 1```. Die VMs heiße ```Testvm{1..10}``` und haben die IP-Adresse ```192.168.228.1{21..30}```. Ihr könnt euch mit der VM nur wenn ihr im Tower seid und mit dem Juniter WLAN verbunden seid direkt per SSH verbinden. Seid ihr in einem anderen WLAN müsst ihr euch zuerst mit SSH auf login-node.cct-ev.de verbinden und dann von dort per SSH weiter auf eure VM.
## Aufgabe 1.1: Account Einrichtung
Es ist eine übliche Praxis statt alle Befehle mit Root-Rechten auszuführen den normale Nutzeraccount zu verwenden und wann immer nötig „sudo „verwendet. Ein direkter Login über SSH sollte standartmäßig deaktiviert sein. Da SSH Login via Passwort generell angreifbar ist sollte stattdessen ein SSH-Key zur Authentifizierung verwendet werden. Da im Zweifel aber immer ein Notfall-Account verfügbar sein soll über den noch ein Login via Passwort möglich ist sollte dieser Ebenfalls eingerichtet werden. In Juniter hat sich als Accountname „Toor“ durchgesetzte. Folgende Schritte sollten in Aufgabe 1.1 erledigt werden:
1. Richtet einen Account für euch ein
2. Lest nach wie eine Authentifizierung mittels Key funktioniert und was der unterschied zwischen einem private und public Key ist.
3. Stellt den Account auf Login SSH-Key um (*)
4. Gebt euch selbst sudo Rechte
5. Richtet einen Notfallacount mit dem Benutzernamen Toor ein 
```PW: Passwort 2```
6. Schaltet den Login via SSH für den Root Account aus
7. Schaltet den Login mit Passwort für alle Account außer Toor ab
## Aufgabe 1.2: Brute Force Schutz
SSH Zugänge die offen im Internet sind werden regelmäßig von Bots mit Brute Force oder Wörterbuchangriffen bombardiert. Ein sinnvoller Schutzmaßname ist Fail2Ban.
1. Setzte dich mit der Funktionsweise von Fail2Ban auseinander
2. Installiere Fail2Ban
3. Erhöhe die Anzahl der erlaubten Fehlversuche auf 3 und die Sperrzeit auf 15 Minuten
## Aufgabe 1.3: Firewall einrichten
Der nächste Schritt ist es eine Firewall einzurichten. Diese soll nur die Ports nach außen freigeben die benötigt werden. Also zum Beispiel port 80 und 443 für eine Webanwendung oder Port 22 für SSH. Eine einfach zu konfigurierende Firewall ist iptables. Da Fail2Ban mit iptables funktioniert ist das Programm schon installiert.
1. Lasse dir die bestehenden Firewall Regeln anzeigen und lies nach wie das Funktionsprinzip von iptables ist. Versuche damit die funktionsweise von Fail2Ban zu verstehen.
2. Blockiere allen einkommenden Traffic außer Port 22 (sonst kommt ihr nichtmehr per SSH auf eure VM) 
3. Gebt als Vorbereitung auf Aufgabe 2 Port 80 frei.
4. Sorgt dafür das die Firewall Regeln persisent sind und auch einen Neustart überleben
# Aufgabe 2: Webserver einrichten
## Aufgabe 2.0: SSH Proxy einrichten
Wenn ihr nicht in der Uni seid könnt ihr auf die Websiten die ihr in eurer VM laufen lasst nicht zugreifen, da die VMs keine öffentliche IP haben. Um die Funktion des Webservers dennoch testen zu können richtet euch einen SSH Proxy ein.
## Aufgabe 2.1 Apache installieren und eigene (statische) Testwebsite anlegen
## Aufgabe 2.2 Subdomain als VirtualHost anlegen
## Aufgabe 2.3 HTTPS mit let's Encrypt einrichten
# Aufgabe 3: Datenbankserver einrichten
# Aufgabe 4: FTP Server einrichten
# Aufgabe 5: Docker


*(1): (wenn ihr euren SSH Key einrichtet und per SSH über Domino hoppen wollt ist das Stichwort SSH Agent Forwarding, bitte auf keinen Fall einen privaten Schlüssel auf Domino ablegen)
