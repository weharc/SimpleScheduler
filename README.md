# Simple Scheduler

This is a very simple Dynamics 365 Universal Resource Scheduling proof of concept that demonstrates an alternative to using the native Schedule Board. It is a work in progress and incomplete, but should guide the way for a seasoned D365 Developer.

## Web Resources
There are two web resources:
* tsp_bookings-calendar
* tsp_showavailability

## What do they do
Each of the web resources is fully self-contained HTML + JavaScript. They reference and load an external JavaScript based calendar component: [https://github.com/vkurko/calendar](Event Calendar). The web resources query the Dynamics 365 WebAPI making a couple of queries:
* Get me the list of Active Resources.
* Get me all the Bookable Resource Bookings for the current time forward.
* tsp_showavailability also queries the "Search Resource Availabilty API" and shows empty slows on the calendar.

Both of these web resources would be loaded in a new dialog or window. (They could be changed into a control and hosted as an iFrame in a form). They also reference jQuery which is optional. 

## tsp_showavailability
This also expects the id of a service activity in the querystring parameter data, e.g. /tsp_showavailability?data=some-guid. This can be made optional, but currently it requires a valid ID as it loads it into the top of the display. The idea is you would call this page if you were trying to make booking(s) for a specific service activity. 

The dropdown selector allows users to search for slots across the calendar of those pre-determined sizes. 

## Further work to be done
* Handling the click / selection of the slots and booking in the resource. Debug statements use console.log to show the selected items. Alternatively use drag and drop and let people book that way.
* Testing
* Add other filters to the top panel where the time range drop down select is showing - e.g. type of resource.

## Key Points
The main thing being demonstrated here is that it's possibly to call the Search Resource Availability API via JavaScript and deal with the results. It's also possible to call the API to select other information from the core URS tables - Resources, Characteristics, Categories etc. Combine this with JS to make the actual bookings and you have an alternate UI that can be tuned to the requirements.

Overall this might be better in a PCF Component in TypeScript, or even done in Canvas Pages - the challenge with this approach was trying to call the API in a complex manner.

## Tip
Use the XrmToolbox Dataverse REST Builder plugin to generate the query and jQuery code. 

Disclaimer
THIS CODE IS PROVIDED AS IS WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.
