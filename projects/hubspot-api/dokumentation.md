<!-- TITLE: Dokumentation -->
<!-- SUBTITLE: A quick summary of Dokumentation -->

Integration Software fuer McArena zum Import in Hubsport

Projekt


Anforderungen :

Der Importer liest CSV Dateien aus einem bestimmten Ordner, konvertiert die Daten und sendet diese per API Call in die Kontakte des vorgesehen Hubspot Account.

Technische Anforderungen :

Zur problemlosen Installation benoetigt die Anwendung einen Server mit :

- Installiertem python3 ( mit zusaetzlichem request modul)
- Server muss die Moeglichkeit bereit stellen, auf ein Verzeichnis per sftp zureifen zu koennen
- Server muss die Moeglichkeit besitzten, Email per Sendmail zu verschicken
- Es muss die Moeglichkeit bestehen, einen crontab einzurichten


Systemdokumentation

Technische Daten :

- python3
- sendmail
- crontab

Funktionsweise in einzelnen Schritten :

- Der Importer wird per git installiert und enthaelt die Funktionsweise zum Einlesen von CSV dateien und saemtliche Funktionen zur Deprovisionirung von Log Dateien.

Die angeforderten cron jobs sind in diesem Format :


```batchfile
# Crontab fur hbspot api all 15 Minutes
*/15 * * * * /var/www/vhosts/mcarena/tool_hubspot_migration/call_hubspot_api_cron.sh
# Crontab delte logs after half hear
0 0 1 */6 * find /var/www/vhosts/mcarena/tool_hubspot_migration/log/* mtime +182 -type f -delete >/dev/null 2>&1
# Crontab delte logs after half year
0 0 1 */6 * find /var/www/vhosts/mcarena/tool_hubspot_migration//log/* mmin +2 -type f -delete >/dev/null 2>&1
# Crontab remove logs files weekly , every Tueday on 6:25 with date to same file
25 6 * * Tue  /var/www/vhosts/mcarena/tool_hubspot_migration//scripts/movelog.sh >/dev/null 2>&1
# Crontab remove logs files every 2 minutes with date to same folder
#*/1 * * * *   /var/www/vhosts/mcarena/tool_hubspot_migration/scripts/movelog.sh >/dev/null 2>&1

```

Einlesen CSV Dateien :

- Der Importer laest alle Dateien mit der Endung *.csv*  in einem bestimmten Verzeichnis. In dieses Verzeichnis mit den Namen *csvfiles* besteht die Moeglichkeit, per ftps Dateien hochzuladen.
Struktur des Verzeichnisses :

		- csvfiles
				- processsed
				- errorprocessed

Gibt es ein Problem in einer CSV Datei, wo wird ein fehler ausgegeben und die Datei wird mit einem Zeitstempel nach errorprocessed verschoben. Beispiel *csvfiles/errorprocessed/export-schorndorf_2019-12-06.06.12.06.12.20190-20:59:33.csv*
So sieht  man am endenden Zeitstempel der Datei, wann die Datei importiert wurde.
Sollte die CSV Datei fehlerfrei sein, so wird sie komplett importiert

Mails

Sobald einen Datei importiert wurde, wird an die Empfaenger eine Mail gesendet ( Bitte auch im spam Ordner achten. Der Absender ist mcarena@web-02.etes.de)

Error Email :

```Processed:
lw1@mcarena.de

File NOT imported correctly to Hubspot and moved to erroprocessed: export-schorndorf_2019-12-06.06.12.richtigeKategorie.06.12.201908-20:32:49.csv 

Error: Error at Importing : list index out of range : Line 3

``
`
Prozessierte Email:

```Processed:
lw1@mcarena.de

File imported correctly to Hubspot and moved to processed: test_hubspot.single.06.12.201901-13:30:46.csv 
```









