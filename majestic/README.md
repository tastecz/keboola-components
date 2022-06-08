# Majestic (Medio)
**Created with love by Medio**

KBC Docker app for extracting data from Majestic (https://majestic.com). 

The Extractor gets multiple tables from Majestic tool and saves the data to Storage API. Date range of downloaded stats can be changed in configuration.


## Configuration Parameters

* **Output bucket** - Name of bucket where the data will be saved

* **Domain** - URL of the domain you want to download data from (e. g. ``https://www.example.cz/``). If left empty, data for all domains under authorized account will be downloaded. **NOTICE: Put exact naming used in Majestic tool.** 

* **Folder** - Name of the folder, where the domain reports are saved, use the whole string from URL after ``folder=`` query.

* **Username/Password** - Use Majestic credentials. 

## Output

Data are saved into tables **incrementally**:
* **Target_URL**	
* **Source_URL**	
* **Anchor_Text**
* **Source_Crawl_Date**
* **Source_First_Found_Date**
* **FlagNoFollow**	
* **FlagImageLink**		
* **FlagRedirect**		
* **FlagFrame**
* **FlagOldCrawl**		
* **FlagAltText**	
* **FlagMention**
* **SourceCitationFlow**		
* **SourceTrustFlow**	
* **TargetCitationFlow**		
* **TargetTrustFlow**
* **SourceTopicalTrustFlow_Topic_0**		
* **SourceTopicalTrustFlow_Value_0**		
* **RefDomainTopicalTrustFlow_Topic_0**		
* **RefDomainTopicalTrustFlow_Value_0**		
* **downLoaded** - date when the statistics were extracted