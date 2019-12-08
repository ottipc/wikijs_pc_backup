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







