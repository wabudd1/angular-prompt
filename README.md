# angular-prompt

> Angular service to easily display prompt and confirmation modals.

This library depends on [angular-ui-bootstrap](https://github.com/angular-ui/bootstrap).  

## Demo

[Live Demo](http://wabudd1.github.io/angular-prompt/demo)

## Getting Started

Install with Bower or download the files directly from the dist folder in the repo.
```bash
bower install angular-prompt --save
```

Add `dist/angular-prompt.js` to your index.html.  

Add `cgPrompt` as a module dependency for your module.

```js
angular.module('your_app', ['ui.bootstrap','cgPrompt']);
```

Now you can inject and use the `prompt` service.

```js
function MyCtrl($scope, prompt) {

  //simple confirmation
  prompt({
    title: 'Delete this Thing?',
    message: 'Are you sure you want to do that?'
  }).then(function() {
    // They hit ok and not cancel
  });

  // Ask the user for a string
  prompt({
    title: 'Give me a name',
    message: 'What would you like to name it?',
    input: true,
    label: 'Name',
    value: 'Current name',
    values: ['other','possible','names']
  }).then(function(name) {
    // The promise is resolved with the user input
  });  
}
```

## API

### prompt(options);

 - #### options.title
 Type: `String`  
 Default: `''`
 The title for the dialog.

 - #### options.message
 Type: `String`  
 Default: `''`  
 The message inside the dialog.  Can include HTML.

 - #### options.input
 Type: `Boolean`  
 Default: `false`  
 Set to `true` if you wish to prompt the user for a text value.

 - #### options.inputRequired
 Type: `Boolean`  
 Default: `true`
 Sets the input field to be required or optional.

 - #### options.inputMinLength
 Type: `number`  
 Default: `0`
 Sets a maximum length to the input value.

 - #### options.inputMaxLength
 Type: `number`  
 Default: `1000`
 Sets a minimum length to the input value.

 - #### options.label
 Type: `String`  
 Default: `''`  
 The label for the input if `input=true`.

 - #### options.value
 Type: `String`  
 Default: `''`  
 The initial value of the input if `input=true`.

 - #### options.values
 Type: `Array` of `String`  
 Default: `undefined`  
 A list of values available in a dropdown for the user to select as the input value.

 - #### options.buttons
 Type: `Array` of `Object` with properties `label`,`cancel`, `class`, `style`, and `primary`  
 Default: `[{ label:'OK', primary: true }, { label:'Cancel', cancel: true }]`  
 A list of the buttons to display on the dialog.

The function returns a promise.  That promise is resolved with either the button that was pressed, or in the case of input prompts, the value the user entered.  If the user pressed a button where `cancel=true` or canceled the dialog another way (hit ESC, etc.) then the promise is rejected.

## Release History
* v1.4.0
    * `options.message` is now displayed in the template using `ng-bind-html`, so now you can pass in HTML!
 * v1.3.0
   * Added `style` option to buttons
   * Reordered default buttons (Cancel, OK --> OK, Cancel)
 * v1.2.0
    * Moved to Angular 1.5 and UI Bootstrap 1.3
    * Refactored code to no longer use angular.element(...).scope()
 * v1.1.0
    * Added `class` option to buttons
 * v1.0.1
    * Updated modal template with correct modal title class
    * Added bower_components to ignore in bower.json
    * Moved to angular-bootstrap v0.11
 * v1.0.0 - Initial release
