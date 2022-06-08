# Biano.cz extractor
KBC Docker app for extracting data from Biano (http://biano.cz)

The Extractor gets list of campaign stats for previous day and saves the data to Storage API. Date of downloaded stats can be changed in configuration.


## Configuration

- **parameters**:
    - **username** - Username for Biano
    - **password** - Password for Biano
    - **bucket** - Name of bucket where the data will be saved
    - **since** *(optional)* - start date of downloaded stats (default is "-1 day")
    - **until** *(optional)* - end date of downloaded stats (default is "-1 day")
    - **eshopId** - Eshop Id in Biano
    - **showCategoryStats** *(optional)* ```true/false``` - based on that download table with daily stats for Biano categories (default is "false")

## Output

Data are saved into table **incrementally**

- **daily-stats** - contains daily marketing stats, columns are:
    - **eshopId** - primary key
    - **date** - primary key
    - **visits**   
    - **cost**
    - **bianoRevenue**
    - **bianoConversions**
    - **totalBianoRevenue**
    - **totalBianoConversions**

if showCategoryStat is true then following table is also saved:

- **daily-category-stats** - contains category stats, columns are:
    - **eshopId** - primary key
    - **date** - primary key
    - **categoryId** - primary key
    - **parentCategoryId**
    - **category**
    - **visits**
    - **products**    
    - **cost**
    - **bianoRevenue**
    - **totalBianoRevenue**
