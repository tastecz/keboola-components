# Seznam SSP extractor (Medio)

**Created with love by Taste Medio**

This extractor allows you to extract Seznam SSP Zones and stats for them with daily granularity.

# Configuration
**Username / Password** - Use Sklik Account login credentials.

**dateTo** - end of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``today``) can be used.

**dateFrom** - beginning of date range, for which you want statistics to be downloaded. 
Specific date (e. g. ``2018-01-01``) or relative term (``-365`` days) can be used.

## Output

Data are saved into tables **incrementally**:

**zone_stats** table, columns are:
- **date**
- **clicks** 
- **commission**
- **device**
- **height**
- **width**
- **impressions**
- **source**
- **zone_id**