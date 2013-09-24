---
layout: default
title: Spreadly Doku - PuSH API
---

This API is based on the PubSubHubbub Spec.

# verify callback-url

In order to prevent an attacker from creating unwanted subscriptions Spread.ly must ensure that the subscriber did indeed want the subscription request.

Spread.ly verifies a subscription request by sending an HTTP GET request to the subscriber's callback URL (set through the admin interface). This request has the following query string arguments appended:

<table>
  <tr>
    <th>key</th>
    <th>value</th>
  </tr>
  <tr>
    <td>hub.mode</td>
    <td>subscribe</td>
  </tr>
  <tr>
    <td>hub.topic</td>
    <td>the domain/host you try to subscribe to (the url you claimed in the Spread.ly stats)</td>
  </tr>
  <tr>
    <td>hub.challenge</td>
    <td>A generated, random string that must be echoed by the subscriber to verify the subscription.</td>
  </tr>
</table>

To accept the subscription, you have to confirm that the hub.topic correspond to a pending subscription. If so, the callback url have to respond with an HTTP success (2xx) code with a response body equal to the hub.challenge parameter. If you do not agree with the action, the callback url respond with a 404 "Not Found" response.

In the PubSubHubbub spec: http://pubsubhubbub.googlecode.com/svn/trunk/pubsubhubbub-core-0.3.html#verifysub

# receive requests

If the callback url is verified, Spread.ly will send an HTTP POST request to this url every time a user likes one of your pages.

In the PubSubHubbub spec: http://pubsubhubbub.googlecode.com/svn/trunk/pubsubhubbub-core-0.3.html#contentdistribution

# data format

The post has the Content-Type `application/json` and represents a single like.

The fields:

## global

<table>
  <tr>
    <td>verb</td>
    <td>the type of the action (currently we only support "like")</td>
  </tr>
  <tr>
    <td>published</td>
    <td>the time, the like happend</td>
  </tr>
</table>

## object

The object represents the like

<table>
  <tr>
    <td>id</td>
    <td>the uniqe id of the "like"</td>
  </tr>
  <tr>
    <td>objectType</td>
    <td>the type of the liked object (currently we only support "website")</td>
  </tr>
  <tr>
    <td>url</td>
    <td>the url of the liked website</td>
  </tr>
</table>

## target

The claimed domained (see http://spreadly.com/domain_profiles/index).

<table>
  <tr>
    <td>id</td>
    <td>the uniqe id of the claimed domain</td>
  </tr>
  <tr>
    <td>objectType</td>
    <td>always "service"</td>
  </tr>
  <tr>
    <td>url</td>
    <td>the url of the claimed</td>
  </tr>
  <tr>
    <td>host</td>
    <td>the host of the claimed</td>
  </tr>  
</table>

## JSON example

{% highlight json %}
{
   "generator":{
      "url":"http://spreadly.com/"
   },
   "object":{
      "id":"tag:spreadly.com,2011:/activity/4dca4dc4db45111c52000000",
      "objectType":"website",
      "url":"http://notizblog.org/about/"
   },
   "published":"2011-05-11T10:50:12+02:00",
   "target":{
      "host":"notizblog.org",
      "id":"tag:spreadly.com,2010:/domain/23",
      "objectType":"service",
      "url":"http://notizblog.org"
   },
   "verb":"like"
}
{% endhighlight %}

see: http://activitystrea.ms/head/json-activity.html

# Simple _callback url_ implementations

## PHP Example

In PHP, dots and spaces in query parameter names are converted to underscores automatically. So you need to check "hub_mode" instead of "hub.mode". 

{% highlight php %}
<?php
$method = $_SERVER['REQUEST_METHOD'];  

// verify callback-url
if ($method == 'GET' &&
    // check correct hub mode
    $_GET['hub_mode'] == 'subscribe' &&
    // hub.challenge is required
    isset($_GET['hub_challenge']) &&
    // check hub topic to match the url you want to subscribe to
    // this prevents you for spam!
    $_GET['hub_topic'] == "http://example.com") {
  echo $_GET['hub_challenge'];
} else  if ($method == 'POST') { // receive requests
  // get post
  $updates = json_decode(file_get_contents("php://input"), true); 

  // do something ninja like with $updates
} else {
  error_log(print_r(file_get_contents("php://input"), true) . "\n", 3, dirname(__FILE__)."/error.log");
}
?>
{% endhighlight %}