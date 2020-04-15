## Intempt - JavaScript SDK

[Intempt](https://intempt.com/?utm_campaign=sdk&utm_medium=docs&utm_source=github) is an API-first platform for developers and marketers who are dissatisfied with high-maintenance personalizaton software. Our product is a personalization infrastructure through API and easy-to-use Console that provides a quicker way to build personalized applications. Unlike legacy personalization software we have:

* an API-first SaaS platform that enables personliazation of both digital and physical human activity
* a management console that helps cut down maintenance and reporting overhead
* an infrastructure to scale up user activity in no time

This is a library to facilitate tracking of anonymous and logeed in user traffic on your website.

You can find the full API documentation on [dev.intempt.com](https://dev.intempt.com).

Contents:

* [1](https://github.com/intempt/intempt.js#initialize-settings) - Installation and client-side authentication

* [2](https://github.com/intempt/intempt.js#custom-event) - How to send a custom event [custom event](https://dev.intempt.com/reference/#custom-event)
* [3](https://github.com/intempt/intempt.js#identify) - How to identify a user [identify](https://dev.intempt.com/reference/#identify)
* [4](https://github.com/intempt/intempt.js#track-charge) - How to send charges [track charge](https://dev.intempt.com/reference#track-charge) track charge

### Usage

### Install and Initialize script

Add the following code to your site, preferably in the `<head>`.

You can get an automatically generated version of this code, with your account-specific variables filled in, from the sources setup page in the Intempt app.

[Log-in](https://app.intempt.com) to Intempt App and obtain your Client-side Keys from [Sources](https://app.intempt.com/sources):

```javascript
window.addEventListener("intempt.YOUR_TRACKER_NAME.ready", function() {
  //do something when tracker has been loaded;
  //the tracker object becomes accessible at window.intempt["site"] after loading;
});
!function(a,b){if(window.__intempt&&window.intempt)a&&(window.__intempt.init_tracker?window.__intempt.init_tracker(a):window.__intempt.startup_configs.push(a));else{window.__intempt={},window.__intempt.startup_configs=[],a&&window.__intempt.startup_configs.push(a);var c=document.createElement("script");c.type="text/javascript",c.async=!0,c.src=b||"https://cdn.intempt.com/intempt.min.js";var d=document.getElementsByTagName("script")[0];d.parentNode.insertBefore(c,d)}}({orgId:"YOUR_ORG_NAME",trackerId:"YOUR_TRACKER_NAME",token:"YOUR_TRACKER_TOKEN"});

```

Tracker Object
The tracker object is accessible with:
```javascript
window.intempt["TRACKER_NAME"]
```
The TRACKER_NAME string is the name as specified in the Intempt app.
```javascript
if (window.intempt && window.intempt['YOUR_TRACKER_NAME']) {
  // Perform your tracker operations here
}
```
The tracker object does not exist until initialization completes. Therefore you should check its existence before running any custom tracking code.


### Identifying visitors

```javascript
window.intempt["TRACKER_NAME"].identify({
    identifier: 'CUSTOM_IDENTIFIER'
})
```
Our tracking code automatically sets a unique ID for each visitor, and links multiple visits to the same visitor by setting a cookie in the browser.

To track visitors across multiple browsers and apps (or sessions after cookies are removed), pass in a unique identifying code (user email, unique user ID in your database etc.).

You can pass additional key-value pairs to identify, but identifier is the one that defines a unique identity. Other key-value pairs passed in can be used for data queries and segmenting in the Intempt app.

```javascript
window.intempt["TRACKER_NAME"].identify({
    identifier: 'CUSTOM_IDENTIFIER'
})
```
### Tracking Categories and Products


Visitor activity on the page can be scoped by product categories and individual products. This might come in handy when, for instance, you would like to understand differences between visitor activities for different categories or products pages, or when you simply want to know for notification purposes, which is the current one.

All you need to track categories and products is changing the tracked JS variables - our tracker will create the context and persist it automatically. You can either set both, or set one of them:

```javascript
window.intempt_category = 'my-category'; // sets the category for current page
window.intempt_product = 'my-product'; // sets the product for current page
```
To reset category and product, simply purge values from these variables (if your website is multi-page application, that is done automatically upon page transition):

```javascript
window.intempt_category = undefined; // sets the category for current page
window.intempt_product = undefined; // sets the product for current page
```
You can also use Object to track some additional properties both for categories and for products. In such case the requirement is that this object must contain field name with string in it, like this:
```javascript
window.intempt_category = {
    name: 'my-category', // required field, must contain string
    property1: 'some value 1',
    property2: 'some value 2'
};
```
```javascript
window.intempt_product = {
    name: 'my-product', // required field, must contain string
    property1: 'some value 1',
    property2: 'some value 2'
};
``` 

You also can create events for visitors actions, that cause changes to categories and products using Custom action type, and in subsequent menu picking category_changed or product_changed.





### Track custom events

Custom events are actions taken by your customers. Those events are best suited for tracking high-value interactions with your app. Logging a custom event can trigger any number of subsequent operations (e.g.: email distribution). It is enabled by default. There is no need for changing project configuration.

`Voucherify.track(eventName, metadata, customer, function callback (response) { })`

- `eventName` - required, an identifier of event
- `metadata` - required, an object containing data describing an event
- `customer` - optional, customer details, by default Voucherify takes profile declared with method Voucherify.setIdentity()

