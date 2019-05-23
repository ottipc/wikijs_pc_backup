<!-- TITLE: Webcrawler -->
<!-- SUBTITLE: A quick summary of Webcrawler Project -->

# Webcrawler

## Specification

We want to implement a webcrawler which scan the Internet for webpages and analyse the used Technologies. After manual validation of this Technologies, we want to make the customer an offer for a new Webpage constructed by Petitcode.
Petitcode here needs some Infomrationen by the scan which is really necessary :

- Customer name
- Technologies used at actual Webpage
- Contact Person of the potential Customer

The Crawler should run every day scannin new Urls which it havent scanned so far.


## Technical Details


## Crawler workflow 
1. Scan specified Sites
2. Send Emai to petitcode employes with found Data
3. Eventually save all related to a Database ( if we want to scan a lot of sides, it will be a lot of data, so we have to decide if this is necessary) 
## Important
* Customers only should note on for one time. If he is explicitly answering, that he dont want a homepage, it is forbidden to notify the customer twice.
* Are we are permitted to save data we use from google? I think not
* Where we getting urls we are scanning?   
	Answer : We getting infos about the soogle search of the branche
* How about saving the technical Details of the specified webpage?	
* Which Technics we should use if we write the crawler

## Solutions

There are already plenty of open source web crawlers in the web :https://bigdata-madesimple.com/top-50-open-source-web-crawlers-for-data-mining/

Maybe we can figure out,if one is useful for us, so we dont have to write a new application.

From quick research, the most referenced solutions (popularity, ratings, amount of google results) are:
Heritrix /	Java	Linux
Nutch	/ Java	Cross-platform
Scrapy /	Python	Cross-platform
PHP-Crawler	/ PHP	Cross-platform
WebSPHINX	/ Java	Cross-platform

Good thing is they are all open-source = free tools

## Action Points

abc..