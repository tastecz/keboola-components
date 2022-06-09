# **Medio Attribution Tool**

Custom application in Keboola Connection for attribution modeling experimentation.

See [www.mediointeractive.com/attribution](http://www.mediointeractive.com/attribution) for overall introduction.



# Table of shortcuts {#table-of-shortcuts}


<table>
  <tr>
   <td><strong>shotcut</strong>
   </td>
   <td><strong>explanation</strong>
   </td>
  </tr>
  <tr>
   <td>AM
   </td>
   <td>Attribution Model
   </td>
  </tr>
  <tr>
   <td>CAM
   </td>
   <td>Custom Attribution Model
   </td>
  </tr>
  <tr>
   <td>GA
   </td>
   <td>Google Analytics
   </td>
  </tr>
  <tr>
   <td>JSON
   </td>
   <td>JavaScript Object Notation
   </td>
  </tr>
  <tr>
   <td>KBC
   </td>
   <td>Keboola Connection
   </td>
  </tr>
  <tr>
   <td>MAT
   </td>
   <td>Medio Attribution Tool (application itself)
   </td>
  </tr>
</table>



# Data preparation {#data-preparation}

Before you start with application (APP) is necessary prepare data for attribution testing to following format. Every line in the table represents a single interaction – a website visit, mobile app launch, banner impression, ad click-through, reading an email, helpdesk phone call, offline shop visit. All interactions which are considered as “conversions” like newsletter sign-up or completed purchase must have assigned value. Types of interaction are distinguished in “hitType” column no other columns are considered due to different channel grouping settings for each client.

Please be sure that you also mark “direct” traffic as “direct” in this column.


## Input data {#input-data}

Table of all events for attribution:



1. **visitor_id** - unique identificator for each visitor
2. **date_time** - event timestamp
3. **hitType** - event or “action” type
4. campaign - traffic campaign
5. source - traffic source
6. medium - traffic medium
7. **revenue** - conversion value
8. **weight** - empty column % weight of interaction calculated by MAT
9. **revenue_attribution_value** - empty column, interaction value calculated by MAT

Bold columns are mandatory, campaign, source and medium a recommended for results interpretation.

Column names can be different, this needs to be reflected in following configuration.


# MAT activation and settings {#mat-activation-and-settings}

APP is currently available in APP store in Keboola (KBC) just click at “Applications” in bottom of left menu and write “attrib” to search field.

By clicking to “More” will you add APP to your project.

Before you create first configuration you must confirm T&C and licence agreement.

Next step is typical KBC UI for settings input and output mapping. Input and output can be the same table in storage. Last part is for configuration JSON described in following part of document.

MAT output file is “results.csv” used for output mapping as you can see at the bottom of following picture.

# MAT configuration JSON {#mat-configuration-json}

MAT currently support various attribution models:


        ► First click attribution

		► Last click attribution

		► Last non-direct click attribution

		► Linear attribution

		► Non-direct linear attribution

		► Position based attribution

		► Non-direct position based attribution 	

All these models can be used as they are by simple configuration which contains:


## Basic settings {#basic-settings}

Following list of keys and key values are used for using MAT and predefined attribution models:
* **sortInputFile** - optional key for sorting output file
* **visitorColumn**- mandatory settings of unique identifier column in input data
* **timestampColumn**- mandatory settings of timestamp in input data
* **interactionType**- maattribution input data
* **task** - define specific run of attribution model
* **attributionModel**- mandatory key determining type of attribution (allowed values):

        * firstClick
        * lastClick
        * linear
        * lastNonDirect
        * linear
        * linearNonDirect
        * positionBased
        * positionBasedNonDirect

    		


* **inputValueColumn** - mandatory key for conversion value column definition 
* **outputWeightColumn**- key for column to save percentage share of each row at conversion
* **outputValueColumn** - key for hit revenue share column

## Final configuration {#final-configuration}

By combining all previous functions you can get following configuration:
```json
{
  "sortInputFile": true,
  "visitorColumn": "visitor_id",
  "timestampColumn": "date_time",
  "interactionType": "hitType",
  "tasks": [
	{
  	"attributionModel": "linear",
  	"inputValueColumn": "revenue",
  	"outputWeightColumn": "weight",
  	"outputValueColumn": "revenue_attribution_value"
	}
  ]
}

```

Just take it and put it to MAT and click “run”. By running this code you will get sorted output of your data calculated by linear attribution. Attribution paths will be sorted by user and time in ascending order.


# CAM configuration {#cam-configuration}

MAT allows to modified standard AM to create CAM by your specific needs with custom exceptions. In every case designed shape will by affected by number of interactions in each attribution path.

_Few examples: 1) First (45%) - Last (55%), 2) 35% - 20% - 45%_


## Additional task keys {#additional-task-keys}

To create CAM base or your need are used additional keys and key valuesConfiguration JSON can look like following, setting reflect names of columns of input table above.
* **startDate** - can be used for attribution calculation in specific time frame
* **endDate**- specific time frame can be limited also from top
* **lookbackWindow**- allows you create lookback window for “startDate”
* **shares**- key array for customization of maximum share for specific hitTypes
* **weights**- key array for setting of weight to specific hitTypes

“Share” key can  be used to create exceptions like: “no matter how many emails customer opens, but **ALL** “open” interactions together in one conversion path will have 10% of conversion value”. Key value is taken as maximum no matter to number of interactions.

“Weights” key is useful in cases when you want to rate or limit some type of interactions versus other types, key value works like multiplier zero is allowed for total limitation.

All togerher:
```json
{
  "sortInputFile": true,
  "visitorColumn": "visitor_id",
  "timestampColumn": "date_time",
  "interactionType": "hitType",
  "tasks": [
	{
  	"startDate": "2015-01-01",
  	"endDate": "2016-03-13",
  	"lookbackWindow": 90,
  	"shares": {
    	"conversion": 0
  	},
  	"weights": {
    	"view": 0
  	},
  	"attributionModel": "linear",
  	"inputValueColumn": "revenue",
  	"outputWeightColumn": "weight",
  	"outputValueColumn": "revenue_attribution_value"
	}
  ]
}

```

## Position task keys {#position-task-keys}

MAT allows to create CAM by two following position tasks.
* **firstInteraction** - can be used for assign value to first interaction in conversion path
* **lastInteraction**- specific key  for assign value to last interaction in conversion path

Both values are taken in percentages so 10 means 10%.

Configuration for U-shaped CAM with 40% - 20% - 40% looks like following:
```json
 {
  "sortInputFile": true,
  "visitorColumn": "visitor_id",
  "timestampColumn": "date_time",
  "interactionType": "hitType",
  "tasks": [
	{
  	"startDate": "2015-01-01",
  	"endDate": "2016-03-13",
  	"lookbackWindow": 90,
  	"firstInteraction": 40,
  	"lastInteraction": 40,
  	"inputValueColumn": "revenue",
  	"outputWeightColumn": "weight",
  	"outputValueColumn": "revenue_attribution_value"
	}
  ]
}

```