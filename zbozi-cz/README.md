# Zbozi.cz extractor
**Created with love by Medio**

KBC Docker app for extracting data from Zboží.cz (http://zbozi.cz). Get your daily impressions, clicks, cost and conversion data.

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.

# Configuration Parameters
* **Since** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used,

* **Output bucket** - Name of bucket where the data will be saved,

* **Username / Password** - Use Zbozi.cz login credentials,

* **PremiseId** * - Premise Id in Zboží.cz,

* **Download detailed category reports** * - ``true/false`` If ``true``, additional table **"categories"** (see description below in "Output" part). 

* *Download detailed category reports since* - beginning of date range, for which you want statistics in **"categories"** table to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used,

# Output
Data are saved into table incrementally:

**stats** table - contains marketing stats, columns are:
* **premiseId**
* **date**
* **visits**
* **cpc**
* **spend**
* **conversion_rates**
* **orders**
* **aov**
* **transaction_revenue**
* **pno**

**categories** table - will be extracted only if parameter **Download detailed category reports** will be set to ``true``. 

Contains marketing stats sliced by categories, columns are:
* **premiseId**
* **date**
* **exportId**
* **id_kategorie**
* **Nazev_kategorie**
* **Zobrazeni**
* **Prokliky**
* **Celkova_cena_za_prokliky**
* **Pocet_konverzi**
* **pno**

>NOTICE!
>Data can change for last 30 days