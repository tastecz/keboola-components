# Pricemania.sk (Medio)
**Created with love by Taste Medio**

Pricemania.sk reports and statistics extractor. Get your daily impressions, clicks, cost and conversion data. Saves the data to Storage API.

# Configuration

* **Since** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used.

* **Output bucket** - Name of bucket where the data will be saved

* **Username / Password** - Use Pricemania.sk login credentials.



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


