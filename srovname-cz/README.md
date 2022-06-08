# Srovnáme.cz (Medio) extractor
**Created with love by Medio**

KBC Docker app for extracting data from Srovname.cz (http://srovname.cz). Get your daily impressions, clicks, cost and conversion data.

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.

# Configuration

* **Since** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used.

* **Output bucket** - Name of bucket where the data will be saved

* **Username / Password** - Use Srovname.cz login credentials.

# Output

Data are saved into table **incrementally**:

**stats** table - contains marketing stats, columns are:
* **date**
* **visits**
* **cpc**
* **spend**
* **conversion_rates**
* **orders**
* **aov**
* **transaction_revenue**
* **pno**

>NOTICE!
> Data can change for last 30 days