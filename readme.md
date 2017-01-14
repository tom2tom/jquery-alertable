# jquery.alertable.js - Minimal alert, confirm, and prompt replacements.

Developed by Cory LaViska for A Beautiful Site, LLC

Licensed under the MIT license: http://opensource.org/licenses/MIT

## Overview:

This plugin provides a minimal, lightweight, and customizable alternative to `window.alert()`, `window.confirm()`, and `window.prompt()`. It's flexible enough to mold to your application's existing stylesheet and markup.

Features:

- Simple syntax:
    - `$.alertable.alert('Howdy!')`
    - `$.alertable.confirm('You sure?').then(function() { ... })`
    - `$.alertable.prompt('How many?').then(function(data) { ... })`
- Minimal default styles; easy to customize or write your own.
- Show/hide hooks for adding custom animation (works well with Velocity.js).
- Prevents focus from leaving the modal.
- Returns promise-compatible (jQuery deferred) for ok/cancel actions.
- Compact! (about 180 lines)

## Demo

A quick demo can be found on CodePen: http://codepen.io/claviska/pen/mPNWxy

A local demo can be found in `example.html`.

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

// Example with action when the dialog is dismissed
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

Example prompts:

```javascript
// Basic example
$.alertable.prompt('How many?').then(function(data) {
    // Prompt was submitted
});

// Example with then/always
$.alertable.prompt('How many?').then(function(data) {
    // Prompt was submitted
}, function() {
    // Prompt was canceled
}).always(function() {
    // Modal was dismissed
});
```

**Important:** Unlike `window.alert()`, `window.confirm()`, and `window.prompt()`, using this plugin *will not* cause execution of the script to stop while the modal is open. This behavior is not possible to emulate with a plugin nor is it desirable in modern web applications.

### Options

Pass options as the second argument of any method:

```javascript
$.alertable.alert('Howdy!', {
    optionName: optionValue,
    ...
});

$.alertable.confirm('You sure?', {
    optionName: optionValue,
    ...
});

$.alertable.prompt('How many?', {
    optionName: optionValue,
    ...
});
```

Available options:

- `container`: The container to append the modal to. Defaults to 'body'.

- `html`: Whether or not the displayed prompt-message contains HTML. Defaults to `false`.

- `cancelName`: Label for reject button, unless pre-empted by cancelButton option. Defaults to 'Cancel'.

- `okName`: Label for resolve button, unless pre-empted by okButton option. Defaults to 'OK'.

- `cancelButton`: HTML to use for the reject button. Something like
```html
<button id="alertable-cancel" type="button">Cancel</button>
```
Default value: `null`.

- `okButton`: HTML to use for the resolve button. Something like
```html
<button id="alertable-ok" type="button">OK</button>
```
Default value: `null`.

- `overlay`: HTML to use for the overlay. Default value:
```html
<div id="alertable-overlay"></div>
```

- `prompt`: HTML to use for the prompt body. All inputs contained in this HTML will be serialized and returned when the prompt is submitted. Default value:
```html
<input id="alertable-input" type="text" name="value">
```

- `modal`: HTML to use for the modal objects. Default value:
```html
<form id="alertable">
    <p id="alertable-message"></p>
    <div id="alertable-prompt"></div>
    <div id="alertable-buttons"></div>
</form>
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

All methods return a promise-compatible ([jQuery-deferred](https://api.jquery.com/jquery.deferred/)) object. As a result, you can use any of the supported chainable methods. However, the examples above demonstrate the most appropriate ones to use.
