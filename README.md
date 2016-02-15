# Tokenfield

Input field with tagging/token/chip capabilities written in raw JavaScript. Tokens in OS X or Chips in Android -  
small UI elements which are inserted into various inpt fields that often combine with autocomplete functionality.

Tokens allow designers to display extra information about input. For example, in email applications when typing an  
email address of the recipient, input field could display full name of the owner of a given email and a his/her picture.

This Tokenfield implementation is written in raw JavaScript without any extra dependencies like jQuery.

## Examples

View live [examples here](https://kanecohen.github.io/tokenfield).

## Usage

### Via JavaScript

Tokenfield could be applied to any visible `<input />` element that allows users  
to input text or number.

````js
// Given that we have following HTML element: <input class="my-input" />
var tf = new Tokenfield({
  el: document.querySelector('.my-input')
});
````

This action would create Tokenfield wrapped around given input element. Without additional options, this Tokenfield  
would allow users to add multiple token items without any specific restrictions. Only unique items are allowed, though,  
so it is not possible to add multiple items such as: "foo", "bar", "foo". Only first "foo" would be added and the last  
one discarded.

## Options

| Name | Type | Default | Description |
| ---- | ---- | ------- | ----------- |
| el | string or DOM node | null | DOM element or string with selector pointing at an element you want to turn into tokenfield. |
| items | array | [] | Array of objects amongst which autocomplete will try to find a match. Default format might look like this: `[{id: 1, name: 'foo'}, {id: 2, name: 'bar'}]` |
| setItems | array | [] | Array of objects which would be displayed as selected after Tokenfield has been created. |
| newItems | bool | true | Option to allow user to add custom tokens instead of using preset list of tokens or tokens retrevied from the server. |
| multiple | bool | true | Option to allow multiple tokens in the field. |
| maxItems | integer | 0 | Option to limit number of items. Set to 0 to remove the limit. |
| remote | object | | Details on that - below in Autocomplete section. |
| placeholder | null or string | null | Set a placeholder that will be shown in the input. If set to null, will try to use placeholder attribute from the original element set in `el` |
| minChars | integer | 2 | Specifies how many characters user has to input before autocomplete suggester is shown. |
| maxSuggests | integer | 10 | Specifies how many suggestions should be shown. |
| itemLabel | string | `'name'` | Property of an item object which is used to display text in tokens. |
| itemName | string | `'items'` | Each token item will have its own hidden input which will contain an ID of a given item and a name attribute in an array format. This option sets a name. By default it is set to "items" which means that when user will submit a form server would receive an array of IDs under the name "items". |
| newItemName | string | `'itemsNew'` | Same as the above except it is only related to new items which were not added via autocomplete. |
| itemValue | string | `'id'` | Specifies which property from the autocomplete data to use as a primary identfing value. |
| itemData | string | `'name'` | Which property should be used when you do autocomple on a given array of items. |

### Remote Options

Below you will find list of options which are related to remote autocomplete requests. Options are set as properties  
of an object assigned to `remote` property of the parent options object:

````js
new Tokenfield({
  remote: {
    url: "http://example.com",
    ...
  }
});
````

| Name | Type | Default | Description |
| ---- | ---- | ------- | ----------- |
| type | string | `'GET'` | Sets AJAX request type. Usually GET or POST |
| url | string | null | Specifies which URL will be used to retreive autocomplete data. If set to null - remote autocomplete won't be performed. |
| queryParam | string | `'q'` | Sets name of the parameter which would contain value that user typed in the input field. |
| delay | integer | 300 | Sets delay in milliseconds after which remote request is performed. |
| timestampParam | string | `'t'` | Sets parameter for the timestamp when remote call was requested. |
| params | object | `{}` | Sets any additional AJAX params |

## Events

Modal Vanilla uses standard node.js EventEmitter and therefore supports such
event as: 'on', 'once', 'removeAllListeners', 'removeListener'.

For more details on EventEmitter, please check official [https://nodejs.org/api/events.html](documentaion page).

Available events are:

| Event Type | Description |
| ---------- | ----------- |
| change | Fired after any change in tokens list - after adding or removing tokens, setting multiple tokens manually etc. |
| showSuggestions | Fired before Tokenfield would show suggestions box. |
| shownSuggestions | Fired after Tokenfield has shown suggestions box. |
| hideSuggestions | Fired before Tokenfield would hide suggestions box. |
| hiddenSuggestions | Fired after Tokenfield has hidden suggestions box. |


## TODO

Add gif demo, more variances of Tokenfield in demo page, available methods.
