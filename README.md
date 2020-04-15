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

### Install script

Attach `voucherify.min.js` to your page, somewhere near `</body>`:

```html
<script type="text/javascript" src="/libs/voucherify/voucherify.min.js"></script>
```

You can also link it from [jsdelivr CDN](https://www.jsdelivr.com/projects/intempt.js):

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/rspective/intempt.js@latest/dist/intempt.min.js"></script>
```


### Initialize settings

[Log-in](https://app.voucherify.io/#/login) to Voucherify web interace and obtain your Client-side Keys from [Configuration](https://app.voucherify.io/#/app/configuration):

![](https://www.filepicker.io/api/file/uOLcUZuSwaJFgIOvBpJA)

Invoke `Voucherify.initialize(...)` when your application starts up:

```javascript
$(function () {
    Voucherify.initialize(
        "YOUR-CLIENT-APPLICATION-ID-FROM-SETTINGS",
        "YOUR-CLIENT-TOKEN-FROM-SETTINGS"
    );
});
```

As a third argument you can specify a timeout setting (in *milliseconds*):

```javascript
$(function () {
    Voucherify.initialize(
        "YOUR-CLIENT-APPLICATION-ID-FROM-SETTINGS",
        "YOUR-CLIENT-TOKEN-FROM-SETTINGS",
        2000
    );
});
```

We are tracking users which are validating vouchers with those who consume them by a `tracking_id`. For that we are setting up an identity for the user.
We will generate a `tracking_id` on the server side unless you specify it on your own. In both cases you will receive it in the validation response.

To provide your custom value use this simple function:

```javascript
$(function () {
    Voucherify.setIdentity("Your format of tracking_id e.g. Phone number or Email address.");
});
```





### Track custom events

Custom events are actions taken by your customers. Those events are best suited for tracking high-value interactions with your app. Logging a custom event can trigger any number of subsequent operations (e.g.: email distribution). It is enabled by default. There is no need for changing project configuration.

`Voucherify.track(eventName, metadata, customer, function callback (response) { })`

- `eventName` - required, an identifier of event
- `metadata` - required, an object containing data describing an event
- `customer` - optional, customer details, by default Voucherify takes profile declared with method Voucherify.setIdentity()
