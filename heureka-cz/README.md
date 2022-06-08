# Heureka.cz extractor
**Created with love by Medio**

KBC Docker app for extracting data from Heureka (http://heureka.cz). 

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.


## Configuration

- **parameters**:
    - **username** - Username to Heureka
    - **password** - Password to Heureka
    - **bucket** - Name of bucket where the data will be saved
    - **since** *(optional)* - start date of downloaded stats (default is "-1 day")
    - **until** *(optional)* - end date of downloaded stats (default is "-1 day")
    - **eshopId** - Eshop Id in Heureka
    - **showSources** ```true/false``` - If ```true```, statistics will be separated for each portal (heureka.cz,nejlepsiceny.cz,srovnani.cen), otherwise only summed figures will be returned 

## Output

Data are saved into table **incrementally**:

**stats** - contains marketing stats, columns are:
- **eshopId** 
- **date** 
- **visits**   
- **cpc** 
- **spend**
- **conversion_rates** 
- **orders** 
- **aov**
- **transaction_revenue**
- **pno**
- **source** `source is downloaded by setting optional parameter showSources to true`


> **NOTICE!**
> - Data can change for last 30 days
> - Data from previous day are available at morning