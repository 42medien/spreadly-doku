To implement the Spreadly JavaScript Button you have to add the following line to your HTML <head>

`<script type='text/javascript' src='http://button.spread.ly/js/v1/loader.js'></script>`

and

`<a href="{url}" class="spreadly-button"></a>`

at the place, the button should show up. Replace {url} with the URL that should be shared.

## Optional parameters ##

### Adlayer Position ###

to open the adlayer below the button, add the following attribute `data-adlayer-position="bottom"` the complete button code should now look like this:

`<a href="{url}" class="spreadly-button" data-adlayer-position="bottom"></a>`

### Choose service-icons ###