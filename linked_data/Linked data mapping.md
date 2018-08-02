# General Bikeshare Feed Specification (GBFS) Linked Data Mapping


## Files
The different file types have been left behind and have been replaced with classes for a system, station and bike.


## File Requirements

### Localization
Instead of having multiple files, a certain resource can be described in multiple languages using language tags. Eg. `"Public name of the station"@en` and `"Nom public de la station"@fr`

## Field Definitions

### Output Format
Every JSON file presented in this specification contains the same common header information at the top level of the JSON response object:


Field Name          | Required  | Linked Data
--------------------| ----------| ----------
last_updated        | Yes       | gbfs:last_updated
ttl                 | Yes       | gbfs:ttl
data                | Yes       | Left out


### gbfs.json


Field Name              | Linked Data
------------------------| ----------
language  | Use language tags
  \- feeds               | Can be represented using gbfs:Feed
  \- name                | gbfs:name
  \- url                 | Left out


### system_information.json

> A class gbfs:System was added to represent a system

Field Name        | Linked data
------------------| ----------
system_id         | gbfs:system_id 
language          | Use language tags
name              | gbfs:name
short_name        | gbfs:short_name
operator          | gbfs:operator
url               | gbfs:url
purchase_url      | gbfs:purchase_url
start_date        | gbfs:start_date
phone_number      | foaf:phone
email             | foaf:mbox
timezone          | gbfs:timezone
license_url       | gbfs:license_url


### station_information.json

> A class gbfs:Station was added to represent a station


Field Name        | Linked data
------------------| ----------
stations          | Left out
\- station_id      | gbfs:station_id
\- name            | gbfs:name
\- short_name      | gbfs:short_name
\- lat             | geo:lat
\- lon             | geo:long
\- address         | gbfs:address
\- cross_street    | gbfs:cross_street 
\- region_id       | gbfs:region_id
\- post_code       | vcard:postal-code
\- rental_methods  | Class: gbfs:RentalMethod, subclasses:<br /><ul><li>gbfs:KEY </li> <li>gbfs:CREDITCARD</li> <li>gbfs:PAYPASS</li> <li>gbfs:APPLEPAY</li> <li>gbfs:ANDROIDPAY</li> <li>gbfs:TRANSITCARD</li> <li>gbfs:ACCOUNTNUMBER</li> <li>gbfs:PHONE</li> </ul>
\- capacity        | gbfs:capacity

### station_status.json

Field Name            | Linked data
--------------------- | ----------
stations              | Left out
\- station_id          | gbfs:station_id
\- num_bikes_available | gbfs:num_bikes_available
\- num_bikes_disabled  | gbfs:num_bikes_disabled
\- num_docks_available | gbfs:num_docks_available
\- num_docks_disabled  | gbfs: num_docks_disabled
\- is_installed        | gbfs:is_installed
\- is_renting          | gbfs:is_renting
\- is_returning        | gbfs:is_returning
\- last_reported       | gbfs:last_reported

### free_bike_status.json

> A class gbfs:Bike has been added to describe a bike

Field Name        | Linked data
------------------| ----------
bikes             | Left out
\- bike_id         | gbfs:bike_id
\- lat             | geo:lat
\- lon             | geo:long
\- is_reserved     | gbfs:is_reserved
\- is_disabled     | gbfs:is_disabled

### system_hours.json


Field Name          | RDefines
--------------------| ----------
rental_hours       | gbfs:rental_hour
\- user_types        | gbfs:is_member
\- days              | gbfs:day
\- start_time        | gbfs:start_time
\- end_time          | gbfs:end_time

### system_calendar.json

> A class gbfs:Calendar has been added

Field Name          |  Defines
--------------------| ----------
calendars           |  gbfs:calendar 
\- start_month       | gbfs:start_date
\- start_day         | gbfs:start_date
\- start_year        | gbfs:start_date
\- end_month         | gbfs:end_date
\- end_day           | gbfs:end_date
\- end_year          | gbfs:end_date

### system_regions.json
> Replaced by vcard:region

### system_pricing_plans.json

> A class gbfs:Plan has been added to describe a pricing plan


Field Name        | Defines
------------------| ----------
plans             | Left out
\- plan_id         | gbfs:plan_id
\- url             | gbfs:url
\- name            | gbfs:name
\- currency        | gbfs:currency
\- price           | gbfs:price
\- is_taxable      | gbfs:is_taxable
\- description     | rdfs:comment

### system_alerts.json
> A class gbfs:Alert has been added to describe an alert

Field Name        | Defines
----------------- | ----------
alerts            | Left out
\- alert_id        | gbfs:alert_id
\- type            | gbfs:AlertType - valid values are: <ul><li>gbfs:SYSTEM_CLOSURE</li> <li>gbfs:STATION_CLOSURE</li> <li>gbfs:STATION_MOVE</li> <li>gbfs:OTHER</li> </ul>
\- times           | gbfs:AlertTime
&emsp;- start     | gbfs:start
&emsp;- end       | gbfs:end
\- station_ids     | gbfs:station_id
\- region_ids      | gbfs:region_id
\- url             | gbfs:url
\- summary         | dct:abstract
\- description     | rdfs:comment
\- last_updated    | dct:modified


## Disclaimers

_Apple Pay, PayPass and other third-party product and service names are trademarks or registered trademarks of their respective owners._

## License

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/).
