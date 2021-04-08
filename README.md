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

Intempt automatically tracks a number of events. You can log a custom event by calling Intempt's recordEvent function, passing in a set of key-value pairs.

```javascript
    intempt.CLIENT.recordEvent('COLLECTION_NAME', {
		key: value,
	});
```

The COLLECTION_NAME refers to an event type. For example, if you wanted to log every purchase made on your site, you might call that collection "purchase". Then, when a purchase happens, you call track and pass in the purchase details.

### Example

```javascript
	intempt.CLIENT.recordEvent("purchase", {
		 "items": [{"item name": "item 1","price": 20}, {"item name": "item 2","price": 15}],
		 "totalprice": 35,
		 "ispaid": true,
		 "timestamp": new Date().getTime(),
		 "fixed.name": "John Smith",
		 "fixed.age": 28,
		 "intempt.visit.trackcharge": 35
	})
```

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
