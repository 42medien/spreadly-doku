a 'How to integrate Spread.ly to a various services'

*How to add Spread.ly to...*

# AddThis

Spread.ly is natively supported by AddThis: http://www.addthis.com/services/detail/yiid

You can add it through the "personalize" interface: http://www.addthis.com/personalize

# AddToAny

AddToAny allows you to add some custom services, here is a little example how to add Spread.ly

```html
<a class="a2a_dd" href="http://www.addtoany.com/share_save">
    <img src="http://static.addtoany.com/buttons/share_save_171_16.png" border="0" alt="Share"/>
</a>

<script type="text/javascript">
var a2a_config = a2a_config || {};

a2a_config.custom_services = [
        ["Spread.ly",
                "http://spread.ly/?title=A2A_LINKNAME_ENC&url=A2A_LINKURL_ENC",
                "http://spread.ly/favicon.ico"
        ]
];
</script>

<script type="text/javascript" src="http://static.addtoany.com/menu/page.js"></script>
```

For more customisation, please visit the AddToAny developer doku: http://www.addtoany.com/buttons/customize/

# Google Reader

Go to "Reader Settings" -> "Send To" and klick "Create a custom link" at the end of the page.

Now complete the form like that:

<table>
  <tr>
    <td>Name</td>
    <td>Spread.ly</td>
  </tr>
  <td>
    <td>URL</td>
    <td>`http://spread.ly/?title=${title}&url=${url}`</td>
  </tr>
  <tr>
    <td>Icon URL</td>
    <td>`http://spread.ly/favicon.ico`</td>
  </tr>
</table>

# WordPress

## Share Daddy

Download and install Share Daddy as described here: http://wordpress.org/extend/plugins/sharedaddy/installation/

Go to "Settings" -> "Sharing", click "Add a new service" and fill out the form with the following params:

<table>
  <tr>
    <td>Service name</td>
    <td>Spread.ly</td>
  </tr>
  <tr>
    <td>Sharing URL</td>
    <td>`http://spread.ly/?title=%post_title%&tags=%post_tags%&url=%post_full_url%`</td>
  </tr>
  <tr>
    <td>Icon URL</td>
    <td>`http://spread.ly/favicon.ico`</td>
  </tr>
</table>