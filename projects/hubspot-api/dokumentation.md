<!-- TITLE: Dokumentation McArena Hubspot Importer</center> -->
<!-- SUBTITLE: <center>Systemdokumentation zum CSV Importer nach Hubspot fuer McArena</center> -->

# <center>Integration Software fuer McArena zum Import in Hubsport</center>



**<center>Author: Ottavio Braun</center>** ©
**<center>© Ottavio Braun</center>**
**<center>otti@petitcode.com</center>**
**<center>08.12.2019</center>**

## Projekt

Der Importer liest CSV Dateien aus einem bestimmten Ordner, konvertiert die Daten und sendet diese per API Call in die Kontakte des vorgesehen Hubspot Account.

### <center>Technische Anforderungen :</center>

Zur problemlosen Installation benoetigt die Anwendung einen Server mit :

- Installiertem python3 ( mit zusaetzlichem request modul)
- Server muss die Moeglichkeit bereit stellen, auf ein Verzeichnis per sftp zureifen zu koennen
- Server muss die Moeglichkeit besitzten, Email per Sendmail zu verschicken
- Es muss die Moeglichkeit bestehen, einen crontab einzurichten


### <center>Systemdokumentation</center>


**Technische Daten :**

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
Sollte die CSV Datei fehlerfrei sein, so wird sie komplett importiert.

**Hubspot :**
Anschliessend werden die Daten zu json formatiert und per request zu hibspot gesendet. Gibt Hubspot Fehler zurueck, so werden diese in einer Mail versendet.

**Mails**

Sobald einen Datei importiert wurde, wird an die Empfaenger eine Mail gesendet ( Bitte auch im spam Ordner achten. Der Absender ist mcarena@web-02.etes.de)

- Error Email :

```Processed:
lw1@mcarena.de

File NOT imported correctly to Hubspot and moved to erroprocessed: export-schorndorf_2019-12-06.06.12.richtigeKategorie.06.12.201908-20:32:49.csv 

Error: Error at Importing : list index out of range : Line 3

```

- Prozessierte Email:

```Processed:
lw1@mcarena.de

File imported correctly to Hubspot and moved to processed: test_hubspot.single.06.12.201901-13:30:46.csv 
```


Processed stellt eine Liste der Eintraege dar, die bereits importiert wurden. 
Ansonsten wird die Zeile ausgegeben, in der der Fehler in der CSV Datei liegt.


### Vorgehensweise.

- Wird eine Mail gesendet, bei der ein Fehler in der CSV Datei ausgegen wird ( dies kann auch ein Fehler im Hubspot sein : keine Property, falscher Property Typ, etc) so korrigiert der Benuter dies in der Mail angegeben CSV Datei, die mit dem jeweilogen Zeitstempel in *errorprocessed* liegt und schiebt diese Datei wieder in den Ordner *csvfiles*). Diese wird dann vom Importer wieder abgeholt und prozessiert. Dieser Prozess geschieht so lang, bis die CSV Datei nur fehlerfrei Daten enhaelt ( sollte durch einen automatischen Export sowieso gewaehrleistet sein.

**Wichtig :**

- Neue Spaltenn und Aenderungen im Dateiformat bedarf Anpassungen im Importer
- Der Importer datet die Daten per email ab. Steht in der email somit schon ein in Hubspot eingetragener Satz, so wird kein neuer Kontakt angelegt, sondern die Daten angepasst


Properties in Hubspot, die momentan eingelesen werden :

                        "property": "email",
                        "property": "lastname",
                        "property": "website",
                        "property": "company",
                        "property": "phone",
                        "property": "mobilephone",
                        "property": "address",
                        "property": "date_of_birth",
                        "property": "city",
                        "property": "fax",
                        "property": "datum_der_letzten_Buchung",
                        "property": "wert_der_letzten_Buchung",
                        "property": "zip",
                        "property": "datum_der_n_chsten_buchung",
                        "property": "kontaktkategorie"
												
**Logging:**

Zum Logging wird logger.pl verwendet. Die komplette Funktionalitaet uebernimmt dieser.
Die Funktion zur Rotierung der log Dateien uebernehmen die oben genannten Cron Jobs.


Installation  auf Server:

Path : */var/www/vhosts/mcarena/tool_hubspot_migration*
Script zum ausfuehren : */var/www/vhosts/mcarena/tool_hubspot_migration/call_hubspot_api_cron.sh*
Log Files : */var/www/vhosts/mcarena/tool_hubspot_migration/log
				
				