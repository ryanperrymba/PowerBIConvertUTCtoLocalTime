# PowerBIConvertUTCtoLocalTime
Query Functions to convert times from UTC to Local Time

The purpose of this repositiory is to provide sample code for developers struggling with the different ways in which Power BI Desktop and Power BI handle time zone conversion.  

Power BI Desktop performs time zone conversion using the uses machine time settings.  At the time of publishing, the PBI service uses the timezone of the service, which is set to UTC, as is standard practice for web servers. Unfortunately, they do not provide any out of the box option to specify a desired time zone.  This causes the reported values to differ between the PBI Desktop and PBI service for all timezones other than UTC.  A specific example is sales figures for deals turned in during the final hours of a month in the western hemisphere.  On the desktop client, the numbers will appear accurate, but once loaded to PBI service, sales figures from the end of the month sales push will be reported as the following month, due to UTC being some 4-7 hrs ahead, depending on time zone. 

Daylight Savings Time (DST) further compounds this effect. While there are many examples found online, adjusting time fields by a static offset, they don't account for DST. 

This example code is not perfect, but it should provide a good framework for the student or developer working to improve the accuracy of their reports.  
It can adjust for DST based on published DST start and end dates in a support table.
It can adjust for Time zones based on U.S. states, but time zones don't correlate 1:1 with states. 
It cannot adjust to the local time zone of the viewing users machine, because it is run by the query engine, not the report rendering engine, and is only aware of the timezone of the viewing user's machine.  The query refresh happens on the server, so the datetime fields are adjusted before being presented to the report engine. 
