<!-- TITLE: Webcrawler -->
<!-- SUBTITLE: A quick summary of Webcrawler Project -->

# Webcrawler

## Specification

We want to implement a webcrawler to scan the internet for websites and webshops and analyze their applied technologies and most recent update or change dates. After manual validation of the technologies, the idea is to contact the lead and propose our sefices to help them update or renew their digital presence.

To that end, petitcode needs sthe following information to be revealed by the scan:

- CEO name
- Technologies used at present digital presence
- Date of most recent changes
- Applied technologies on website

The crawler should be fed with URLs from industries and geographies as defined for campaigns periodically set up for direct marketing and sales.


## Technical Details

Existing crawlers should be tested for the above functionality. 


## Data Privacy Related Procedures & Questions

* URLs will be identified and collected by using a commercially available lead database.
* Leads will only be contacted once.  We will not store any lead data from non-interested contacts other than their URL, the date we contacted them and that they did not want to go forward with pc.  These data have not been provided by the lead.
* Are we are permitted to store data we acquird from Google search?  To be determined (By whom? When?)
* Are we permitted to store the outcome of a scan?  Most certainly yes, temporarily until a lead enters into a sales dialog with us or we give up on the lead and all data will be deleted with the exception of those stated above.	
* Does it make sense for us to develop our own crawler?  If so, which technics should we be using?  A preliminary answer is: No, see below.


## Solutions

There are already plenty of open source web crawlers in the web :https://bigdata-madesimple.com/top-50-open-source-web-crawlers-for-data-mining/

We should examine which of these would be useful for the task so we don't have to write our own.

From quick research, the most referenced solutions by popularity, ratings and number of Google results are:
- Heritrix /	Java	Linux
- Nutch	/ Java	Cross-platform
- Scrapy /	Python	Cross-platform
- PHP-Crawler	/ PHP	Cross-platform
- WebSPHINX	/ Java	Cross-platform

Good thing is they are all open-source = free tools

*UPDATE* : the options above seem quite complicated for first time usage. Please consider the following: https://www.octoparse.com/blog/free-online-web-crawler-tool

## Action Points

* 1 - Identify the most promising crawler from above list [to do: Lukas & Axel, < 28.5.2019]
* 2 - Understand use of selected crawler and make a short test run using 20 known URLs [to do: Guy 28./29.5.2019]]
* 3 - Review results and (a) change crawler or (b) hone crawler use or (c) go forward with same crawler [to do: Guy & Axel, < 30.5.2019] 
* 3 - Define a first campaign by target industry and geography, start time, pc resource and potential cost [Seb, Guy & Axel < 4.6.2019]
* 4 - Write a script for the approach to the lead - both phone and email versions [Axel < 4.6.2019]
* 5 - Write a sales process to follow up on responsive leads [Axel < 4.6.2019]
* 6 - Pre-select targets from Bisnode Hoppenstedt database, collect URLs, run crawler, begin contacting [Guy, Lukas & Axel < 4.6.2019]
* 7 - Review results from crawler, (a) change crawler or (b) hone crawler use or (c) go forward with same crawler and process - depending on quality of the outcome [Guy & Axel < 4.6.2019]
* 8 - Reiterate to # 6 [to do: see above]