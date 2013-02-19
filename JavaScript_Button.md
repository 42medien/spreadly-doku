To implement the Spreadly JavaScript Button you have to add the following line to your HTML <head>

```HTML
<script type='text/javascript' src='http://button.spread.ly/js/v1/loader.js'></script>
```

and

```HTML
<a href="{url}" class="spreadly-button"></a>
```

at the place, the button should show up. Replace {url} with the URL that should be shared.

## Optional parameters ##

### Adlayer Position

to open the adlayer below the button, add the following attribute `data-adlayer-position="bottom"` the complete button code should now look like this:

```HTML
<a href="{url}" class="spreadly-button" data-adlayer-position="bottom"></a>
```

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

```HTML
<a href="{url}" class="spreadly-button" data-services="twitter,facebook,xing"></a>
```

will show the twitter, facebook and xing icon.

the default icons are: facebook, twitter, linkedin

### Show counter

to show the counter you symply have to add `data-counter="true"`.

```HTML
<a href="{url}" class="spreadly-button" data-counter="true"></a>
```

__IMPORTANT: you can't hide the "package" icon__

## Code examples

### WordPress

Copy and paste this code into a php file, place it in the plugin-directory and activate it.

```php
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
```
