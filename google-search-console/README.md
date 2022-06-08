# Google Search Console (Medio)
Updated: 25.9.2019

**Created with love by Medio**

KBC Docker app for extracting data from Google Search Console (http://search.google.com). 

The Extractor gets multiple tables from GSC tool and saves the data to Storage API. Date range of downloaded stats can be changed in configuration.


## Configuration

**Authorization**
- Use Google Account Sign In interface. Log In under account which have access to GSC you want extract data from.

**Other Parameters**:

* **Since** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-486`` days) can be used. 486 days is current maximum that GSC will return.

* **Until** - end of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``today``) can be used

* **Output bucket** - Name of bucket where the data will be saved

* **Domain** - URL of the domain you want to download data from (e. g. ``https://www.example.cz/``). If left empty, data for all domains under authorized account will be downloaded.


## Limits
* **Daily download limits** - You can select number of daily results for tables keywords, pages and landing_pages. Note that in GSC interface this limit is set to default 10 per day. 

* ~~**Request limit**~~ - deprecated

## Output

Data are saved into tables **incrementally**:

~~**errors** table~~ - deprecated

**keywords** table - contains keywords (in GSC terminology queries) performance statistics from Google SE, columns are:
- **clicks**
- **impressions**
- **keys**
- **date**

**pages** table - contains page performance statistics from Google SE, columns are:
- **clicks**
- **impressions**
- **page**
- **date**

**landing pages** table - contains keyword performance statistics from Google SE grouped by pages, columns are:
- **clicks**
- **impressions**
- **page**
- **date**
- **keyword**


**sitemap** table - contains statistics of submitted/indexed pages in Google SE , columns are:
- **indexed**
- **submitted**
- **downloaded** - date when the statistics were extracted

These tables may or may not give the same totals as some information are witheld by GSC (for example to protect user privacy) according to its [documentation] (https://support.google.com/webmasters/answer/7576553?hl=en&visit_id=637024176655847526-2390367239&rd=1). Details of possible differences are covered by the paragraph Data discrepancies. 