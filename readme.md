# jquery.alertable.js - Minimal alert and confirmation alternatives.

Developed by Cory LaViska for A Beautiful Site, LLC

Licensed under the MIT license: http://opensource.org/licenses/MIT

## Overview:

This plugin provides a minimal, lightweight, and customizable alternative to `window.alert()` and `window.confirm()`. It's flexible enough to mold to your application's existing stylesheet and markup.

Features:

- Simple syntax:
    - `$.alertable.alert('Howdy!')`
    - `$.alertable.confirm('You sure?').then(function() { ... })`
- Minimal default styles; easy to customize or write your own.
- Show/hide hooks for adding custom animation (works well with Velocity.js).
- Prevents focus from leaving the modal.
- Returns promise-compatible (jQuery deferred) for ok/cancel actions.
- Compact! (about 150 lines)

## Demo

A quick demo can be found on CodePen: http://codepen.io/claviska/pen/mPNWxy

## Installing

Include the minified version of this plugin in your project or install via NPM:

```
npm install --save @claviska/jquery-alertable
```

## Using the plugin

Example alerts:

```javascript
// Basic example
$.alertable.alert('Howdy!');

// Example with action when the modal is dismissed
$.alertable.alert('Howdy!').always(function() {
    // Modal was dismissed
});
```

Example confirmations:

```javascript
// Basic example
$.alertable.confirm('You sure?').then(function() {
    // OK was selected
});

// Example with then/always
$.alertable.confirm('You sure?').then(function() {
    // OK was selected
}, function() {
    // Cancel was selected
}).always(function() {
    // Modal was dismissed
});
```

**Important:** Unlike `window.alert()` and `window.confirm()`, using this plugin *will not* cause execution of the script to stop while the modal is open. This behavior is not possible to emulate with a plugin nor is it desirable in modern web applications.

### Options

Pass options as the second argument of either method:

```javascript
$.alertable.alert('Howdy!', {
    optionName: optionValue,
    ...
});

$.alertable.confirm('You sure?', {
    optionName: optionValue,
    ...
});
```

Available options:

- `container`: The container to append the modal to. Defaults to 'body'.

- `html`: Whether or not your message contains HTML. Defaults to `false`.

- `cancelButton`: HTML to use for the reject button. Default value:
```html
<button class="alertable-cancel" type="button">Cancel</button>
```

- `okButton`: HTML to use for the resolve button. Default value:
```html
<button class="alertable-ok" type="button">OK</button>
```

- `overlay`: HTML to use for the overlay. Default value:
```html
<div class="alertable-overlay"></div>
```

- `modal`: HTML to use for the modal. Default value:
```html
<div class="alertable">
    <div class="alertable-message"></div>
    <div class="alertable-buttons"></div>
</div>
```

- `hide`: Function for hiding the modal and overlay. Use `this.modal` and `this.overlay` to reference the modal and overlay elements. Default value:
```javascript
$(this.modal).add(this.overlay).fadeOut(100);
```

- `show`: Function for showing the modal and overlay. Use `this.modal` and `this.overlay` to reference the modal and overlay elements. Default value:
```javascript
$(this.modal).add(this.overlay).fadeIn(100);
```

You may also update the default options *before calling either method*:

```javascript
$.alertable.defaults.optionName = yourValue;
```

### Promises

Both `alert` and `confirm` return a promise-compatible ([jQuery-deferred](https://api.jquery.com/jquery.deferred/)) object. As a result, you can use any of the supported chainable methods. However, the examples above demonstrate the most appropriate ones to use.