# Sklik Zones (Medio)

**Created with love by Taste Medio**

This extractor allows you to extract Sklik Zones (for Publishers) and stats for them.

# Configuration
**Username / Password** - Use Sklik Account login credentials.

**dateTo** - end of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``today``) can be used.

**dateFrom** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used.

## Output

Data are saved into tables **incrementally**:

**zone** table, columns are:
- **id** 
- **name**
- **create_date**
- **web_id**

**zone_statistics** table, columns are:
- **date**
- **web_id,** 
- **web_name**
- **zone_id**
- **zone_name**
- **zone_impressions**
- **impressions**
- **clicks**
- **ctr**
- **commission**
- **web_impressions**
