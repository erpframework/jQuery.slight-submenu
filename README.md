# jQuery Slight Submenu plugin

## Why is this?

For the single purpose of automating nested menu management with the slight presence of javascript.

## Short overview

### What does it do?
- adds behavior related to nested unordered lists - adds buttons for expand/collapse inside the corresponding list item with the nested UL
- lets you configure every aspect of the plugin in any way you want - setting button events of your choice, modifying added css classes, executed callbacks, even overriding defaults globally

### Features:
- very easy to use and just a few kilobytes in size with full control over every aspect that the plugin touches;
- *does not shadow* any **a**'s hrefs (this is why buttons are used to expand/collapse submenus);
- possibility to replace defaults globally
- almost no css, as this plugin is intended to add behavior so its up to you how things will look
- multilevel submenu nesting with each nesting for itself (full control, again)
- inline css option allowing css to be applied inline (by default it is not) for the javascript lover and the one who would need that kind of functionality
- deep nesting (loose, even uneven structure, no pun intended) for fine control even in the most markup-twisted situation or for custom scenarios (say an accordeon)
- supports even ie7+ (keep in mind that jQuery 2.* and upwards does not support < IE9 and if you use that, no support for those old browsers)

For a showcase of those features you can have a look at the GitHubPages [demo page](http://velidar.github.io/jQuery.slight-submenu/) or the demo page which is included with the plugin.

### Limitations:
- only a single submenu (UL) in a LI is supported and will work as expected;
- currently, opening/closing a submenu always uses a "submenu button" (for now you cannot delegate this responsibility directly to the corresponding &lt;a&gt; next to the button) though you can emulate the behaviour
- I can't think of any other major limitations;

### Min jQuery version: 1.8

## Plugin options and usage:

To use the plugin you need >= jQuery 1.8 and the plugin itself:

```javascript
<script src="http://code.jquery.com/jquery-1.8.0.min.js"></script>
<script src="js/jquery.slight-submenu.min.js"></script>
```

If you are not using inline css (plugin option), there is some mandatory css (for things to work) that you might want to include or copy contents from:

```javascript
<link rel="stylesheet" href="css/slight-submenu.css" />
```

After that you can simply apply the plugin to an element/s which has/have an UL (or is itself an UL) and has in his children LIs another UL (to become a submenu):

```javascript
$('selector').slightSubmenu(options);
 ```

### Options:

You can modify almost every aspect that the plugin has contact with:

```javascript
$('#master-menu').slightSubmenu({
    buttonActivateEvents: 'click mouseenter',   // Space separated events string (just as you would use in a plain jQuery .on('events-string', ...) ) that activate the expand/collapse buttons
    buttonCloseNotSubmenuEvents: 'mouseenter',  // the events that should collapse a submenu are the same as the ones that open it - this option lets you specify those that should not be able to close it
    multipleSubmenusOpenedAllowed: true,    // pretty straighforward - if set to false, only a single submenu at a time can stay expanded 
    prependButtons: false,  // this is where to put the buttons inside the parent LI - in the beginning (true) or just before the submenu UL (false)
    applyInlineCss: false,  // more control with javascript
    topUlClass: 'slight-submenu-master-ul', // class for the top most ul, holding the LIs with submenu ULs
    topLiClass: '', // class for the top UL LIs
    topLiWithUlClass: 'li-with-ul', // class for the LIs that hold an UL
    buttonClass: 'slight-submenu-button',   // class for the expand/collapse buttons
    buttonSubmenuOpenedClass: 'opened', // class for the button when its corresponding submenu is visible
    submenuUlClass: 'slight-submenu-ul',    // class for the 
    directLiInlineCss: $.fn.slightSubmenu.defDirectLiInlineCss, // *InlineCss options hold js objects with css definitions (those options correspond to the elements we can attach classes to)
    submenuUlInlineCss: $.fn.slightSubmenu.defSubmenuUlInlineCss,
    topContainerInlineCss: $.fn.slightSubmenu.defTopContainerInlineCss,
    buttonInlineCss: $.fn.slightSubmenu.defButtonInlineCss,
    buttonActiveInlineCss: $.fn.slightSubmenu.defButtonActiveInlineCss,
    // callbacks that control the way the currently processed submenu is managed
    handlerButtonIn: $.fn.slightSubmenu.handlerButtonIn,    // receives a jQuery object (the $submenuUl) as an argument; makes the menu visible
    handlerForceClose: $.fn.slightSubmenu.handlerForceClose // receives a jQuery object (the $submenuUl) as an argument; hides the menu
    handlerGenerateButtonMarkup: $.fn.slightSubmenu.handlerGenerateButtonMarkup // allows for custom submenu button markup 
});
```

The referenced $.fn.slightSubmenu.* objects/functions look like this:
 
```javascript
$.fn.slightSubmenu.handlerButtonIn = function($submenuUl) {
    $submenuUl.show(1000);
};

$.fn.slightSubmenu.handlerForceClose = function($submenuUl) {
    $submenuUl.hide(1000);
};

// the passed argument, by default is settings.buttonClass
$.fn.slightSubmenu.handlerGenerateButtonMarkup = function(buttonClass) {
    return '<span class="' + buttonClass + '"></span>';
};

$.fn.slightSubmenu.defTopContainerInlineCss = { position: 'relative' };
$.fn.slightSubmenu.defDirectLiInlineCss = {};   
$.fn.slightSubmenu.defSubmenuUlInlineCss = {};
$.fn.slightSubmenu.defButtonActiveInlineCss = {};

$.fn.slightSubmenu.defButtonInlineCss = {
    background: '#ccc',
    display: 'inline',
    marginLeft: '8px',
    width: '10px',
    height: '18px',
    position: 'absolute',
    cursor: 'pointer'   // this might be the difference 
                        // between the 'click' working on iOS and not
};
```

You can guess you can replace (globally) any of that with your own defaults as it is all public.

```javascript
$.fn.slightSubmenu.handlerButtonIn = function($submenuUl) {
    // code
};
 ```
 
Have fun using the plugin! 