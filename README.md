jquery.adaptive-background.js
===============================
_A simple jQuery plugin to extract the dominant color of an image and apply it to the background of its parent element._

**[Check it out on the web!](http://briangonzalez.github.io/jquery.adaptive-backgrounds.js/)**

Getting Started
------------------
Simply include jQuery and the __[script](https://raw.github.com/briangonzalez/jquery.adaptive-backgrounds.js/master/src/jquery.pep.js)__ in your page, then run the script like so:

```javascript
$(document).ready(function(){
  $.adaptiveBackground.run()
});
```

The script looks for image(s) with the `data-adaptive-background` attribute:

```html
<img src="/image.jpg" data-adaptive-background='1'>
```

Demo 
-----------
Here's a little demo of how it works. (1) The page loads (2) the dominant background color of the image is extracted (3) said color is applied to parent of image.
<img src="https://raw.github.com/briangonzalez/jquery.adaptive-background.js/master/misc/ab.gif">

API
---
This plugin exposes one method:
- __$.adaptiveBackground.run(opts)__ _arg: opts (Object)_ an optional argument to be merged in with the defaults.

Default Options
----------------
- __selector__ String _(default: `'img[data-adaptive-background="1"]'`)_ a CSS selector which denotes which images to grab/process. Ideally, this selector would start with _img_, to ensure we only grab and try to process actual images.
- __parent__ falsy _(default: `null`)_ a CSS selector which denotes which parent to apply the background color to. By default, the color is applied to the parent one level up the DOM tree.

__Example:__
Call the `run` method, passing in any options you'd like to override.

```javascript
var opts = {
  selector: '.some-selector',
  parent:   '.some-parent-of-some-selector'
}
$.adaptiveBackground.run(opts)
```

Events Emitted
--------------
- __ab-color-found__ [Event](http://api.jquery.com/category/events/event-object/) This event is fired when the dominant color of the image is found. The payload includes the dominant color as well as the color palette contained in the image.

__Example:__
Subscribe to the `ab-color-found` event like so:

```javascript
$('img.my-image').on('ab-color-found', function(payload){
  console.log(payload.color);   // The dominant color in the image.
  console.log(payload.palette); // The color palette found in the image.
});
```

Caveats
--------------
This plugin utlizes the `<canvas>` element and the `ImageData` object, and due to cross-site security limitations, the script will fail if one tries to extract the colors from an image not hosted on the current domain, *unless* the image allows for [Cross Origin Resource Sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing). This plugin is built on top of a script called [RGBaster](https://github.com/briangonzalez/rgbaster.js). 

Author
-------
| ![twitter/brianmgonzalez](http://gravatar.com/avatar/f6363fe1d9aadb1c3f07ba7867f0e854?s=70](http://twitter.com/brianmgonzalez "Follow @brianmgonzalez on Twitter") |
|---|
| [Brian Gonzalez](http://briangonzalez.org) |

License
-------
MIT, yo.
