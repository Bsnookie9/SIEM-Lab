# Lab Instruction Changes

There are a few tweaks that were made to complete the lab. The video was posted in 2022 before Azure made changes to their   
UI, and finding certain things can be a little challenging. However, I can point you in the right direction.

## Enable gathering VM logs in Security Center
* Security Center is now named `Microsoft Defender for the Cloud`
* Pricing & Settings under the Management tab is now named `Environment Settings`

## Setup Azure Sentinel
* When using the search bar to search for "Sentinel"', it is now named `Microsoft Sentinel` under Services

## Getting Geolocation.io API Key
* You must change the API Key in the Powershell Script in order to get the location data for the Workbook later on

## Creating custom log in LAW to bring in our custom log
* Custom logs under the Settings tab is now named `Tables`
* When creating a new custom log, select `New custom log (MMA-based)`

## Create custom fields/extract fields from raw custom log data
* Due to the UI change, the `...` icon doesn't exist anymore. Still watch this part to gain understanding but we can fix this part later

## Setup map in sentinel with Latitude and Longitude (or country)
* Here is where you can enter the following script into the workbook to separate the different fields  
`FAILED_RDP_WITH_GEO_CL 
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by latitude, longitude, sourcehost, label, destination, country`

Everything else should be good to go when completing this SIEM Lab
