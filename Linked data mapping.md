# General Bikeshare Feed Specification (GBFS) Mapping


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
last_updated        | Yes       | dcterms:modified
ttl                 | Yes       | gbfs:ttl
data                | Yes       | Left out


### gbfs.json


Field Name              | Linked Data
------------------------| ----------
_language_ **use standard tag** | Use language tags
  \- feeds               | Can be represented using gbfs:Feed
  \- name                | Left out
  \- url                 | Left out


### system_information.json

> A class gbfs:System was added to represent a system

Field Name        | Linked data
------------------| ----------
system_id         | gbfs:system_id 
language          | gbfs:language
name              | gbfs:name
short_name        | gbfs:short_name
operator          | gbfs:operator
url               | gbfs:url
purchase_url      | gbfs:purchase_url
start_date        | gbfs:start_date
phone_number      | foaf:phone
email             | foaf:mbox
timezone          | transit:timezone
license_url       | gbfs:license_url


### station_information.json

> A class gbfs:Station was added to represent a station


Field Name        | Linked data
------------------| ----------
stations          | Left out
\- station_id      | gbfs:station_id
\- short_name      | gbfs:short_name
\- lat             | geo:lat
\- lon             | geo:long
\- address         | gbfs:address
\- cross_street    | gbfs:cross_street 
\- region_id       | vcard:region
\- post_code       | vcard:postal-code
\- rental_methods  | Class: gbfs:rental_method, subclasses:<br /><ul><li>gbfs:KEY </li> <li>gbfs:CREDITCARD</li> <li>gbfs:PAYPASS</li> <li>gbfs:APPLEPAY</li> <li>gbfs:ANDROIDPAY</li> <li>gbfs:TRANSITCARD</li> <li>gbfs:ACCOUNTNUMBER</li> <li>gbfs:PHONE</li> </ul>
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
rental_hours        | gbfs:rental_hour_member and gbfs:rental_hour_non_member
\- user_types        | replaced by gbfs:rental_hour_member and gbfs:rental_hour_non_member
\- days              | replaced by gbfs:rental_hour_member and gbfs:rental_hour_non_member
\- start_time        | replaced by gbfs:rental_hour_member and gbfs:rental_hour_non_member
\- end_time          | replaced by gbfs:rental_hour_member and gbfs:rental_hour_non_member

Rental hours can be expressed as following:

```
<example.com/system_1> gbfs:rental_hour_member "mon 08:00:00 - 18:00:00"
<example.com/system_1> gbfs:rental_hour_member "mon 07:30:00 - 18:30:00"
```

### system_calendar.json


Field Name          |  Defines
--------------------| ----------
calendars           |  gbfs:calendar 
\- start_month       | Replaced by gbfs:calendar
\- start_day         | Replaced by gbfs:calendar
\- start_year        | Replaced by gbfs:calendar
\- end_month         | Replaced by gbfs:calendar
\- end_day           | Replaced by gbfs:calendar
\- end_year          | Replaced by gbfs:calendar

### system_regions.json
> Replaced by vcard:region

### system_pricing_plans.json

> A class gbfs:Plan has been added to describe a pricing plan


Field Name        | Defines
------------------| ----------
plans             | Left out
\- plan_id         | gbfs:plan_id
\- url             | String - a fully qualified URL where the customer can learn more about this particular scheme
\- name            | Name of this pricing scheme
\- currency        | gbfs:currency
\- price           | gbfs:price
\- is_taxable      | gbfs:is_taxable
\- description     | rdfs:comment

### system_alerts.json
> A class gbfs:Plan has been added to describe an alert

Field Name        | Defines
----------------- | ----------
alerts            | Left out
\- alert_id        | gbfs:alert_id
\- type            | gbfs:alert_type - valid values are: <ul><li>gbfs:SYSTEM_CLOSURE</li> <li>gbfs:STATION_CLOSURE</li> <li>gbfs:STATION_MOVE</li> <li>gbfs:OTHER</li> </ul>
\- times           | Array of hashes with the keys "start" and "end" indicating when the alert is in effect (e.g. when the system or station is actually closed, or when it is scheduled to be moved). If this array is omitted then the alert should be displayed as long as it is in the feed.
&emsp;- start     | Integer POSIX timestamp - required if container "times" key is present
&emsp;- end       | Integer POSIX timestamp - if there is currently no end time planned for the alert, this key can be omitted indicating that there is no currently scheduled end time for the alert
\- station_ids     | Array of strings - If this is an alert that affects one or more stations, include their ids, otherwise omit this field. If both station_ids and region_ids are omitted, assume this alert affects the entire system
\- region_ids      | Array of strings - If this system has regions, and if this alert only affects certain regions, include their ids, otherwise, omit this field. If both station_ids and region_ids are omitted, assume this alert affects the entire system
\- url             | String - URL where the customer can learn more information about this alert, if there is one
\- summary         | String - A short summary of this alert to be displayed to the customer
\- description     | String - Detailed text description of the alert
\- last_updated    | Integer POSIX timestamp indicating the last time the info for the particular alert was updated


## Disclaimers

_Apple Pay, PayPass and other third-party product and service names are trademarks or registered trademarks of their respective owners._

## License

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/).
