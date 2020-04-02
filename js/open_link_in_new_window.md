# Open link in new window

```js
window.open('http://www.google.com', '_blank', 'toolbar=0,location=0,menubar=0');

// Hack for safari
function safariOpenWindowInNewTab (href) {
    var event = document.createEvent('MouseEvents'),
    mac = (navigator.userAgent.indexOf('Macintosh') >= 0);

    // do Ctrl + Shift + LeftClick / Meta + Shift + LeftClick (focus)
    // create your own event
    event.initMouseEvent (
        /* type */ "click",
        /* canBubble */ true
        /* cancelable */ true,
        /* view */ window,
        /* detail */ 0,
        /* screenX, screenY, clientX, clientY */ 0, 0, 0, 0,
        /* ctrlKey */! mac,
        /* altKey */ false,
        /* shiftKey */ true
        /* metaKey */ mac,
        /* button */ 0,
        /* relatedTarget */ null
    );
    // create a link in memory and click this event by reference - a new tab will open
    $ ('<a/>', {'href': href, 'target': '_blank'})[0].dispatchEvent(event);
}
```
