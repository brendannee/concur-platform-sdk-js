Concur SDK for JavaScript
==============

JavaScript SDK for the [Concur Platform](http://developer.concur.com). For more information on the set of platform services, see the [Web services overview](https://developer.concur.com/get-started/webservices-overview) document on the developer portal.
Register for a [developer Sandbox here](https://developer.concur.com/register).

[![NPM](https://nodei.co/npm/concur-platform.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/concur-platform/)

## Installation

    npm install concur-platform

## Usage

All platform services are exposed via a root module which can be imported using the following.

    var concur = require('concur-platform');

##Table of Contents

###Platform Services

####Common

- [OAuth](#oauth)
    - [Native Flow](#native-flow)
    - [AppCenter Flow](#appcenter-flow)
- [ConnectionRequests](#connectionrequests)
    - [SEND](#post-connectionrequests)
    - [GET](#get-connectionrequests)
    - [PUT](#put-connectionrequests)
    - [DELETE](#delete-connectionrequests)
- [Locations](#locations)
    - [GET](#get-locations)
- [Suppliers](#suppliers)
    - [GET](#get-suppliers)
- [User](#user)
    - [SEND](#post-user)
    - [GET](#get-user)

####Expense

- [Allocations](#allocations)
    - [GET](#get-allocations)
- [Attendees](#attendees)
    - [SEND](#post-attendees)
    - [GET](#get-attendees)
    - [PUT](#put-attendees)
    - [DELETE](#delete-attendees)
- [AttendeeTypes](#attendeetypes)
    - [SEND](#post-attendeetypes)
    - [GET](#get-attendeetypes)
    - [PUT](#put-attendeetypes)
    - [DELETE](#delete-attendeetypes)
- [DigitalTaxInvoices](#digitaltaxinvoices)
    - [GET](#get-digitaltaxinvoices)
    - [PUT](#put-digitaltaxinvoices)
- [Entries](#entries)
    - [SEND](#post)
    - [GET](#get-entries)
    - [PUT](#put-entries)
    - [DELETE](#delete-entries)
- [ExchangeRates](#exchangerates)
    - [GET](#get-exchangerates)
- [ExpenseGroupConfigurations](#expensegroupconfigurations)
    - [GET](#get-expensegroupconfigurations)
- [Itemizations](#itemizations)
    - [SEND](#post-itemizations)
    - [GET](#get-itemizations)
- [ListItems](#listitems)
    - [SEND](#post-listitems)
    - [GET](#get-listitems)
    - [PUT](#put-listitems)
    - [DELETE](#delete-listitems)
- [Lists](#lists)
    - [SEND](#post-lists)
    - [GET](#get-lists)
    - [PUT](#put-lists)
- [Quick Expenses](#quick-expenses)
    - [SEND](#post-quick-expenses)
    - [GET](#get-quick-expenses)
    - [PUT](#put-quick-expenses)
    - [DELETE](#delete-quick-expenses)
- [Receipt](#receipt)
    - [SEND](#post-receipts)
    - [GET](#get-receipts)
    - [DELETE](#delete-receipts)
- [ReportDigests](#reportdigests)
    - [GET](#get-reportdigests)
- [Reports](#reports)
    - [SEND](#post-reports)
    - [GET](#get-reports)
    - [PUT](#put-reports)

####Insights

- [LatestBookings](#latestbookings)
    - [GET](#get-latestbookings)
- [Opportunities](#opportunities)
    - [GET](#get-opportunities)

####Invoice

- [PurchaseOrderReceipts](#purchaseorderreceipts)
    - [PUT](#put-purchaseorderreceipts)
- [PurchaseOrders](#purchaseorders)
    - [SEND](#post-purchaseorders)
    - [PUT](#put-purchaseorders)
    - [DELETE](#delete-purchaseorders)
- [SalesTaxValidationRequests](#salestaxvalidationrequests)
    - [GET](#get-salestaxvalidationrequests)
    - [PUT](#put-salestaxvalidationrequests)
    - [DELETE](#delete-salestaxvalidationrequests)
- [Vendors](#vendors)
    - [SEND](#post-vendors)
    - [GET](#get-vendors)
    - [PUT](#put-vendors)
    - [DELETE](#delete-vendors)

####Travel

- [Itinerary](#itinerary)
    - [SEND](#post-itinerary)
    - [GET](#get-itinerary)
- [TravelProfile](#travelprofile)
    - [GET](#get-travelprofile)

####Travel Request

- [Requests](#requests)
    - [GET](#get-requests)

####Other

- [Tests](#tests)
- [Promises](#promises)
- [License](#license)

## Platform Services

### OAuth

Enables the client to acquire an [OAuth token](https://developer.concur.com/oauth-20).

#####Native Flow

This is for the [native flow Oauth](https://developer.concur.com/oauth-20/native-flow). Use this
to get a token to test your application. This requires username, password and your registered consumerkey.

    var concur = require('concur-platform');

    var options = {
        username:username,
        password:password,
        consumerKey:consumerKey
    }

    concur.oauth.native(options)
    .then(function(token) {
        // token will contain the value, instanceUrl, refreshToken, and expiration details
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

#####AppCenter Flow

This is for the [AppCenter Flow](https://developer.concur.com/oauth-20/app-center-flow).
AppCenter Flow requires the code query parameter from Concur AppCenter, clientID (consumerKey) and clientSecret
for your registered partner application.

    var options = {
        code:code,
        client_id:client_id,
        client_secret:client_secret
    }

    concur.oauth.appCenter(options)
    .then(function(token) {
        // token will contain the value, instanceUrl, refreshToken, and expiration details
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

###Allocations

Used for getting a list of [Allocations](https://www.concursolutions.com/api/docs/index.html#!/Allocations) on an Expense Report.

#####GET Allocations

     //This will contain a list of Allocations
     var options = {
       oauthToken:oauthToken
     };

     concur.allocations.get(options)
     .then(function(data) {
       // Data will contain the Allocations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Allocation
     var options = {
       oauthToken:oauthToken
       id:AllocationsId
     };

     concur.allocations.get(options)
     .then(function(data) {
       // Data will contain the Allocation
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Attendees

Used for adding, getting, updating or deleting [Attendees](https://www.concursolutions.com/api/docs/index.html#!/Attendees) on a users or shared list.

#####POST Attendees

     var options = {
       oauthToken:oauthToken
     };

     concur.attendees.send(options)
     .then(function(data) {
       // Data will contain the Attendees
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Attendees

     //This will contain a list of Attendees
     var options = {
       oauthToken:oauthToken
     };

     concur.attendees.get(options)
     .then(function(data) {
       // Data will contain the Attendees
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Attendee
     var options = {
       oauthToken:oauthToken
       id:AttendeesId
     };

     concur.attendees.get(options)
     .then(function(data) {
       // Data will contain the Attendees
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT Attendees

     var options = {
       oauthToken:oauthToken,
       id:attendeesId
     };

     concur.attendees.put(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE Attendees

     var options = {
       oauthToken:oauthToken,
       id:attendeesId
     };

     concur.attendees.delete(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###AttendeeTypes

Used for adding, getting, updating or deleting [AttendeeTypes](https://www.concursolutions.com/api/docs/index.html#!/AttendeeTypes)
for a company. AttendeeTypes are used in the Attendees API to define the type of attendee you want to add.

#####POST AttendeeTypes

     var options = {
       oauthToken:oauthToken
     };

     concur.attendeeTypes.send(options)
     .then(function(data) {
       // Data will contain the AttendeeTypes
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET AttendeeTypes

     //This will contain a list of AttendeeTypes
     var options = {
       oauthToken:oauthToken
     };

     concur.attendeeTypes.get(options)
     .then(function(data) {
       // Data will contain the AttendeeTypes
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single AttendeeType
     var options = {
       oauthToken:oauthToken,
       id:AttendeeTypesId
     };

     concur.attendeeTypes.get(options)
     .then(function(data) {
       // Data will contain the AttendeeTypes
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT AttendeeTypes

     var options = {
       oauthToken:oauthToken,
       id:AttendeeTypesId
     };

     concur.attendeeTypes.put(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE AttendeeTypes

     var options = {
       oauthToken:oauthToken,
       id:AttendeeTypesId
     };

     concur.attendeeTypes.delete(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###ConnectionRequests

Used to interact with [ConnectionRequests](https://www.concursolutions.com/api/docs/index.html#!/ConnectionRequests) from
the Auto-Connect listing in Concur AppCenter. Given a supplier ID it will match all available ConnectionRequests.

#####POST ConnectionRequests

     var options = {
       oauthToken:oauthToken
     };

     concur.connectionRequests.send(options)
     .then(function(data) {
       // Data will contain the ConnectionRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET ConnectionRequests

     //This will contain a list of ConnectionRequests
     var options = {
       oauthToken:oauthToken
     };

     concur.connectionRequests.get(options)
     .then(function(data) {
       // Data will contain the ConnectionRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single ConnectionRequest
     var options = {
       oauthToken:oauthToken,
       id:ConnectionRequestsId
     };

     concur.connectionRequests.get(options)
     .then(function(data) {
       // Data will contain the ConnectionRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT ConnectionRequests

     var options = {
       oauthToken:oauthToken,
       id:connectionRequestId
     };

     concur.connectionRequests.put(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE ConnectionRequests

     var options = {
       oauthToken:oauthToken,
       id:connectionRequestId
     };

     concur.connectionRequests.delete(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###DigitalTaxInvoices

Returns all [Digital Tax Invoices](https://www.concursolutions.com/api/docs/index.html#!/DigitalTaxInvoices) that can be validated by the user based on the search criteria. Also given a digital tax invoice ID you can update them.

#####GET DigitalTaxInvoices

     //This will contain a list of DigitalTaxInvoices
     var options = {
       oauthToken:oauthToken
     };

     concur.digitalTaxInvoices.get(options)
     .then(function(data) {
       // Data will contain the DigitalTaxInvoices
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single DigitalTaxInvoice
     var options = {
       oauthToken:oauthToken,
       id:DigitalTaxInvoicesId
     };

     concur.digitalTaxInvoices.get(options)
     .then(function(data) {
       // Data will contain the DigitalTaxInvoices
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT DigitalTaxInvoices

     var options = {
       oauthToken:oauthToken,
       id:digitalTaxInvoiceID
     };

     concur.digitalTaxInvoices.put(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

### Entries

Used to work with [Entries](https://www.concursolutions.com/api/docs/index.html#!/Entries). which belong to an [Expense Report.](#get-reports)

#####POST

    //This will post an Expense Entry to a given ReportID
    var entry = {
        'Comment': 'Test Mileage Entry',
        'Description': 'Client Meeting',
        'ExchangeRate': '1.234',
        'ExpenseTypeCode': 'MILEG',
        'TransactionDate': '2014-10-27',
        'reportid': 'REPORTID'
    };

    var options = {
        oauthToken:oauthToken,
        contentType:'application/json',
        body:entry
    };

    concur.entries.send(options)
    .then(function(data){
        // In data will be the entry ID & URL to the entry
    })
    .fail(function (error) {
        // Error will contian the error returned by the server
    });

#####GET Entries

    //This will contain a list of expense entries
    var options = {
        oauthToken:oauthToken
    };

    concur.entries.get(options)
    .then(function(data) {
        //Data will contain a list of entries
    })
    .fail(function (error) {
        // Error will contian the error returned by the server
    });

    //This will contain a list of expense entries
    var options = {
        oauthToken:oauthToken,
        id:entriesId
    };

    concur.entries.get(options)
    .then(function(data) {
        //Data will contain an entry
    })
    .fail(function (error) {
        // Error will contain the error returned by the server
    });

#####PUT Entries

    //This will update the entry given by the entryId, and you can use any field support by entries from the link above.
    var entry = {
        'Comment': 'Test put',
    };

    var options = {
        oauthToken:oauthToken,
        contentType:'application/json',
        id:entryId,
    };

    concur.entries.put(options)
    .then(function(data){
        //Contains the response code 204, for a successful resource update
    })
    .fail(function (error) {
        // Error will contain the error returned by the server
    });

#####DELETE Entries

    //This will delete the entry given an ID.
    var options = {
        oauthToken:oauthToken,
        id:entryId
    };

    concur.entries.delete(options)
    .then(function(data) {
        //Contains the response code 204, for a successful resource update
    })
    .fail(function (error) {
        //Contains the error returned
    });

###ExchangeRates

Retrieve [Exchange Rate](https://www.concursolutions.com/api/docs/index.html#!/ExchangeRates) between two currencies on a given date.

#####GET ExchangeRates

     //This will contain a list of ExchangeRates
     var options = {
       oauthToken:oauthToken
     };

     concur.exchangeRates.get(options)
     .then(function(data) {
       // Data will contain the ExchangeRates
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###ExpenseGroupConfigurations

Get an [Expense Group Configurations](https://www.concursolutions.com/api/docs/index.html#!/ExpenseGroupConfigurations) owned by the user based on the search criteria.

#####GET ExpenseGroupConfigurations

     //This will contain a list of ExpenseGroupConfigurations
     var options = {
       oauthToken:oauthToken
     };

     concur.expenseGroupConfigurations.get(options)
     .then(function(data) {
       // Data will contain the ExpenseGroupConfigurations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single ExpenseGroupConfiguration
     var options = {
       oauthToken:oauthToken
       id:ExpenseGroupConfigurationsId
     };

     concur.expenseGroupConfigurations.get(options)
     .then(function(data) {
       // Data will contain the ExpenseGroupConfiguration
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Itemizations

Returns all expense [Itemizations](https://www.concursolutions.com/api/docs/index.html#!/Itemizations) owned by the user. Also allows you to add new itemizations to an existing [report](#get-reports).

#####POST Itemizations

     var options = {
       oauthToken:oauthToken
     };

     concur.itemizations.send(options)
     .then(function(data) {
       // Data will contain the Itemizations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Itemizations

     //This will contain a list of Itemizations
     var options = {
       oauthToken:oauthToken
     };

     concur.itemizations.get(options)
     .then(function(data) {
       // Data will contain the Itemizations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Itemization
     var options = {
       oauthToken:oauthToken
       id:ItemizationsId
     };

     concur.itemizations.get(options)
     .then(function(data) {
       // Data will contain the Itemizations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Itinerary

The [Itineraries](https://developer.concur.com/itinerary-tmc-and-third-party-developers/itinerary-resource) in Concur Travel, also referred to as Trips. Can contain multiple bookings.
[Itineraries](https://developer.concur.com/itinerary-tmc-and-third-party-developers/itinerary-resource) will allow you to post new trips or get existing trips for a user.

#####POST Itinerary

     var options = {
       oauthToken:oauthToken
     };

     concur.itinerary.send(options)
     .then(function(data) {
       // Data will contain the Itinerary
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Itinerary

     //This will contain a list of Itineraries
     var options = {
       oauthToken:oauthToken
     };

     concur.itinerary.get(options)
     .then(function(data) {
       // Data will contain the Itinerary
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Itinerary
     var options = {
       oauthToken:oauthToken
       id:ItineraryId
     };

     concur.itinerary.get(options)
     .then(function(data) {
       // Data will contain the Itinerary
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###LatestBookings

Get the [Latest booking](https://www.concursolutions.com/api/docs/index.html#!/LatestBookings) for hotel and air booking for a particular user.

#####GET LatestBookings

     //This will contain a list of LatestBookings
     var options = {
       oauthToken:oauthToken
     };

     concur.latestBookings.get(options)
     .then(function(data) {
       // Data will contain the LatestBookings
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Lists

Returns the [Lists](https://www.concursolutions.com/api/docs/index.html#!/Lists) available to the oauth token used. Also allows you to add and updating existing lists. Lists are a grouping of related items.
For example a School has departments and those could be a list, and the courses under departments are the list items.

#####POST Lists

     var options = {
       oauthToken:oauthToken
     };

     concur.lists.send(options)
     .then(function(data) {
       // Data will contain the Lists
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Lists

     //This will contain a list of Lists
     var options = {
       oauthToken:oauthToken
     };

     concur.lists.get(options)
     .then(function(data) {
       // Data will contain the Lists
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single List
     var options = {
       oauthToken:oauthToken
       id:ListsId
     };

     concur.lists.get(options)
     .then(function(data) {
       // Data will contain the Lists
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT Lists

     var options = {
       oauthToken:oauthToken,
       id:listID
     };

     concur.lists.put(options)
     .then(function(data) {
       // Data will contain the Lists
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


###ListItems

Returns all the [ListItems](https://www.concursolutions.com/api/docs/index.html#!/ListItems) for a given list. Also allows you to add, update and delete existing list items.

#####POST ListItems

     var options = {
       oauthToken:oauthToken
     };

     concur.listItems.send(options)
     .then(function(data) {
       // Data will contain the ListItems
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET ListItems

     //This will contain a list of ListItems
     var options = {
       oauthToken:oauthToken
     };

     concur.listItems.get(options)
     .then(function(data) {
       // Data will contain the ListItems
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single ListItem
     var options = {
       oauthToken:oauthToken
       id:ListItemsId
     };

     concur.listItems.get(options)
     .then(function(data) {
       // Data will contain the ListItems
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT ListItems

     var options = {
       oauthToken:oauthToken,
       id:listItemId
     };

     concur.listItems.put(options)
     .then(function(data) {
       // Data will contain the ListItems
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE ListItems

     var options = {
       oauthToken:oauthToken,
       id:listItemId
     };

     concur.listItems.delete(options)
     .then(function(data) {
       // Data will contain the ListItems
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Locations

Return details based on the search criteria for all [Locations](https://www.concursolutions.com/api/docs/index.html#!/Locations) for a company.

#####GET Locations

     //This will contain a list of Locations
     var options = {
       oauthToken:oauthToken
     };

     concur.locations.get(options)
     .then(function(data) {
       // Data will contain the Locations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Location
     var options = {
       oauthToken:oauthToken
       id:LocationsId
     };

     concur.locations.get(options)
     .then(function(data) {
       // Data will contain the Locations
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Opportunities

This is for the Insight [Opportunities API](https://www.concursolutions.com/api/docs/index.html#!/Opportunities)

#####GET Opportunities

     //This will contain a list of Opportunities
     var options = {
       oauthToken:oauthToken
     };

     concur.opportunities.get(options)
     .then(function(data) {
       // Data will contain the Opportunities
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###PurchaseOrderReceipts

Updates [Purchase Order](https://www.concursolutions.com/api/docs/index.html#!/PurchaseOrderReceipts) line item with receipt information and returns status of updation.

#####PUT PurchaseOrderReceipts

     var options = {
       oauthToken:oauthToken
     };

     concur.purchaseOrderReceipts.put(options)
     .then(function(data) {
       // Data will contain the PurchaseOrderReceipts
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###PurchaseOrders

Gets an existing [PurchaseOrder](https://www.concursolutions.com/api/docs/index.html#!/PurchaseOrders). You can also create and update an existing purchase order and returns the status of the request.

#####POST PurchaseOrders

     var options = {
       oauthToken:oauthToken
     };

     concur.purchaseOrders.send(options)
     .then(function(data) {
       // Data will contain the PurchaseOrders
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT PurchaseOrders

     var options = {
       oauthToken:oauthToken
     };

     concur.purchaseOrders.put(options)
     .then(function(data) {
       // Data will contain the PurchaseOrders
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE PurchaseOrders

     var options = {
       oauthToken:oauthToken
     };

     concur.purchaseOrders.delete(options)
     .then(function(data) {
       // Data will contain the PurchaseOrders
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

### Quick Expenses

Returns all  [quick expense](https://www.concursolutions.com/api/docs/index.html#!/QuickExpenses)  owned by the user. Allows you to create, update and delete existing quick expenses for the user.

##### POST Quick Expenses

    var quickexpenseJSON = {
        "Comment": "I am a Quick Expense",
        "CurrencyCode": "USD",
        "ExpenseTypeCode": "CARMI",
        "LocationCity": "Seattle",
        "LocationCountry": "US",
        "LocationSubdivision": "US-WA",
        "TransactionAmount": "12.23",
        "TransactionDate": "2015-05-10",
        "VendorDescription": "Testing"
    };

    var options = {
        oauthToken:oauthToken,
        contentType:'application/json',
        body:quickexpenseJSON
    };

    concur.quickexpenses.send(options)
    .then(function(data){
        //Contains the ID and URI to the resource
    })
    .fail(function (error) {
        //Error contains the error returned
    });

##### GET Quick Expenses

    //Get a list of quick expenses
    var options = {
        oauthToken:oauthToken
    };

    concur.quickexpenses.get(options)
    .then(function(data) {
        //Data contains a list of quick expenses
    })
    .fail(function (error) {
        //Error contians the error returned
    });

    //Get a single quick expense, just add quickexpenseId to options
    var options = {
        oauthToken:oauthToken,
        id:quickexpenseId
    };

    concur.quickexpenses.get(options)
    .then(function(data) {
        //Contains the single quick expense
    })
    .fail(function (error) {
        //Contains the error returned
    });

##### PUT Quick Expenses

    var quickexpenseJSON = {
        "TransactionAmount": "16.23"
    };

    var options = {
        oauthToken:oauthToken,
        contentType:'application/json',
        id:quickexpenseId,
        body:quickexpenseJSON
    };

    concur.quickexpenses.put(options)
    .then(function(data){
        //Contains the response code 204, for a successful resource update
    })
    .fail(function (error) {
        //Contains the error returned
    });

##### DELETE Quick Expenses

    var options = {
        oauthToken:oauthToken,
        id:quickexpenseId
    };

    concur.quickexpenses.delete(options)
    .then(function(data) {
        //Contains the response code 204, for a successful resource update
    })
    .fail(function (error) {
        //Contains the error returned
    });

### Receipt

Enables the client to interact with the [receipt](https://www.concursolutions.com/api/docs/index.html#!/ReceiptImages) and
[eReceipt](https://developer.concur.com/api-documentation/more-resources/draft-documentation/e-receipt-service) Web services. Using this in the
SDK will also allow you to add receipts to any resource in Concur that allows receipts. For example entries and reports.

#####POST Receipts

    var concur = require('concur-platform');

    //If you have the image locally, this will post it to Concur.
    var options = {
        oauthToken:oauthToken,
        image:image, //base 64 encoded
        contentType:'image/png'
    }

    // Sending a receipt
    concur.receipt.send(options)
    .then(function(receiptID) {
        //receiptID is returned on success
    })
    .fail(function(error) {
        // error will contain the error message returned
    });


    //If you have a link to the image, using this will get the image, then post it to Concur.
    options = {
        oauthToken:oauthToken,
        imageURL:'http://upload.wikimedia.org/wikipedia/commons/2/22/Turkish_Van_Cat.jpg'
    };

    concur.receipt.send(options)
    .then(function(imageId) {
        //receiptID is returned on success
    })
    .fail(function(error) {
        //error will contain the error message returned
    });

    //If you have an [Expense Entry ID](#get-entries) this will add the image to the Entry.
    options = {
        oauthToken:oauthToken,
        entryId:entryId,
        image:image //base64 encoded image
    };

    concur.receipt.send(options)
    .then(function(imageId) {
        //receiptID is returned on success
    })
    .fail(function(error) {
        //error will contain the error message returned
    });

    //If you have an [Expense Report ID](#get-reports) this will add the image to the Report.
    options = {
        oauthToken:oauthToken,
        reportId:reportId,
        image:image //base64 encoded image
    };

    concur.receipt.send(options)
    .then(function(imageId) {
        //receiptID is returned on success
    })
    .fail(function(error) {
        //error will contain the error message returned
    });

#####GET Receipts

    // Getting a lit of receipts
    var options = {
        oauthToken:oauthToken
    }

    concur.receipt.get(options)
    .then(function(data) {
        //data will contain a list of receipts
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

    //Get a receipt image URL by image ID.
    var options = {
        oauthToken:oauthToken,
        id:receiptId
    }

    concur.receipt.get(options)
    .then(function(data) {
        //data will contain the receipt image url
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

#####DELETE Receipts

    // Deleting a receipt
    var options = {
        oauthToken:oauthToken,
        id:receiptId
    }

    concur.receipt.delete(options)
    .then(function(data.statusCode) {
        // data.statusCode will be equal to 204, the receipt was deleted
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

###ReportDigests

Returns all [ReportDigests](https://www.concursolutions.com/api/docs/index.html#!/ReportDigests) owned by the user based on the search criteria.

#####GET ReportDigests

     //This will contain a list of ReportDigests
     var options = {
       oauthToken:oauthToken
     };

     concur.reportDigests.get(options)
     .then(function(data) {
       // Data will contain the ReportDigests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Report
     var options = {
       oauthToken:oauthToken
       id:ReportDigestsId
     };

     concur.reportDigests.get(options)
     .then(function(data) {
       // Data will contain the Report
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Reports

This is for Expense [Reports](https://www.concursolutions.com/api/docs/index.html#!/Reports). Allows you to add or update report fields such as Name, comment, custom fields, org unit and policy.

#####POST Reports

     var options = {
       oauthToken:oauthToken
     };

     concur.reports.send(options)
     .then(function(data) {
       // Data will contain the Reports
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Reports

     //This will contain a list of Reports
     var options = {
       oauthToken:oauthToken
     };

     concur.reports.get(options)
     .then(function(data) {
       // Data will contain the Reports
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Report
     var options = {
       oauthToken:oauthToken
       id:ReportsId
     };

     concur.reports.get(options)
     .then(function(data) {
       // Data will contain the Report
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT Reports

     var options = {
       oauthToken:oauthToken,
       id:reportID
     };

     concur.reports.put(options)
     .then(function(data) {
       // Data will contain the 204 response
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Requests

This is for the [Travel Requests API](https://www.concursolutions.com/api/docs/index.html#!/Requests)


#####GET Requests

     //This will contain a list of Requests
     var options = {
       oauthToken:oauthToken
     };

     concur.requests.get(options)
     .then(function(data) {
       // Data will contain the Requests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Request
     var options = {
       oauthToken:oauthToken
       id:RequestsId
     };

     concur.requests.get(options)
     .then(function(data) {
       // Data will contain the Requests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###SalesTaxValidationRequests

Retrieves invoices for calculating tax, filtered based on input params. [SalesTaxValidationRequests API](https://www.concursolutions.com/api/docs/index.html#!/SalesTaxValidationRequests)

#####GET SalesTaxValidationRequests

     //This will contain a list of SalesTaxValidationRequests
     var options = {
       oauthToken:oauthToken
     };

     concur.salesTaxValidationRequests.get(options)
     .then(function(data) {
       // Data will contain the SalesTaxValidationRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single SalesTaxValidationRequest
     var options = {
       oauthToken:oauthToken
       id:SalesTaxValidationRequestsId
     };

     concur.salesTaxValidationRequests.get(options)
     .then(function(data) {
       // Data will contain the SalesTaxValidationRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT SalesTaxValidationRequests

     var options = {
       oauthToken:oauthToken
     };

     concur.salesTaxValidationRequests.put(options)
     .then(function(data) {
       // Data will contain the SalesTaxValidationRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE SalesTaxValidationRequests

     var options = {
       oauthToken:oauthToken
     };

     concur.salesTaxValidationRequests.delete(options)
     .then(function(data) {
       // Data will contain the SalesTaxValidationRequests
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###Suppliers

Returns all [Suppliers API](https://www.concursolutions.com/api/docs/index.html#!/Suppliers) based on the search criteria.

#####GET Suppliers

     //This will contain a list of Suppliers
     var options = {
       oauthToken:oauthToken
     };

     concur.suppliers.get(options)
     .then(function(data) {
       // Data will contain the Suppliers
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Supplier
     var options = {
       oauthToken:oauthToken
       id:SuppliersId
     };

     concur.suppliers.get(options)
     .then(function(data) {
       // Data will contain the Suppliers
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###TravelProfile

This is for the Concur [TravelProfile.](https://developer.concur.com/travel-profile/travel-profile-resource/travel-profile-resource-get). Which includes traveler preferences.

#####GET TravelProfile

     //This will contain a single TravelProfile
     var options = {
       oauthToken:oauthToken
       id:TravelProfileId
     };

     concur.travelProfile.get(options)
     .then(function(data) {
       // Data will contain the TravelProfile
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###User

This is for the Concur [User](https://developer.concur.com/api-documentation/web-services/user) Profile. Which includes what Concur products the user has, and what groups the user is associated with inside their company.

#####POST User

     var options = {
       oauthToken:oauthToken
     };

     concur.user.send(options)
     .then(function(data) {
       // Data will contain the User
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

###GET User

    var options = {
        oauthToken:oauthToken,
        loginId:loginId
    }

    concur.user.get(options)
    .then(function(user) {
        // user will contain user data
    })
    .fail(function(error) {
        // error will contain the error message returned
    });

###Vendors

Gets an existing [Vendors.](https://www.concursolutions.com/api/docs/index.html#!/Vendors) Allows you to create, update and deleting existing vendors avilable to the oauth token. 

#####POST Vendors

     var options = {
       oauthToken:oauthToken
     };

     concur.vendors.send(options)
     .then(function(data) {
       // Data will contain the Vendors
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####GET Vendors

     //This will contain a list of Vendors
     var options = {
       oauthToken:oauthToken
     };

     concur.vendors.get(options)
     .then(function(data) {
       // Data will contain the Vendors
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });


     //This will contain a single Vendor
     var options = {
       oauthToken:oauthToken
       id:VendorsId
     };

     concur.vendors.get(options)
     .then(function(data) {
       // Data will contain the Vendors
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####PUT Vendors

     var options = {
       oauthToken:oauthToken
     };

     concur.vendors.put(options)
     .then(function(data) {
       // Data will contain the Vendors
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

#####DELETE Vendors

     var options = {
       oauthToken:oauthToken
     };

     concur.vendors.delete(options)
     .then(function(data) {
       // Data will contain the Vendors
     })
     .fail(function(error) {
       // Error will contain the error returned.
     });

## Tests

To run the client SDK tests, create a default.json file in the config folder which contains the credentials of the Concur account to test with. Template.json can be used as a template. Then, run the following:

    npm test

The test will upload the concur logo to the expense receipt store associated with the OAuth token. It will also upload an E-Receipt to the associated user account. 

## Promises
In order to simplify the asynchronous nature of the platform Web service calls, the client SDK has made use of the Q promises library. More information can be found on the [project's GitHub site](https://github.com/kriskowal/q).

## License

Copyright 2014 [Concur](http://www.concur.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.