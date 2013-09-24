---
layout: default
title: Spreadly Doku - Deal API
---

**NOTE: To use the Deal-API you need an Access-Key! You can request yours here: http://spreadly.com/advertiser/dealapi**

# API endpoint

<table>
  <tr>
    <td>endpoint</td>
    <td>http://api.spreadly.com/deals</td>
  </tr>
  <tr>
    <td>method</td>
    <td>POST</td>
  </tr>
</table>

# authentication

To access the Spread.ly API you have to add the Access-Key (request yours here: http://spreadly.com/advertiser/dealapi) like this:


{% highlight html %}
http://api.spreadly.com/deals?access_token=#your_access_key#
{% endhighlight %}

# data format

A `POST` has the Content-Type `application/json` and represents a single deal.

## JSON example (coupon type: code)

{% highlight json %}
{
     "name": "Test-Kampagne",

     "motivation": {
      "title": "20 € für Ihren Like!",
      "text": "Ihr Like ist uns Geld wert. Sie erhalten für Ihren Like einen 20 Euro Amazon Gutschein! Like klicken und danach sofort Gutschein herunterladen."
     },

     "spread": {
      "title": "DozentenScout: Marktplatz für Weiterbildung",
      "text": "Seminare und Trainer finden, Jobs ausschreiben, Fachartikel aus der Weiterbildungsbranche lesen.",
      "url": "http://example.com/",
      "img": "http://example.com/spread.jpg",
      "tos": "http://example.com/tos"
     },

     "coupon": {
      "type": "code",
      "title": "Amazon Gutschein von Spreadly",
      "text": "Klicken Sie diesen Link um sich Ihren Amazon Gutschein herunter zu laden. Sie können diesen Gutschein uneingeschränkt nutzen und auch an Dritte weitergeben.",
      "code": "DEMO",
      "redeem_url": "http://example.com/redeem"
     },

     "billing": {
      "type": "like",
      "target_quantity": 10.0
     }
}
{% endhighlight %}

The fields:

## global

<table>
  <tr>
    <td>name</td>
    <td>the name of your campain (only visible for the advertiser)</td>
    <td>varchar</td>
  </tr>
  <tr>
    <td>activate</td>
    <td>choose if your deal should automatically be activated (`true`) or run some tests and re-check the submitted deals through or admin interface (`false`) for some testing-experience for example</td>
    <td>boolean</td>
  </tr>
</table>

## motivation

<img src="http://spreadly.com/img/popup-deal.png" />

The motivation-part describes your deal and is used to motivate the user to participate

<table>
  <tr>
    <td>title<sup>(1)</sup></td>
    <td>a short popup title</td>
    <td>varchar(255)</td>
  </tr>
  <tr>
    <td>text<sup>(2)</sup></td>
    <td>a short motivation text</td>
    <td>varchar(500)</td>
  </tr>
</table>

## spread

With the spread, you can choose which informations will be shared by the user.

<table>
  <tr>
    <td>title<sup>(3)</sup></td>
    <td>the title of the share</td>
    <td>varchar(255)</td>
  </tr>
  <tr>
    <td>text<sup>(4)</sup></td>
    <td>the description of a share</td>
    <td>varchar(500)</td>
  </tr>
  <tr>
    <td>url<sup>(5)</sup></td>
    <td>the url of the share</td>
    <td>must be valid url</td>
  </tr>
  <tr>
    <td>img<sup>(6)</sup></td>
    <td>the path to an image</td>
    <td>must be valid url</td>
  </tr>
  <tr>
    <td>tos</td>
    <td>the link to your tos</td>
    <td>must be valid url</td>
  </tr>
</table>

## coupon

you can choose between three types of coupons.


The coupon **code**:

<img src="http://spreadly.com/img/coupon_type_code.png" />

<table>
  <tr>
    <td>type</td>
    <td>the type is *`coupon`*</td>
    <td></td>
  </tr>
  <tr>
    <td>title<sup>(1)</sup></td>
    <td>the title of your coupon</td>
    <td>varchar(255)</td>
  </tr>
  <tr>
    <td>text<sup>(2)</sup></td>
    <td>a short text that descripes your coupon</td>
    <td>varchar(500)</td>
  </tr>
  <tr>
    <td>code<sup>(3)</sup></td>
    <td>the code</td>
    <td>must be valid url</td>
  </tr>
  <tr>
    <td>redeem_url<sup>(5)</sup></td>
    <td>a link to a page where the user could redeem the coupon</td>
    <td>varchar(255)</td>
  </tr>
</table>

JSON example:

{% highlight json %}
[...]
"coupon": {
  "type": "code",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link ...",
  "code": "DEMO",
  "redeem_url": "http://example.com/redeem"
}
[...]
{% endhighlight %}


The **download** coupon:

<img src="http://spreadly.com/img/coupon_type_download.png" />

<table>
  <tr>
    <td>type</td>
    <td>the type is **`download`**</td>
    <td></td>
  </tr>
  <tr>
    <td>title<sup>(1)</sup></td>
    <td>the title of your coupon</td>
    <td>varchar(255)</td>
  </tr>
  <tr>
    <td>text<sup>(2)</sup></td>
    <td>a short text that descripes your coupon</td>
    <td>varchar(500)</td>
  </tr>
  <tr>
    <td>url<sup>(3)</sup></td>
    <td>the download-url</td>
    <td>must be valid url</td>
  </tr>
</table>

JSON example:

{% highlight json %}
[...]
"coupon": {
  "type": "download",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link ...",
  "url": "http://example.com/download"
}
[...]
{% endhighlight %}

The **url** coupon:

<img src="http://spreadly.com/img/coupon_type_url.png" />

<table>
  <tr>
    <td>type</td>
    <td>the type is `url`</td>
    <td></td>
  </tr>
  <tr>
    <td>title<sup>(1)</sup></td>
    <td>the title of your coupon</td>
    <td>varchar(255)</td>
  </tr>
  <tr>
    <td>text<sup>(2)</sup></td>
    <td>a short text that descripes your coupon</td>
    <td>varchar(500)</td>
  </tr>
  <tr>
    <td>url<sup>(3)</sup></td>
    <td>the url to your content</td>
    <td>must be valid url</td>
  </tr>
</table>

JSON example:

{% highlight json %}
[...]
"coupon": {
  "type": "url",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link...",
  "url": "http://example.com/visit"
}
[...]
{% endhighlight %}

## billing

<table>
  <tr>
    <td>type</td>
    <td>you can choose between the billing types `like` and `media_penetration`</td>
    <td>enum(like, media_penetration)</td>
  </tr>
  <tr>
    <td>target_quantity</td>
    <td>the number of likes or media-penetration you want to buy</td>
    <td>int</td>
  </tr>
</table>

To get some informations about the pricing, visit http://spreadly.local/advertiser/dealapi oder write an e-mail to marco@ekaabo.com