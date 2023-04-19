# Intempt - JavaScript SDK

[Intempt](https://intempt.com/?utm_campaign=sdk&utm_medium=docs&utm_source=github) is an API-first platform for developers and marketers who are dissatisfied with high-maintenance personalization software. Our product is a personalization infrastructure through API and easy-to-use Console that provides a quicker way to build personalized applications. Unlike legacy personalization software we have:

* an API-first SaaS platform that enables personalization of both digital and physical human activity
* a management console that helps cut down maintenance and reporting overhead
* an infrastructure to scale up user activity in no time

This is a library to facilitate tracking of anonymous and logged-in user traffic on your website.

## Contents:

* [1](https://github.com/intempt/intempt-intemptjs#installation-and-initialization) - Installation and Initialization 
* [2](https://github.com/intempt/intempt-intemptjs#identifying-visitors) - How to identify a user
* [3](https://github.com/intempt/intempt-intemptjs#retrieving-a-users-visitorid) - Retrieving A User's VisitorId
* [4](https://github.com/intempt/intempt-intemptjs#recording-custom-events) - Recording Custom Events
* [5](https://github.com/intempt/intempt-intemptjs#events-collections-and-properties) - Events, Collections & Properties
* [6](https://github.com/intempt/intempt-intemptjs#auto-tracking-events) - Auto-tracking Events
* [7](https://github.com/intempt/intempt-intemptjs#tracking-consents) - Recording Consents
* [8](https://github.com/intempt/intempt-intemptjs#opting-in-out-of-tracking) - Opting in/out of Tracking
* [9](https://github.com/intempt/intempt-intemptjs#data-subject-requests) - Opting in/out of Tracking

## Installation and Initialization

You can get an automatically generated version of this code, with your account specific variables filled in, from the sources page.

[Login](https://app.intempt.com) to Intempt and obtain your snippet from the [sources](https://app.intempt.com/sources) page:

Add the following code to your site, inside the `<head>` tag:

```javascript
    <script src="https://cdn.intempt.com/js/v2/intempt.min.js"></script>
```

Outside the `<head>` tag - you will need to add your configuration details:

```javascript
    intempt.configure("orgName", "sourceId", "apiKey")
```

## Identifying Visitors

Our tracking code automatically sets a unique ID for each visitor, and links multiple visits to the same visitor by setting a cookie in the browser.

To track visitors across multiple browsers and apps (or sessions after cookies are removed), pass in a unique identifying string (user email, unique user ID in your database etc.).

```javascript
	intempt.identifyUser("test@gmail.com")
```

### Retrieving A User's VisitorId

```javascript
    intempt.getVisitorId()
```

## Recording Custom Events

Our client-side API allows creation of any event type you might desire to be tracked for your page or application.

Custom collections allow you to bring custom data into your organization.

## Create Custom Collection
To start tracking custom events for our organization, after creating a [source](https://app.intempt.com/sources) you intend to use on your website, navigate to schema then use the schema Builder to create a collection with your personalized fields. Make sure to add a visitorId field and set a profile identifier as one of its properties. [See intempt docs for keys and identifiers](https://dev.intempt.com/#keys-and-identifiers) to find out why.

Make sure to also add an eventId to your schema. This depends on your use case. Adding an eventId fields tracks each event but without an eventId, existing data is replaced

Set up other custom field properties that match the data you plan to track.

Intempt automatically tracks a number of events. You can log a custom event by calling Intempt's recordEvent function, passing in a set of key-value pairs.


```javascript
    intempt.recordEvent('COLLECTION_NAME', {
		key: value,
	});
```

The COLLECTION_NAME refers to an event type. For example, if you wanted to log every purchase made on your site, you might call that collection "purchase". Then, when a purchase happens, you call track and pass in the purchase details.

### Example

```javascript
	intempt.recordEvent("purchase", {
		 "items": [{"item name": "item 1","price": 20}, {"item name": "item 2","price": 15}],
		 "totalprice": 35,
		 "ispaid": true,
		 "timestamp": new Date().getTime(),
		 "fixed.name": "John Smith",
		 "fixed.age": 28,
		 "intempt.visit.trackcharge": 35
	})
```

In the example above, we have a custom collection with name of `purchase`, then we have an object of key-value pairs. The Object passed into represent the fields we created while creating the collection. 

`NB`: Data type sent should match data type set when creating the collection. For instance, We are sending a field `timestamp` which has a Data type of `number`, Sending data with a type of `string` instead of `number` will make this custom collection not get tracked

```<script>
        const btn = document.querySelector("#regBtn")
        btn.addEventListener("click", () => {
        const first_name = document.querySelector('input[name="customer[first_name]"]').value;
        const last_name = document.querySelector('input[name="customer[last_name]"]').value;
        const email = document.querySelector('input[name="customer[email]"]').value;
        const discount_card_number = document.querySelector('input[name="customer[note][DiscountCardNumber]"]').value;
        intempt.recordEvent('signed_up', {
        first_name: first_name,
        last_name: last_name,
        email: email,
        discount_card_number: discount_card_number,
      });
        },false)
    </script>
  ```
The code snippet captures user sign-up data, such as their first name, last name, email, and discount card number. When the "regBtn" is clicked, the data is extracted from the input fields and passed as an object to Intempt's "recordEvent" function. The event name is "signed_up", and the data passed as an object includes the user's first name, last name, email, and discount card number.  

Event listeners:
Event listeners are used to detect user interaction with specific elements on the webpage, such as a button or a form input. In the code snippets, the "click" event listener is used to detect when the user clicks the "regBtn" or "loginBtn" button, respectively. When the event is detected, the function specified in the event listener is executed.

The script tags are used to define client-side JavaScript code, which can be used to add interactivity and functionality to web pages. In this case, the custom Intempt methods are defined within script tags to track user behavior on the website.

Query selectors are used to select specific elements on the webpage based on their HTML tag, class name, or ID. In the code snippets, query selectors are used to select the input fields containing the user's data, such as their first name, last name, and email.



## Events, Collections, and Properties

An event is any interaction that occurs on your site. Events are organized by collections and proper naming. Events have properties that are key-value pairs that record relevant information about the event.

Anyone can create a custom collection using Intempt's schema builder that is available on the console.

For example, a user clicks on a link:

1. The click is an event.

2. It belongs to the click collection.

3. The properties of the event include the time of the click, the id and other HTML attributes of the element that was clicked, the URL of the page on which the click happened, and so forth.

4. Later this data can be viewed on Intempt's console.

## Auto-tracking Events

Some events as recorded by default, and the data items are inserted into the respective collection that it belongs to.

These events are:

- Clicks (clicks) (Triggered on any interactive click)
  
- Page Views (pageviews) (Triggered once a user exits a page (therefore recording the time on the page))
  
- Form Submissions (form_submissions) (Triggered on any form submission)
  
- Profile (profile) (Triggered on identification of the user)

Custom events logged manually using the JavaScript API appear with whatever collection name was assigned.

## Tracking Consents

Save user consents and apply them to data flow. Make sure you have created consents purposes in your organization's settings



### Supported Regulation Types - GDPR & CCPA;

Consents are tracked using Intempt's exported function ;

```javascript
	intempt.trackConsents(consents)
```

`Intempt.trackConsents()` expects consents as an array of Objects inorder to be tracked successfully. 
Example: 

```Javascript
	intempt.trackConsents([
		{
         "regulation": "GDPR",
         "purpose": "advertising",
         "consented": true
        },
		{
         "regulation": "CCPA",
         "purpose": "advertising",
         "consented": false
        },
	])

```

Consents can contain as much as possible depending on your use case.

## Opting in and out of tracking

Every user can decide whether he/she can be tracked. To know the current tracking status of a user, you call our exported function `Intempt.has_opted_in_tracking()` to check if the user is opted into tracking and `Intempt.has_opted_out_tracking()` to check if the user opted out of tracking. 

`Intempt.has_opted_in_tracking()` returns true if the user is currently opted in to tracking and false if not.

`Intempt.has_opted_out_tracking()` obeys standard browser opt-out settings. By default, this will check standard browser opt out settings such as `Navigator.doNotTrack`. The method returns true if the user is currently opted out of tracking and false if not.

`Intempt.opt_in_tracking()` opts the user into data tracking resumes data tracking irrespective of the customer's browser settings. In this case, Setting `DonotTrack` in your browser settings is ignored because the user has enabled tracking. Data Tracking is enabled by setting a localStorage/cookies entry.

`Intempt.opt_out_tracking()` opts the user out of data tracking and pauses data tracking indefinitely until it is resumed at a later time. Data tracking is disabled by setting a localStorage/cookies entry.

`Intempt.clear_opt_in_out_tracking()` reverts all Intempt's tracking settings back to the browser's settings. This means that even if the user initially opted Into tracking, calling this exported function will revert this back to the default settings of the browser meaning that if `DonotTrack` is turned on in your settings, you are automatically optedOut of tracking and if it is turned on, you are optedIn to tracking by default.

## Data Subjects requests

Both the General Data Protection Regulation (GDPR) and the California Consumer Privacy Act (CCPA) define that consumers/data subjects have the right to view, update, extract and delete data that controllers & businesses have saved on them. When a consumer/data subject exercises their rights, they create a data subject request (DSR).

To create a data subject request, call 
### Creating a Data Subject Request Object

You need to discover supported options for creating data subject requests such as request type or the supported subject identities

To discover this options, call our exported function;

`Intempt.get_data_subject_request_supported_options()`

The function above returns a `Promise`.

The Object below is a response from our servers for supported options.

```JSON
	{
		"api_version":"2.0",
	    "supported_identities": {
			"identity_type":"email,
			 mobile_number",
			 "identity_format":"raw"
		},
		"supported_subject_request_types":[
			"portability",
			"access",
			"erasure"
		],
		"processor_certificate":
		"https://static.intempt.com/dsr/opendsr_cert.pem"
	}
```

After discovering supported options, we now move on to creating our DSR object.

````Javascript
	const DSRObject = {
		regulation: "GDPR",
        subject_request_type: "Access",
        subject_identities: [
			{
				identity_type: "mobile_number",
				identity_value: "+13022482744"
			}
		]
	}
````

After creating the object, we now create the data subject request using the method below. The exported function below returns a `Promise`. 

```Javascript
	Intempt.create_data_subject_request(DSRObject)
```

After creating a data subject request, you should see it created in your organization on the [console](https://app.intempt.com/settings/requests). 

