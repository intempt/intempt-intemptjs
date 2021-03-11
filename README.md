# Intempt - JavaScript SDK

[Intempt](https://intempt.com/?utm_campaign=sdk&utm_medium=docs&utm_source=github) is an API-first platform for developers and marketers who are dissatisfied with high-maintenance personalizaton software. Our product is a personalization infrastructure through API and easy-to-use Console that provides a quicker way to build personalized applications. Unlike legacy personalization software we have:

* an API-first SaaS platform that enables personliazation of both digital and physical human activity
* a management console that helps cut down maintenance and reporting overhead
* an infrastructure to scale up user activity in no time

This is a library to facilitate tracking of anonymous and logeed in user traffic on your website.

You can find the full API documentation on [dev.intempt.com](https://dev.intempt.com).

## Contents:

* [1](https://github.com/intempt/intempt-intemptjs#install-and-initialize-script) - Installation and Initialization 
* [2](https://github.com/intempt/intempt-intemptjs#identifying-visitors) - How to identify a user
* [3](https://github.com/intempt/intempt-intemptjs#tracking-categories-and-products) - How to track products and category browsing
* [4](https://github.com/intempt/intempt-intemptjs#recording-custom-events) - How to record a custom event
* [5](https://github.com/intempt/intempt-intemptjs#tracking-revenue-with-trackcharge) - How to track revenue
* [6](https://github.com/intempt/intempt-intemptjs#events-collections-and-properties) - Events, Collections & Properties
* [7](https://github.com/intempt/intempt-intemptjs#tracker-events) - Event primer
* [8](https://github.com/intempt/intempt-intemptjs#event-properties) - Properties primer

## Install and Initialize Script

Add the following code to your site, in the `<head>` tag.

You can get an automatically generated version of this code, with your account specific variables filled in, from the sources page.

[Login](https://app.intempt.com) to Intempt and obtain your snippet from the [sources](https://app.intempt.com/sources) page:

```javascript
    <script src="https://cdn.intempt.com/intempt.min.js"></script>
```

Outside the `<head>` tag - you will need to add your configuration details:

```javascript
    intempt.configure("playground", "193528997887303680", "J_2HrlwS5tTVMJ3NkG7mT_L8INw4j1B6.8mC5KS-0BV8AtOBLJuewCDgo_NQa80c4x_ayyiHMRg2QLjX6Q8xf6-T0_ZJz5xVL")
```

The tracker object does not exist until initialization completes. Therefore, you should check its existence before running any custom tracking code.

## Identifying Visitors

Our tracking code automatically sets a unique ID for each visitor, and links multiple visits to the same visitor by setting a cookie in the browser.

To track visitors across multiple browsers and apps (or sessions after cookies are removed), pass in a unique identifying code (user email, unique user ID in your database etc.).

```javascript
	intempt.identifyUser("test@gmail.com")
```

### Retrieving Unique VisitorId

```javascript
    intempt.getVisitorId()
```

## Recording Custom Events

Our client-side API allows creation of any event type you might desire to be tracked for your page or application.

Custom collections allow you to bring custom data into your organization.

Intempt automatically tracks a number of on page events. You can log a custom event by calling track, passing in a set of key-value pairs.

```javascript
    intempt.CLIENT.recordEvent('COLLECTION_NAME', {
		key: value,
	});
```

The COLLECTION_NAME refers to an event type. For example, if you wanted to log every purchase made on your site, you might call that collection "purchase". Then, when a purchase happens, you call track and pass in the purchase details.

```javascript
	intempt.CLIENT.recordEvent("purchase", {
		 "items": [{"item name": "item 1","price": 20}, {"item name": "item 2","price": 15}]
		 "totalprice": 35,
		 "ispaid": true,
		 "timestamp": new Date().getTime(),
		 "fixed.name": "John Smith",
		 "fixed.age": 28,
		 "intempt.visit.trackcharge": 35
	})
```

## Events, Collections, and Properties

An event is a discrete interaction that occurs on your site. Events are organized by type into collections. Events have properties, key-value pairs that record relevant information about the event.

For example, a user clicks on a link:

1. The click is an event.

2. It belongs to the click collection.

3. The properties of the event include the time of the click, the id and other HTML attributes of the element that was clicked, the URL of the page on which the click happened, and so forth.

4. The tracker code, once installed on a website, will automatically record many events that occur on the site and subdomains.

## Tracker Events

Events as recorded by the tracker code are inserted as data items into the respective collection that it belongs to.

- click (Triggered on any interactive click)
	- visitorId (Created on the first visit for the user on the website)
	- eventId

- pageviews (Triggered on any page view or page change)
	- visitorId
	- eventId
	
- forum_submissions (Triggered on any forum submission)
	- visitorId
	- eventId

- profile (Triggered on identification of the user)
	- visitorId

Because of this hierarchy, any event can be filtered or accessed based on the properties associated with something further up the tree.

For example, if you wanted to find all button clicks associated with a particular visit, you can do that.

Custom events logged manually using the JavaScript API appear with whatever collection name was assigned, under the custom collection.

## Event Properties

Events have properties, key-value pairs the record information about the event.

Properties are grouped into two collections:

fixed — Properties that are (relatively) stable, related to the visit or the visitor. This includes things like operating system, browser, and geolocation.

timeseries — Properties that are specific to a particular interaction. This includes element-specific details, time stamps, and anything recorded as part of custom events.

When logging a custom event, you can pass in any existing property key names, as well as define your own.
