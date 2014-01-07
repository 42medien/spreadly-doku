---
layout: default
title: Spreadly Doku - Button (JavaScript)
---

To implement the Spreadly JavaScript Button you have to add the following line to your HTML &lt;head /&gt;

{% highlight html %}
<script type='text/javascript' src='http://button.spread.ly/js/v1/loader.js'></script>
{% endhighlight %}

and

{% highlight html %}
<a href="{url}" class="spreadly-button"></a>
{% endhighlight %}

at the place, the button should show up. Replace {url} with the URL that should be shared.

## Optional parameters

### Adlayer Position

to open the adlayer below the button, add the following attribute `data-adlayer-position="bottom"` the complete button code should now look like this:

{% highlight html %}
<a href="{url}" class="spreadly-button" data-adlayer-position="bottom"></a>
{% endhighlight %}
to place the adlayer over the button use the attribute: top

{% highlight html %}
<a href="{url}" class="spreadly-button" data-adlayer-position="top"></a>
{% endhighlight %}

This parameter is optional!

### Button style

With `data-style` you are able to change the "style" of your button.

If missing or set to `classic`

{% highlight html %}
<a href="{url}" class="spreadly-button" data-style="classic"></a>
{% endhighlight %}

you get the classic-style: <a href="http://dev.spreadly.com" class="spreadly-button" data-style="classic">Share</a>

If set to `flat`

{% highlight html %}
<a href="{url}" class="spreadly-button" data-style="flat">Share</a>
{% endhighlight %}

you get a modern flat designed button: <a href="http://dev.spreadly.com" class="spreadly-button" data-style="flat">Share</a>

This parameter is optional!

### Customize social-network-icons

you can customize the social-network-icons with the `data-services` attribute. the spreadly button supports the following networks:

* twitter
* facebook
* linkedin
* xing
* flattr
* tumblr
* none (no social-network-icons except the "package")

the example:

{% highlight html %}
<a href="{url}" class="spreadly-button" data-services="twitter,facebook,xing"></a>
{% endhighlight %}

will show the twitter, facebook and xing icon.

This parameter is optional, the default icons are: facebook, twitter, linkedin

### Show counter

to show the counter you symply have to add `data-counter="true"`.

{% highlight html %}
<a href="{url}" class="spreadly-button" data-counter="true"></a>
{% endhighlight %}

This parameter is optional!

__IMPORTANT: you can't hide the "package" icon__

## Custom HTML

To add the layer to a custom button/link, you simply have to add a `class="spreadly-link"` to the element of your choice.

{% highlight html %}
<a href="{url}" class="spreadly-link"></a>
{% endhighlight %}

If it is a link (`<a />`) the popup uses the `href`-link to share. If you want to use a div/span/... instead, you can use
the `data-spreadly-url` attribute to specify the "link to share".

{% highlight html %}
<div data-spreadly-url="{url}" class="spreadly-link"></div>
{% endhighlight %}

If there is no `data-spreadly-url` or `href`, the popup will share the url of the address-bar.

## Code examples

### WordPress

Copy and paste this code into a php file, place it in the plugin-directory and activate it.

{% highlight php %}
<?php
/*
Plugin Name: Spreadly JavaScript Button
Plugin URI: http://spreadly.com
Description: keine
Version: 1.0.0-beta
Author: pfefferle
Author URI: http://notizblog.org/
License: GPLv2 or later
*/

function spreadly_scripts_method() {
  wp_enqueue_script( 'spreadly-share', 'http://button.spread.ly/js/v1/loader.js' );
}
add_action('wp_enqueue_scripts', 'spreadly_scripts_method');

function spreadly_add_button($content) {
  $button = '<a href="'.get_permalink().'" title="'.get_the_title().'" class="spreadly-button" data-adlayer-position="bottom" rel="share like">Like</a>';

  return $content . $button;
}
add_action('the_content', 'spreadly_add_button', 1);
{% endhighlight %}
