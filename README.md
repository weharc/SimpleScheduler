# Simple Scheduler

This is a very simple Dynamics 365 Universal Resource Scheduling proof of concept that demonstrates an alternative to using the native Schedule Board UI. It is a work in progress and incomplete, but should guide the way for a seasoned D365 Developer. Rather than reinvent the wheel, the [Search Resource Availability API](https://learn.microsoft.com/en-us/dynamics365/customer-service/develop/universal-resource-scheduling) is called in one of the demonstrations. It's documentation is a bit hard to follow, hopefully the examples here make it a bit more accessible. 

## Web Resources
There are two web resources in this demonstration:
* [tsp_bookings-calendar](src/tsp_bookings-calendar.html)
* [tsp_showavailability](src/tsp_showavailability.html)

## What do they do
Each of the web resources is fully self-contained HTML + JavaScript file. They reference and load an external JavaScript based calendar component: [Event Calendar](https://github.com/vkurko/calendar). The web resources query the Dynamics 365 WebAPI making a couple of queries:
* Get me the list of Active Resources.
* Get me all the Bookable Resource Bookings for the current time forward.
* tsp_showavailability also queries the "Search Resource Availabilty API" and shows empty slots on the calendar.

Both of these web resources would be loaded in a new dialog or window for a user. (They could be changed into a control and hosted as an iFrame in a form). They also reference jQuery which is optional. So the idea is maybe replace the native 'Book' button on the Service Activity form with a similar button that invokes one of these web resources instead. 

## tsp_showavailability
This also expects the id of a service activity in the querystring parameter data, e.g. /tsp_showavailability?data=some-guid. Thisis optional, but if you passed that ID you could refine the search for availability by looking up the Service data. The idea is you would call this page if you were trying to make booking(s) for a specific service activity. 

The dropdown selector at the top allows users to search for slots across the calendar of those pre-determined durations. 

## Further work to be done
* Handling the click / selection of the slots and booking in the resource. Debug statements use console.log to show the selected items. Alternatively use drag and drop and let people book that way.
* Add other filters to the top panel where the time range drop down select is showing - e.g. type of resource. 
** The API allows resources to be passed as constraints, so if you just wanted to book in Mary a user could select Mary and you call the API
* Testing

## Key Points
The main thing being demonstrated here is that it's possible to call the [Search Resource Availability API](https://learn.microsoft.com/en-us/dynamics365/customer-service/develop/universal-resource-scheduling) via JavaScript and deal with the results. It's also possible to call the WebAPI to select other information from the core URS tables - Resources, Characteristics, Categories etc. Combine this with JS to make the actual bookings and you have an alternate UI that can be tuned to the requirements.

Overall this might be better hosted in a PCF Component in TypeScript, or even done in Canvas Pages - the challenge with this approach was trying to call the API in a complex manner.

## Tip
Use the [XrmToolbox](https://www.xrmtoolbox.com/) Dataverse REST Builder plugin to generate the query and jQuery code. 


# Disclaimer
THIS CODE IS PROVIDED AS IS WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.
