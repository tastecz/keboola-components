# Google Analytics Data Import (Medio)

#### Note
All the described configuration expect that you are running it inside Keboola.

## Source
The file to be imported must follow these constraints:
- CSV file
- Maximally 1GB
- UTF-8 encoding

For detailed insight see [Google's constraints as it is](https://developers.google.com/analytics/devguides/config/mgmt/v3/data-import#format_and_constraints).

For multiple input tables, import is proceeded in `N` separate requests. Order may not be preserved.

### Split
Huge CSV files can not be imported in one request, because of memory limits. So, the CSV file is split into **1 000 000 chunks**. It means, that if your CSV file has **2 565 100 lines**, there will be proceeded **3 requests**.

## Required configuration
Every writer configuration must provide the following configuration in `JSON` format:
```json
{
  "account_id": "123456789",
  "web_property_id": "UA-123456789-1",
  "custom_data_source_id": "abxHghajCkaE4-E"
}
```
## Optional configuration
### Transformation
#### Mapping
During import, all the included columns are mapped to `ga:yourColumnName`. To affect this behavior you can pass your desired mapping via `mapping` field.
Your custom mapping is merged with the default one mentioned above. Unknown columns are ignored. The mapping is applied to all input tables.

```json
{
  "mapping": {
      "yourColumnName": "ga:date",
      "yourColumnName2": "ga:medium"
  }
}
```
#### Formatting
During the import you have to obey Google's format for some data types. For instance, `ga:date` must be converted to `YYYYMMDD` [date format](https://developers.google.com/analytics/devguides/reporting/core/dimsmets#view=detail&group=time&jump=ga_date). To simplify things, `formatting` field has been introduced.
```json
{
  "formatting": {
      "yourColumnName": {"type": "date", "format": "Ymd"},
      "yourColumnName2": {"type": "int", "format": 8},
      "yourColumnName3": {"type": "float"},
      "yourColumnName4": {"type": "string", "format": "%s..."},
      "yourColumnName5": {"type": "code", "format": "%s > 5 ? 1 : 0"},
      "yourColumnName6": {"type": "code", "format": "%1$s > 5 ? %1$s : 0"}
  }
}
```
##### Available types
- **date** [using php format](https://secure.php.net/manual/en/function.date.php)
- **int** within base (octal, decimal, ...) [using php intval function](https://secure.php.net/manual/en/function.intval.php)
- **float** [using php floatval function](https://secure.php.net/manual/en/function.floatval.php)
- **double** as alias for float
- **bool** [using php boolval function](https://secure.php.net/manual/en/function.boolval.php)
- **string** [using php sprintf function](https://secure.php.net/manual/en/function.sprintf.php)
- **code** [using php eval function](https://secure.php.net/manual/en/function.eval.php) to execute arbitrary php code. `%s` and `%1$s` is placeholder for your current record.

#### Cut
In case your CSV file contains columns which are not necessary for target data import, you can cut off them. Use `cut` field with list of ignored columns.
```json
{
  "cut": ["yourColumnName", "yourColumnName2"]
}
```

The transformation goes in this particular order: cutting, formatting, mapping. You always pass the original name of a column - as mapping phase is the last one.

### Result
By default, there is a waiting phase for your result. During the phase is validated your import.
If your import fail, Keboola job too.
If you do not want to wait and rather look into the result in Google Analytics, you can pass `validation` field with `false` value.
```json
{
  "validation": false
}
```
Optionally you can choose break between validations. Default and minimal break is 1 second. To increase the value,
pass `break` field within value in seconds.
```json
{
  "break": 1
}
```