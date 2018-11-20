# Pageable

[![Maintenance](https://img.shields.io/maintenance/yes/2018.svg?style=for-the-badge)](https://github.com/Mobius1/Pageable/)
[![Code Climate maintainability](https://img.shields.io/codeclimate/maintainability/Mobius1/Pageable.svg?style=for-the-badge)](https://codeclimate.com/github/Mobius1/Pageable/maintainability)
![](http://img.badgesize.io/Mobius1/Pageable/master/dist/pageable.js?style=for-the-badge) 
![](http://img.badgesize.io/Mobius1/Pageable/master/dist/pageable.js?compression=gzip&label=gzipped&style=for-the-badge)
[![npm](https://img.shields.io/npm/dt/pageable.svg?style=for-the-badge)](https://www.npmjs.com/package/pageable)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=for-the-badge)](https://github.com/Mobius1/Pageable/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/Mobius1/Pageable.svg?style=for-the-badge)](https://github.com/Mobius1/Pageable/releases)
[![npm](https://img.shields.io/npm/v/pageable.svg?style=for-the-badge)](https://www.npmjs.com/package/pageable)
[![GitHub issues](https://img.shields.io/github/issues-raw/Mobius1/Pageable.svg?style=for-the-badge)](https://github.com/Mobius1/Pageable)
[![GitHub issues](https://img.shields.io/github/issues-closed-raw/Mobius1/Pageable.svg?style=for-the-badge)](https://github.com/Mobius1/Pageable)

Pageable transforms a web page into a full page scrolling presentation.

  - Lightweight (less than 3kb gzipped)
  - Responsive
  - Performant
  - Touch support
  - Easy to set up

---

## Demos
  - [Playground](https://mobius1.github.io/Pageable/)
  - [Adding progress bars](https://mobius1.github.io/Pageable/progress.html)
  - [Fun with delays](https://mobius1.github.io/Pageable/delay.html)
  - [Full-page image gallery](https://mobius1.github.io/Pageable/gallery.html)  

---

## Install

### npm
```
npm install pageable --save
```

---

### Browser

Grab the file from one of the CDNs and include it in your page:

```
https://unpkg.com/pageable@latest/dist/pageable.js
```

You can replace `latest` with the required release number if needed.

---

## Set up

Define a container element that has at least one descendant element with the `data-anchor` attribute.
### HTML
```html
<div id="container">
    <div data-anchor="Page 1"></div>
    <div data-anchor="Page 2"></div>
    <div data-anchor="Page 3"></div>
    <div data-anchor="Page 4"></div>
    ....
</div>
```

Instantiate Pageable and pass a reference to the container in the constructor:
### JS
```javascript
new Pageable("#container");
```

---

You can pass an object as the second paramater to customise the instance:

### JS
```javascript
new Pageable("#container", {
    pips: true, // display the pips
    interval: 300, // the duration in ms of the scroll animation
    delay: 0, // the delay in ms before the scroll animation starts
    throttle: 50, // the interval in ms that the resize callback is fired
    orientation: "vertical", // or horizontal
    swipeThreshold: 50, // swipe / mouse drag distance (px) before firing the page change event
    freeScroll: false, // allow manual scrolling when dragging instead of automatically moving to next page
    navPrevEl: false, // define an element to use to scroll to the previous page (CSS3 selector string or Element reference)
    navNextEl: false, // define an element to use to scroll to the next page (CSS3 selector string or Element reference)
    events: {
        wheel: true, // enable / disable mousewheel scrolling
        mouse: true, // enable / disable mouse drag scrolling
        touch: true, // enable / disable touch / swipe scrolling
    },
    easing: function(currentTime, startPos, endPos, interval) {
        // the easing function used for the scroll animation
        return -endPos * (currentTime /= interval) * (currentTime - 2) + startPos;
    },
    onInit: function() {
        // do something when the instance is ready
    },
    onUpdate: function() {
        // do something when the instance updates
    },    
    onBeforeStart: function() {
        // do something before scrolling begins
    },
    onStart: function() {
        // do something when scrolling begins
    },
    onScroll: function() {
        // do something during scroll
    },
    onFinish: function() {
        // do something when scrolling ends
    },
});
```

---

### Anchors

Any anchor on your page that has a hash that matches the ones in the current `Pageable` instance will trigger scrolling. This allows you to add navigation links without needing to define event listeners or callbacks to get them to trigger a scroll.

---
## Methods

### `next()`
Scroll to next page.
```javascript
pageable.next();
```

### `prev()`
Scroll to previous page.
```javascript
pageable.prev();
```

### `scrollToPage()`
Scroll to defined page number.
```javascript
pageable.scrollToPage(3);
```

### `scrollToAnchor()`
Scroll to defined anchor.
```javascript
pageable.scrollToAnchor("#myanchor");
```

### `orientate()`
Orientate the instance to either vertical or horizontal.
```javascript
pageable.orientate("horizontal");
```

---

## Events

You can listen to Pageable's custom events with the `on(type, callback)` method.

The callback has one argument which returns an object:
```javascript
{
    index: // the current page index
    scrolled: // the current scroll offset
    max: // the maximum scroll amount possible
}
```

### Examples
```javascript
const pages = new Pageable("#container");

pages.on("init", data => {
    // do something when the instance is ready
});

pages.on("update", data => {
    // do something when the instance is updated
    
    // this event also fires when the screen size changes
});

pages.on("scroll.before", data => {
    // do something before scrolling starts
    
    // this event will fire when the defined delay begins
    
    // e.g. if the delay is set to 400, this event will
    // fire 400ms BEFORE the "scroll.start" event fires    
});

pages.on("scroll.start", data => {
    // do something when scrolling starts
    
    // this event will fire when the defined delay ends
    
    // e.g. if the delay is set to 400, this event will
    // fire 400ms AFTER the "scroll.before" event fires
});

pages.on("scroll", data => {
    // do something during scroll
});

pages.on("scroll.end", data => {
    // do something when scrolling ends
});
```

---

Copyright © 2018 Karl Saunders | BSD & MIT license