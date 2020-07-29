<!-- TITLE: Spenden -->
<!-- SUBTITLE: A quick summary of Spenden -->

# Anforderungen

## Kurzfassung Anforderungen

> EKKK braucht ein CRM und Accounting Tool.
> 
> Hierzu müssen einige Anpasungen erstellt werden, sodass alle Daten der Spender und der Mitglieder vernünftig verwaltet werden können. 
> 
> Das wichtigste ist, dass alle Daten der unterschiedlichen Spenden den jeweiligen Accounts/ Spendern zugeordnet werden. 
> 
> Es muss daher ein Upsate aus Lexoffice in Hubspot passieren. Weil aus lexoffice die Bankaten kommen.
> 
> Wenn ein kontakt noch nicht existiert, dann muss er angelegt werden. Am besten wäre es für die EKKK, wenn Sie dafür so wenige Tools wie möglich händisch pflegen müssen. 
> 
> Beu Hubspot kann man diverse Apps auf die Plattform coden. Hierzu steht uns ein MItarbeiter zur Verfügung.
> 


### Eingang von Spenden (Dies sind Wege wie eine Spende bei uns ankommt)

* Bankkonten
* Paypal
* Crowdfunding Plattformen 
* Manuelle Zahlungen: Barspenden
* Mitgliedseinzug
* Lastschriften (Dauerspender werden von uns in OH angelegt und dann in die Bank per CSV eingespielt)


## Zu klaeren

- Kann Lexoffice einen CSV Import?

Anscheinend ja, aber es gilt zu pruefen, in wie weit dieser Konfigurierbar ist und sich die Metadaten mit den Stammdaten aus Hubspot deckt

https://support.lexoffice.de/de-form/articles/1829211-import-elektronischer-kontoauszug-uber-csv-datei

- Anlegen der Stammdaten in Hubspot?

> Da eine Zahlung evtl. diversen Kriterien zugeordnet werden muss und dies in Lexoffice nicht so expliziert möglich ist, muss der erste Kontakt in Hubspot angelegt werden. 


> Die angelegten Fibukonten in Hubspot sollten möglichst so sein(zur Zeit auch so in Benefit angelegt):
* Geldtransit
* Durchlaufende Posten
* Sonstige Kosten
* Kontoführung
* Mitgliedsbeiträge
* Dauerspenden monatlich / vierteljährlich / halbjährlich / jährlich
* Kondolenzspenden
* Geburtstage / Jubiläen u. sonstige
* Veranstaltungsspenden
* Fundraising-Aktionen
* Regelmäßige sonstige Spenden
* Sonstige Spenden einmalig und erstmalig
* Kollekten
* Bußgelder
* Stiftungen 
*Erben

..könnten dann zusammengefasst werden und dann nach Lexoffice per CSV auf die entsprechenden Buchhaltungskonten eingespielt werden.


## Problematik 

`Wir erhalten Zahlungseingänge mit nur einem Namen ohne eine Adresse und es gibt auch noch keine weiteren Informationen – ob die Spende z.B. über eine Beerdigung oder Geburtstag, oder sonstige Aktion getätigt worden ist. Dann wird der Eingang verbucht und nachdem wir dann weitere Informationen erhalten haben z.B. Adresse etc. erhält der Spender seine Spendenquittung.
In Lexoffice wird die Spende nur einfach als „Spendeneingang“ Fibu Konto z.B. 2001 gebucht.
`



# Open Hearts

![Stammsatz Aufbau Openhearts](/uploads/spenden/stammsatz-aufbau-openhearts.png "Stammsatz Aufbau Openhearts")

![Sollstellung Lastschrift Uber Stammsatz Anlegen](/uploads/spenden/sollstellung-lastschrift-uber-stammsatz-anlegen.png "Sollstellung Lastschrift Uber Stammsatz Anlegen")

![Quittungsjournal Openhearts](/uploads/spenden/quittungsjournal-openhearts.png "Quittungsjournal Openhearts")

![Zahlungseingang Kontoauszug](/uploads/spenden/zahlungseingang-kontoauszug.png "Zahlungseingang Kontoauszug")

![Stammsatz Richard Melz](/uploads/spenden/stammsatz-richard-melz.png "Stammsatz Richard Melz")

![Zahlungseingang Kontoauszug](/uploads/spenden/zahlungseingang-kontoauszug.png "Zahlungseingang Kontoauszug")




# Fragen und Fazit

## Fragen

* Gilt es schon vorhandene Stammdaten aus Open Hearts zu importieren? Besitzt Open Hearts einen Export?
* Welche Rolle spielt Buchungsbutler?
* Daten aus Lexoffice zu Hubspot oder umkehrt?

## Fazit

Wie schon erwaehnt, will man manuelle Eingaben vermeiden und alles per Importer regeln. Im Hubspot laesst sich alles per Api importieren, was man auch anlegen kann. Somit gilt es festzustellen, was man aus den Stammdaten der Spender **NICHT** in Hubspot abbilden kann. Diese Funktionlitaeten muessen programmiert werden.
Sollte im Hubspot tatsaechlich alles abbildbar sein, wird gar kein Frontend benoetigt, sondern nur diverse Importer und Exporter zu den einzelnen Anwendungen : Lexoffice, Hubspot.. ?
Man muss festellen, wie das in Hubspot mit den Quittungen und dem Journal ist, das wird wohl programmiert werden muessen. Somit benoetigt man eine eigene Datenbank, eventuell eben mit der GUI.
Lexoffice hat einen CSV Import, somit ist das Einbinden der Kontodaten hier anscheinend auch kein Problem.
Das Problem mit den Quittungen, die weit nach Spendeneingang ausgestellt werden, ist programmatisch gar kein Problem.

Wie schon festgestellt wurde, gilt es nun rauszufinden, was denn eigentlich programmiert werden muss, und deswegen ...

## TODO

- Jemand der sich gut mit Hubspot und den Stammdaten der Spender auskennt, sollte mal einen maximalen Bespielsatz in Hubspot anlegen, um zu sehen, was alles moeglich ist zur Abblidung der gewollten Daten. Kein Programmierer!
- Jemand, der sich mit Lexoffice auskennt, sollte eine Beispiel CSV erstellen, die das Schema einer zu wuenschenden Importdatei representiert. Kein Programmierer!
- Anschliessend kann man diese Metadaten abgleichen, den Satz aus Hubspot in eine CSV oder per Api abrufen und genau abschaetzen, was noch programmiert muss und was zu Problemen fuehren kann. Programmierer! 
