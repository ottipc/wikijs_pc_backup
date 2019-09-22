<!-- TITLE: Hubspot Api -->
<!-- SUBTITLE: A quick summary of Hubspot Api -->

# Header

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

Create or Update Contact : https://developers.hubspot.com/docs/methods/contacts/create_or_update

komischerweise hier keine Email dabei?





