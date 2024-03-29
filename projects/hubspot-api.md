<!-- TITLE: McArena//Hubspot Api -->
<!-- SUBTITLE: A quick summary of Hubspot Api -->

# Header
## Kunde

**McArena** 

Matthias Prinz : mp@mcarena.de

Lukas Weissler : lw@mcarena.de

Lukas Weißer
Sales & Marketing Manager

McArena GmbH | Karl-Ferdinand-Braun-Straße 3 | 71522 Backnang | Deutschland
Telefon: +49 (0) 7191 – 3789 90-1 | Mobil: +49 (0) 151 – 101 69 381
Internet: www.mcarena.de <http://www.mcarena.de/>  | E-Mail: lw@mcarena.de <mailto:lw@mcarena.de>
Amtsgericht Stuttgart | HRB 746642 | UID DE291895155


**Forum media**

Salvatore Timparano : st@forumedia.com

Salvatore Timpanaro
 
Forumedia GmbH
Bärenstr. 8
78054 Villingen-Schwenningen

 
Tel. 07720-9949190
Fax 07720-33069
st@forumedia.com

## Anforderungen des Kunden :

*Folgende Daten würden wir sehr gerne aus dem bestehenden Buchungssystem in HubSpot importieren:*
 
*Name
Vorname
Adresse
E-Mail
Telefon
Etc. (Je mehr, desto besser)
Diese Felder gibt der Kunde bei der Registrierung in einem Formular an, sollten also relativ leicht zu exportieren sein.*
 
*Darüber hinaus muss eine Zuordnung der Person zu der entsprechenden Anlage stattfinden. Dies haben wir aktuell mit einem Eigenschaftsfeld „Kontaktkategorie“ in HubSpot gelöst, sodass der Kunde dann die Kontaktkategorie „McArena Schorndorf“ hat. Bei einem manuellen Import ist diese Zuordnung problemlos möglich.*
 
*Optimal wären auch folgende Informationen:
das Datum der getätigten Buchungen / mindestens der letzten Buchung
die Anzahl der getätigten Buchungen (in einem gewissen Zeitraum)
Volumen der Buchungen(Zeit oder €)*


Laut Herr Timparano :

*es gibt in unserem System einen manuellen CSV Export der Kunden Stammdaten (Adresse, usw.) und des Rechnungs-Ausgangsjournals.
Weitergehende Exporte gibt es bislang nicht.*

und 

*Weitere Exporte lassen sich nach euren Wünschen programmieren.
Wie Herr Weisser schon richtig angesprochen hat handelt es sich hierbei jedoch um einen manuell angestossenen Export und die CSV Datei liegt dann
lokal auf dem PC.* 

*So wie ich es verstehe wird hier aber ein automatisierter Export in eure Hubspot Software gewünscht.
Hierzu müsste also die CSV Datei automatisch X mal am Tag erstellt werden und dann auf einem FTP Server abgelegt werden wo sie dann
von der Hubspot Software wiederum automatisch "abgeholt" wird und eingelesen wird. Das ganze ist natürlich schon ein grösserer Aufwand.
Und wir brauchen den FTP Server dazu.*



## Dokumentation

https://developers.hubspot.com/docs


## Calls

Email wird als Primary Key im Call uebergeben

**Create or Update Contact :** https://developers.hubspot.com/docs/methods/contacts/create_or_update

Email wird im update Call gespeichert:

**Update Contact :** https://developers.hubspot.com/docs/methods/contacts/update_contact

HIer werden die Deals gespeichert :

**Create Deal :** https://developers.hubspot.com/docs/methods/deals/create_deal


## Json

Create Contact :

https://api.hubapi.com/contacts/v1/contact/?hapikey=demo


```json
{
  "properties": [
    {
      "property": "email",
      "value": "testingapis@hubspot.com"
    },
    {
      "property": "firstname",
      "value": "Adrian"
    },
    {
      "property": "lastname",
      "value": "Mott"
    },
    {
      "property": "website",
      "value": "http://hubspot.com"
    },
    {
      "property": "company",
      "value": "HubSpot"
    },
    {
      "property": "phone",
      "value": "555-122-2323"
    },
    {
      "property": "address",
      "value": "25 First Street"
    },
    {
      "property": "city",
      "value": "Cambridge"
    },
    {
      "property": "state",
      "value": "MA"
    },
    {
      "property": "zip",
      "value": "02139"
    }
  ]
}

```






Create Deal :


https://api.hubapi.com/deals/v1/deal?hapikey=demo



```json
{
  "associations": {
    "associatedCompanyIds": [
      8954037
    ],
    "associatedVids": [
      27136
    ]
  },
  "properties": [
    {
      "value": "Tim's Newer Deal",
      "name": "dealname"
    },
    {
      "value": "appointmentscheduled",
      "name": "dealstage"
    },
    {
      "value": "default",
      "name": "pipeline"
    },
    {
      "value": "24",
      "name": "hubspot_owner_id"
    },
    {
      "value": 1409443200000,
      "name": "closedate"
    },
    {
      "value": "60000",
      "name": "amount"
    },
    {
      "value": "newbusiness",
      "name": "dealtype"
    }
  ]
}
```



## API Key

Original : eb17aff9-c3bc-42ff-b107-53f6d230b595
Test : 730c761f-9db5-41c3-a391-b981552855bf

## TODO 

- Kunde muss sich einen API Key anlegen
- Entscheidend in welcher Sprache? Wo wird deployed?
- In wie weit incrementell? Wie sieht die CSV Datei aus?
- Herr Timparano muss somit nur den automatischen Export in ein Verzeichnis programmieren. Evtl auch cron?


## Python

CSV einlesen : https://realpython.com/python-csv/

Api Call senden : https://www.geeksforgeeks.org/get-post-requests-using-python/


## Implementierung

- Evtl Python Script ueber normalen cron getriggert
- Script geht ueber Verzeichnis und schaut welche Datei noch nicht in processed oder errorprocessed ist
- neue CSV Dateien einlesen
- Validierung?
- Api Calls zusammenbauen und senden
- Keine Datenbank
- Deprovisionierung von alten CSV Dateien. Verschieben in processed und errorprocessed
- Vielleicht email senden wenn importiert wurde bzw ein Fehler geschmissen wurde


## Fazit

Ich habe mir die Sachen genauer angeschaut.
Tatsaechlich sind es nur zwei simple Hubspot API Calls, die anscheinend hier alles abbilden koennen.

Hier muessen Herr Weissler oder Herr Prinz ueberpruefen, on die folgenden Daten fuer einen Deal zum import reichen :

Ein Deal wird im Huspot wie folgt gespeichert ( ich denke Deal entspricht einer Buchung, bitte korrigieren falls ich falsch liege)
 
 - dealname
 - dealstage
 - pipeline
 - hubspot_owner_id'
 - closedate
 - amount
 - dealtype

Gewunescht war hier : 

- das Datum der getätigten Buchungen / mindestens der letzten Buchung
- die Anzahl der getätigten Buchungen (in einem gewissen Zeitraum)
- Volumen der Buchungen(Zeit oder €)

Fuer Datum koennen wir hier closedate nehmen und die anderen Felder natuerlich auch fuellen. Fuer das Volumen verwenden wir amount.
Fuer die Anzahl der Buchungen gibt es wahrscheinlich eine Funktion in Hubspot. 

Dazu gilt es nur fuer McArena, einen Api Key in Hubspot zu generieren, bzw evtl die Authentifizierung fuer die Api zu klaeren. 

Zur Implementierung :
Da dies wirklich kein grosses Hexenwerk ist, wuerde ich es wirklich ganz simpel halten. Evtl ein Python Script, das jeden Tag automatisch gestartet wird.
Es ueberprueft einen bestimmten Ordner ( Lokal oder per ftp) nach einer neuen Csv Datei, liest diese ein und sendet einfach die Calls an die Hubspot API.
Der Ordner wuerde zwei Unterordner besitzten, processed und errorprocessed, in die bearbeite Datei verschoben wird. 
Evtl sendet man hier noch eine Email, das importiert wurde oder ob es etwas falsch gelaufen ist.
Herr Timparano muesste somit nur einen automatisierten CSV export schreiben, der die CSV Datei in ein bestimmtes Verzeichnis ( oder per ftp) ablegt.

Nun wuerde es dann nur noch zu klaeren geben, wo das ganze Programm deployed wird. Besitzt MacArena evtl schon einen Server. 
Arbeiten Sie mit einer Webanwendung? Dann koennte man das alles auf einem Server installieren.
Sofern nicht, gilt es evlt einen minimalistischem Server zu mieten, der ftp und python unterstuetzt. 

## Schaetzung

### Api Prozessor

	- Recherche und Dokumentation : 1 Manntag
	- Implementierung des CSV Reader (mit Ftp oder aehnliches) : 1 Manntag
	- Implementierung der Api Aufrufe (inkl Testen) : 2 Manntage
	- Implementierung des Datei Prozessors und der versendeten Emails : 1 Manntag
	- Produktivfuehrung und Testen : 1 Manntag


### CSV export
		
	- Implementierung des Zusammenbaus der CSV : 1 Manntag
	- Anlegen des Jobs und Implementierung des Dateiprozessors : 1 Manntag
	 

## Stand 27.09.2019
   
Aufgaben nun unterteil nach Schaetzungen.

Todo der einzelnen Teilnehmer :

**McArena**

- Bereitstellen des Api Keys und eventuell eines Testbenutzers
- Bereitstellen eines Servers bzw Ueberlegungen zur Infrastruktur
- Eventuell Bereistellung einer Email Adresse. Diese wird als Absenderadresse verwendet, sofern ein Import durchgelaufen ist.
- Genaue Zusammenstellung der Daten, wie sie im Hubspot stehen

Die Dokumentation des Hubspots ist nur auf englisch (https://developers.hubspot.com/docs/overview). Somit muessen wir rausfinden, welche Attribute wir verwenden. Da McArena das bis jetzt manuell macht und es moeglich ist, sollte es nicht so schwer sein, die jeweilligen Api Aufrufe heraus zu finden. Evtl Hubspot einfach mal auf englisch stellen und so vorgehen wie gewohnt. Somit sollten die englischen Äquivalente erscheinen ( z.B. der englische Name fuer Buchung im Hubspot) 

**Forumedia**

-  Die Metastruktur der CSV festlegen ( Spaltennamen, Typen der Werte. etc) 
-  Bereistellen der CSV Dateien auf einem Server

**Ottavio**

So wie in den Schaetzungen definiert :

- Implementierung des CSV Reader
- Implementierung der API Aufrufe
- Implementierung des Dateiprozessors und der versendeten Email
- Produktivfuehrung und Testen
 
## HUBSPOT Test Environment

Name : petitcode-dev-6703886.com
url : https://app.hubspot.com/reports-dashboard/6703886/sales

hubspot_test:%ST~x~YxJ%7!A/e3


https://unix.stackexchange.com/questions/83221/how-to-create-a-ftp-user-with-specific-dir-access-only-on-a-centos-linux-ins

## TODO
- Properties im Hubspot anlegen:   (Die Api will alle Properties mit unterstrich statt Sonderzeichen und alles klein)

* Login : Einzeiliger Text
* Mitglied-Status : Einzeiliger Text ->mitglied_status
* Mg.Nr : Formatierte Zahl ->mg_nr
* Mehrwertsteuer : Einzeiliger Text
* Kontoinhaber : Einzeiliger Text
* Kontonummer : Einzeiliger Text
* Bankleitzahl : Zahl
* Name der Bank : Einzeiliger Text
* IBAN : Einzeiliger Text
* BIC : Einzeiliger Text
* SEPA Mandat vom : Einzeiliger Text ->sepa_mandat_vom
* SEPA Referenz : Einzeiliger Text ->sepa_referenz
* Datum der letzten Buchung : Einzeiliger Text
* Wert der letzten Buchung : Einzeiliger Text
* Kontaktkategorie : Einzeiliger Text

## Forummedia
zu CSV hinzufuegen

* Datum der letzten Buchung
* Wert der letzten Buchung
* Kontaktkategorie


CSV Datei : [Test Hubspot](/uploads/test-hubspot.csv "Test Hubspot")

## Testserver
server : 37.61.202.252
user : hubspot_test:9LNh5Sted>xqsDDf
touch /var/log/call_hubspot_api.log
/tmp/call_hubspot_api-lock


## Hubspot App

![Createhubspotapp](/uploads/createhubspotapp.png "Createhubspotapp")

## App Integration

![App Integration Hubspot](/uploads/app-integration-hubspot.png "App Integration Hubspot")


# Production

### Create Dirs

mkdir -p /home/hubspot_test/csvfiles/processed

mkdir -p /home/hubspot_test/csvfiles/errorprocessed

###

App definieren : 
https://app.hubspot.com/developer/6454294/application/207175

Hier muss aus die **Rewrite Url** definiert sein.
Diese muss so heissen wie dann spaeter in der OAuth Url verwendet.



### McArena Data


Link to Application in Hubspot : https://app.hubspot.com/developer/6454294/application/207175

OAuth Petitcode Dev : https://app.hubspot.com/oauth/authorize?client_id=e5851295-49ed-499d-be6f-6c7423526a87&redirect_uri=https://app.hubspot.com/reports-dashboard/6703886/sales&scope=contacts


OAuth-URL: https://app.hubspot.com/oauth/authorize?client_id=b1765eff-44de-4ec1-a7c7-34b51937c85a&scope=contacts
App-ID: 207219
Client-ID: b1765eff-44de-4ec1-a7c7-34b51937c85a
Client-Geheimnis: 24c49620-6252-4c19-b6b9-9154d0738b70
Rewrite Url : 

McArena OAuth : https://app.hubspot.com/oauth/authorize?client_id=b1765eff-44de-4ec1-a7c7-34b51937c85a&redirect_uri=https://app.hubspot.com/reports-dashboard/6703886/sales&scope=contacts


## get Token

![Get Token Mcarena](/uploads/get-token-mcarena.png "Get Token Mcarena"){.align-center}

Refresh Token : 0ac1531a-347d-4c04-8266-c26ce1247f38

### Zu klaren mit ETES

- ssh port verschieben





Repository :

git@github.com:ottipc/tool_hubspot_migration.git


## Live Server

SSH-Server: web-02.etes.de
SSH-Port: 22
SSH-Benutzer: mcarena
SSH-Passwort: Ais0ahRu

## Testergebnisse
- Email muss getrimmt werden
- Datum verschiedenes Format ( wobei egal)
- Wert der letzten Buchung kann leer sein.

Alles trimmen!!!


Error: Error at Importing : time data '..' does not match format '%d.%m.%Y' : 48

Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : time data '..' does not match format '%d.%m.%Y' in Line : 70

Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : {"validationResults":[{"isValid":false,"message":"Email address lenka_kurt@yahoo.de  is invalid","error":"INVALID_EMAIL","name":"email"}],"status":"error","message":"Property values were not valid","correlationId":"8e6ab6b7-d014-46b6-931f-9ea0894d37ac","requestId":"9e314b1e1b6a89911a48d76edbdaafee"} in Line : 209

Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : Email is empty, not able to persist in Hubspot in Line : 253

 Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : time data '..' does not match format '%d.%m.%Y' in Line : 340

Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : time data '..' does not match format '%d.%m.%Y' in Line : 343

 Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : time data '..' does not match format '%d.%m.%Y' in Line : 350

".." anstatt einem Date. Kommt oft vor!

Exception importing /home/hubspot_test/csvfiles/export-schorndorf_2019_12_05.corrected.csv : {"validationResults":[{"isValid":false,"message":"Email address test_fm is invalid","error":"INVALID_EMAIL","name":"email"}],"status":"error","message":"Property values were not valid","correlationId":"a580aece-c354-45b8-bcf8-4870e67cd223","requestId":"ce4b1e03690853c1e2bbc51bfdd0e1c3"} in Line : 397


h2. Exception auf Live


{ 
   "validationResults":[ 
      { 
         "isValid":false,
         "message":"Property \"kontonummer\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"kontonummer"
      },
      { 
         "isValid":false,
         "message":"Property \"bankleitzahl\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"bankleitzahl"
      },
      { 
         "isValid":false,
         "message":"Property \"sepa_mandat_vom\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"sepa_mandat_vom"
      },
      { 
         "isValid":false,
         "message":"Property \"iban\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"iban"
      },
      { 
         "isValid":false,
         "message":"Property \"mg_nr\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"mg_nr"
      },
      { 
         "isValid":false,
         "message":"Property \"name_der_bank\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"name_der_bank"
      },
      { 
         "isValid":false,
         "message":"Property \"sepa_referenz\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"sepa_referenz"
      },
      { 
         "isValid":false,
         "message":"Property \"kontoinhaber\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"kontoinhaber"
      },
      { 
         "isValid":false,
         "message":"Property \"login\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"login"
      },
      { 
         "isValid":false,
         "message":"Property \"bic\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"bic"
      },
      { 
         "isValid":false,
         "message":"Property \"mehrwertsteuer\" does not exist",
         "error":"PROPERTY_DOESNT_EXIST",
         "name":"mehrwertsteuer"
      }
   ],
   "status":"error",
   "message":"Property values were not valid",
   "correlationId":"a641bc45-cb62-476c-9b8c-3ad25d24b56b",
   "requestId":"4c3924a92d345e76c44c24af54551763"
}


## Stand

Hi, also der Impoter laeuft jetzt. Ihr solltet schon erste Mails bekommen haben. Schaut bitte auch im Spam Ordner nach. 
Ich habe jetzt mal nur CSV Dateien mir einer Zeile genommen. Eine kaputte, und eine richtige, das ihr die Testmails seht.
Die kaputten werden mit Zeitstempel in den ordner errorprocessed verschoben, wie man in der Email sieht.
Und die korrekten in den Ordner processed. Auch diese haben den Zeitstempel im Dateinamen, das man sieht, wann sie importiert wurden.

Uebrigens wollt ich noch bemerken, das ihr folgende Attribute ja nicht im Hubspot habt :

Der Importer sowie der CSV Export die Daten aber besitzen. Ihr muesstes sie nur im Hubspot wie oben beschrieben anlegen, dann koennen die ohne weiteres auch mit importiert werden.
Der Importer laeuft alle halbe Stunde.
Es liegt auf dem Server noch eine Datei rum in der ich die Fehler aus der grossen behoben habe. Es sind ungefaehr 430 Saetze und laesst sich komplett importieren : export-schorndorf_2019_12_05.corrected.csv
Diese habe ich nocht nicht auf eurem System importiert. Doch wenn ihr das ok gibt, werde ich diese importieren.

Ihr koennte diese auch selber auf dem Server von "processed" in den ordner "csvfiles" schieben, um eventuell schon mal zu sehen, wie das eigentlich funktioniert.
Sie wird alle 30 Minuten abgeholt, importiert, verschoben.
Ist eine Zeile kaputt im csv, so wird die Datei in errorprocessed verschoben und ihr bekommt eine Mail mit dem Dateinamen und der Zeile.

Ein update funktioniert ueber die Email. Ist die Email gleich, wird somit kein neuer angelegt.

Auf den etes Server werde ich es die naechsten Tage spielen. Macht fuer euch den Unterschied, das ihr einen anderen ftp account benutzt.

Gruesse

Ottavio

## Live Test

Exception importing /home/hubspot_test/csvfiles/test_hubspot.single.csv : {"validationResults":[{"isValid":false,"message":"1000Euro was not a valid number.","error":"INVALID_INTEGER","name":"wert_der_letzten_buchung"}],"status":"error","message":"Property values were not valid","correlationId":"9b3e5ce3-b29e-4729-b379-13d7c868aa41","requestId":"0525226a7a816a9884723cda9c5509ae"} in Line : 2


## Crontabs


```batchfile
# Cron für SuiteCRM
* * * * * php -f /var/www/vhosts/mcarena/htdocs/crm cron.php > /dev/null 2>&1

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

chmod 755 call_hubspot_api.log

chmod 755 log
touch crontab_hubspot_api.log
[mcarena@web-02 log]$ chmod 755 crontab_hubspot_api.log 


## Telefongespraech Lukas :

Zu den Werten :

- Geburtsdatum ( das schaue ich mit heute noch an) ..genau sowas passiert uebrigens, wenn die CSV nicht stimmt. Ich habe das getestet und es muss gehen. Heisst wohl 

Heisst nun geburtstag!!!!


// geburtstag

Team in Hubspot:        Geschaeftsleitung




> Team in Hubspot:        Hier wird den Kontakten Geschäftleitung 
> zugewiesen(Das Feld ist für interne Nutzung und sollte leer bleiben)
> Unternehmensname:       Hier wird "Hubspot" aufgeführt, auch dieses Feld 
> Telefonnummer und Name ist weisser :  Hier erschein der Nachname des Kontaktes

