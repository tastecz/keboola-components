**Created with love by Taste Medio**

Sklik (Medio) extractor downloads campaign statistics on AdGroups level. 

# Requirements
* Access to Sklik Account,
* "Read Only" permission rights.



# Configuration
**Mapping**

First, you need to configure 3 output tables in Table Output Mapping. 

Setting up primary keys nad incremental loading is recommended.

**Authorization**

There are two possible ways:

1. *Username / Password* - Use Sklik Account login credentials.

2. *Token* - Use created token via Sklik interface. Follow instructions below
* Logged in your Sklik Account, click on your account in top right corner (where your email adress is)
* Go to Settings ("Nastavení" in czech language settings), 
* Click on Generate New API key ("Vygenerovat nový API klíè"). 

* NOTICE: Part of the token on the picture is hidden, for correct settings it is necessary to set up the whole API key (with email adress on the end included).

**Other Parameters**
* *User ID* - Unique user ID
You can find it in Sklik Administration > Accounts ("Úèty"). Place mouse cursor on desired account. User ID is in the link. If left empty, statistics for all accounts will be downloaded.

* *Date from* - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used.

* *Date to* - end of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``today``) can be used.

## JSON
```
{
  "parameters": {
    "api": {
      "username": "user@domain.cz",
      "#password": " cdv43ervthg56j",
      "#token": "cdfd443fd4e43frv"
      "user_id": 666
      "timeout": 30,
    },
    "dateFrom": "- 10 days",
    "dateTo": "today"
  }
}
```