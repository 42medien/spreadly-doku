This document is intended for developers who want to write applications that can interact with the Spreadly Button API

# Getting Started

The Spread.ly button is a tool to share content in several social networks simultanously. This content can also be deals of many sorts that give incentives to the user for liking an item. You can use the Spread.ly button API to customize many aspects of the sharing experience for your users.

# Mandatory Parameters

Mandatory parameters are the minimum requirement for the button to work. You should set them programmatically for your software (cms, blog or online shop software) - otherwise you would need to configure each button manually for every separate page (url). 

<table>
  <tr>
    <td>url</td>
    <td>This is the single most important parameter, because this is the link to your page that is shared to the social networks. At the moment we don't do any normalization on your url. This means that you have to take care yourself to assure that slightly different links are counted for the same URL, e.g. you might want http://spreadly.com and https://spreadly.com and http://spreadly.com/ and maybe even http://www.spreadly.com to point to the same, normalized URL. That way all clicks on these variants of the Spread.ly homepage are counted for e.g. http://spreadly.com. If you don't do any normalization, all of the above links would have their separate counter. Possible values: must apply to W3C RFC 3986.</td>
  </tr>
  <tr>
    <td>social</td>
    <td>The "social" parameter decides if there are profile images of your friends below the button (only if your friends have liked this URL before). A maximum of 3 images is shown. Possible values: 1 = show profile images, 0 = hide profile images. Default value: 1. Minimum iframe height value if set to "1": 60px. If set to "0": 24px.</td>
  </tr>
</table>

*Example*:

_iFrame_:

```html
<iframe src="http://button.spread.ly/?url={url}&social={1|0}" 
        style="overflow:hidden; width: 420px; height: 30px; padding: 0px 0;"
        frameborder="0"
        scrolling="no"
        marginheight="0"
        allowTransparency="true">
</iframe>
```

_link_:

```html
<a href="http://spread.ly/?url={url}" 
   target="_blank"
   rel="like">
  <img src="http://spreadly.com/img/staticbutton.png"
       alt="Like"
  />
</a>
```

# Optional Parameters

Optional parameters can enhance the user experience decidedly, by giving you more control over how your shared content will look like. If you don't define these parameters, the Spread.ly crawler software will visit your page and will try to determine the most relevant content programmatically.

||title||The title of the shared post. Possible values: urlencoded string literals. Default value: grabbed from Open Graph og:title tag, fallback is HTML title tag.||
||description||The description text of the shared post. Possible values: urlencoded string literals. Default value: grabbed from Open Graph og:description tag, fallback is HTML description meta tag.||
||photo||An image from the shared post, e.g. a product image. Possible values: urlencoded image URL. Default value: grabbed from Open Graph og:image tag, fallback is a selection of images scraped from your page (the user hase to choose, in case there are several possibilities).||
||tags||You can add one or more comma-separated words as tags to describe e.g. the product category for this button. This is particularly important for deals that are intended for selected categories only.||
||color||You can customize the color scheme of the button by setting a default color. The color must be the six digits hex color without the hash (#), for example: "973765" (this is the default color of the button)||
||label||The urlencoded label of the button, the default label is "like"||

*Example*:

_iFrame_:

```html
<iframe src="http://button.spread.ly/?url={url}&social={1|0}&title={title}&description={description}&photo={photo-url}&tags={tag,tag}&label={like}&color={973765}" 
        style="overflow:hidden; width: 420px; height: 30px; padding: 0px 0;"
        frameborder="0"
        scrolling="no"
        marginheight="0"
        allowTransparency="true">
</iframe>
```

_link_:

```html
<a href="http://button.spread.ly/?url={url}&title={title}&description={description}&photo={photo-url}&tags={tag,tag}&color={973765}" 
   target="_blank"
   rel="like">
  <img src="http://spreadly.com/img/staticbutton.png"
       alt="Like"
  />
</a>
```

# Other Restrictions

* Maximum length for the iframe URL including all parameter settings is 2000 characters.
* At this time there is no usage limitation concerning the number of requests.

== Full Example ==

A complete example how a share button/link could look like. Sample page: http://spreadly.com

||url||http://spreadly.com/||
||social||1||
||title||Spread.ly||
||description||first choice for social sharing||
||photo||http://spreadly.com/img/spreadlyicon.jpg||
||tags||like,deal,spread,share||
||color||973765||
||label||share||

_iFrame_:

```html
<iframe src="http://button.spread.ly/?url=http%3A%2F%2Fspreadly.com%2F&social=1&title=Spread.ly&description=first%20choice%20for%20social%20sharing&photo=http%3A%2F%2Fspreadly.com%2Fimg%2Fspreadlyicon.jpg&tags=like%2Cdeal%2Cspread%2Cshare&color=973765&label=share" 
        style="overflow:hidden; width: 420px; height: 60px; padding: 0px 0;"
        frameborder="0"
        scrolling="no"
        marginheight="0"
        allowTransparency="true">
</iframe>
```

_link_:

```html
<a href="http://button.spread.ly/?url=http%3A%2F%2Fspreadly.com%2F&title=Spread.ly&description=first%20choice%20for%20social%20sharing&photo=http%3A%2F%2Fspreadly.com%2Fimg%2Fspreadlyicon.jpg&tags=like%2Cdeal%2Cspread%2Cshare&color=973765" 
   target="_blank"
   rel="like">
  <img src="http://spreadly.com/img/staticbutton.png"
       alt="Like"
  />
</a>
```