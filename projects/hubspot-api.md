<!-- TITLE: Hubspot Api -->
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

0111e11e-cc6a-41ec-acfc-4539ed27d6f0

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