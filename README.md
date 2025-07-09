# Blackhat - HackMyVM - Easy

![Blackhat HackMyVM Icon](Blackhat.png)

## Maschineninformation

*   **Link zur VM:** [https://hackmyvm.eu/machines/machine.php?vm=Blackhat](https://hackmyvm.eu/machines/machine.php?vm=Blackhat)
*   **Schwierigkeitsgrad:** Easy

## Autor

*   **Pentest Report Author:** DarkSpirit

## Bericht Online

*   **Link zum detaillierten HTML Bericht:** [https://alientec1908.github.io/Blackhat_HackMyVM_Easy/](https://alientec1908.github.io/Blackhat_HackMyVM_Easy/)

## Zusammenfassung

Dieser Bericht dokumentiert den Penetrationstest der HackMyVM-Maschine "Blackhat", die als "Easy" eingestuft ist. Der Test umfasste die initiale Aufklärung (Reconnaissance), die Analyse der Webanwendung, das Erringen des ersten Systemzugriffs (Initial Access) durch die Ausnutzung einer Remote Code Execution (RCE) Schwachstelle, die Ausweitung der Berechtigungen (Privilege Escalation) auf den Benutzer `darkdante` und schließlich auf den `root`-Benutzer, um die User- und Root-Flags zu erlangen.

## Gefundene Schwachstellen & Vorgehen

Der Weg zur vollständigen Kompromittierung der Maschine umfasste folgende Schritte und Schwachstellen:

1.  **Reconnaissance & Web Enumeration:** Identifizierung des Ziels, offener Port 80 (Apache). Fund der `phpinfo.php` Seite, die Informationen über die PHP-Konfiguration preisgibt. Entdeckung des ungewöhnlichen Apache-Moduls `mod_backdoor` und eines Hinweises im HTML-Source Code auf eine Backdoor.
2.  **Remote Code Execution (RCE):** Identifizierung und Ausnutzung einer Backdoor, die über einen spezifischen HTTP-Header namens "Backdoor" Befehle auf dem System als Benutzer `www-data` ausführt.
3.  **Initial Access:** Nutzung der RCE-Schwachstelle, um eine Reverse Shell als Benutzer `www-data` zur Angreifer-Maschine zu initiieren und zu erhalten.
4.  **Privilege Escalation (Benutzer darkdante):** System-Enumeration als `www-data` identifizierte den Benutzer `darkdante` und die User-Flag (`user.txt`), die jedoch nicht lesbar war. Durch manuelles Testen des SUID-Binaries `su` wurde eine Fehlkonfiguration entdeckt, die es ermöglichte, zum Benutzer `darkdante` zu wechseln, ohne dessen Passwort eingeben zu müssen.
5.  **Privilege Escalation (Root):** Aus der `darkdante` Shell heraus wurde festgestellt, dass die Datei `/etc/sudoers` aufgrund fehlerhafter Dateiberechtigungen für den Benutzer `darkdante` schreibbar war. Eine NOPASSWD-Regel für `darkdante` wurde in die `sudoers`-Datei injiziert, was uneingeschränkte `sudo`-Rechte ohne Passwort ermöglichte.
6.  **Root Access:** Nutzung der manipulierten `sudo`-Berechtigungen (`sudo su`) zur Erlangung einer Root-Shell.
7.  **Flags:** Erlangung der User-Flag in `/home/darkdante/user.txt` und der Root-Flag in `/root/root.txt`.

## Verwendete Tools

*   arp-scan
*   vi
*   nmap
*   nikto
*   feroxbuster
*   curl
*   wfuzz
*   nc
*   python3 http.server
*   wget
*   linpeas.sh
*   pspy64
*   Metasploit
*   suForce
*   nano

## Berichtsdatum

09 Jun 2025
