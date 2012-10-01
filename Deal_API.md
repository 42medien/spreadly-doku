|| *NOTE: To use the Deal-API you need an Access-Key! You can request yours here: http://spreadly.com/advertiser/dealapi * ||

# API endpoint

|| endpoint || http://api.spreadly.com/deals ||
|| method || POST ||

# authentication

To access the Spread.ly API you have to add the Access-Key (request yours here: http://spreadly.com/advertiser/dealapi) like this:


```
http://api.spreadly.com/deals?access_token=#your_access_key#
```

# data format

A `POST` has the Content-Type `application/json` and represents a single deal.

=== JSON example (coupon type: code) ===

```json
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
```

The fields:

## global

|| name || the name of your campain (only visible for the advertiser) || varchar ||
|| activate || choose if your deal should automatically be activated (`true`) or run some tests and re-check the submitted deals through or admin interface (`false`) for some testing-experience for example || boolean ||

## motivation

<img align="right" src="http://spreadly.com/img/popup-deal.png" />

The motivation-part describes your deal and is used to motivate the user to participate

|| title^(1)^ || a short popup title || varchar(255) ||
|| text^(2)^ || a short motivation text || varchar(500) ||

## spread

With the spread, you can choose which informations will be shared by the user.

|| title^(3)^ || the title of the share || varchar(255) ||
|| text^(4)^ || the description of a share || varchar(500) ||
|| url^(5)^ || the url of the share || must be valid url ||
|| img^(6)^ || the path to an image || must be valid url ||
|| tos || the link to your tos || must be valid url ||

## coupon

you can choose between three types of coupons.


The coupon _*code*_:

<img align="right" src="http://spreadly.com/img/coupon_type_code.png" />


|| type || the type is *`coupon`* ||  ||
|| title^(1)^ || the title of your coupon || varchar(255) ||
|| text^(2)^ || a short text that descripes your coupon || varchar(500) ||
|| code^(3)^ || the code || must be valid url ||
|| redeem_url^(5)^ || a link to a page where the user could redeem the coupon || varchar(255) ||

JSON example:

```json
[...]
"coupon": {
  "type": "code",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link ...",
  "code": "DEMO",
  "redeem_url": "http://example.com/redeem"
}
[...]
```


The _*download*_ coupon:

<img align="right" src="http://spreadly.com/img/coupon_type_download.png" />

|| type || the type is *`download`* ||  ||
|| title^(1)^ || the title of your coupon || varchar(255) ||
|| text^(2)^ || a short text that descripes your coupon || varchar(500) ||
|| url^(3)^ || the download-url || must be valid url ||

JSON example:

```json
[...]
"coupon": {
  "type": "download",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link ...",
  "url": "http://example.com/download"
}
[...]
```

The _*url*_ coupon:

<img align="right" src="http://spreadly.com/img/coupon_type_url.png" />

|| type || the type is *`url`* ||  ||
|| title^(1)^ || the title of your coupon || varchar(255) ||
|| text^(2)^ || a short text that descripes your coupon || varchar(500) ||
|| url^(3)^ || the url to your content || must be valid url ||

JSON example:

```json
[...]
"coupon": {
  "type": "url",
  "title": "Amazon Gutschein von Spreadly",
  "text": "Klicken Sie diesen Link...",
  "url": "http://example.com/visit"
}
[...]
```

## billing

|| type || you can choose between the billing types `like` and `media_penetration` || enum(like, media_penetration) ||
|| target_quantity || the number of likes or media-penetration you want to buy || int ||

To get some informations about the pricing, visit http://spreadly.local/advertiser/dealapi oder write an e-mail to marco@ekaabo.com