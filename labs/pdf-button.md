## Save page as PDF button implementation

PDF button makes it easy for your users to save your web site pages as PDF files. There are two types of PDF button:
  
- **Public** - button should be used for pages that are publicly accessible without authentication. This button is simple HTML link tag, no external references needed.
- **Private** - button can be used for any pages even accessible with authentication. This button requires JavaSript library to work.

## Button for public pages

Public PDF button can be placed inside pages that are publicly accessible. This button is simple HTML link. If needed link can be styled with the CSS to look like a button.

Please sign in to test this example.

Public PDF button example HTML:

```javascript
<a onclick="this.setAttribute('href', 'https://v2.convertapi.com/convert/web/to/pdf?secret=<YOUR SECRET HERE>&download=attachment&url=' + encodeURI(window.location))" href="#">
    Save page as PDF
</a>
```
Result:

```
<decode>
<a href="#" class="d-block mb-3" onclick="this.setAttribute('href', 'https://v2.convertapi.com/convert/web/to/pdf?secret=<YOUR SECRET HERE>&amp;download=attachment&amp;url=' + encodeURI(window.location))">Save page as PDF</a>
</decode>
```
  

Conversion parameters can be set as a URL query parameters. More information about WEB to PDF conversion parameters can be found in converter page. To hide button itself during conversion use hideelements parameter. This parameter accepts element selector string e.g. to hide button with 'convertapi-btn' class set 'hideelements=.convertapi-btn'.

## Button for private pages

Private PDF button can be placed inside pages that are not publicly accessible. Pages can be protected with any kind of authentication. All linked resources (JS, CSS, images) inside HTML must be publicly accessible. Button requires JS library though CSS library is optional.

Please sign in to test this example.

Private PDF button example HTML:

```javascript
<script src="https://cdn.convertapi.com/button.js" data-secret="<YOUR SECRET HERE>"></script>
<link rel="stylesheet" type="text/css" href="https://cdn.convertapi.com/button.css">
<button class="convertapi-btn">Save page as PDF</button>
```
Result:

```
<decode>
<script src="https://cdn.convertapi.com/button.js" data-secret="<YOUR SECRET HERE>"></script>
<button class="convertapi-btn mb-3">Save page as PDF</button>
</decode>
```
  

## Parameters

### Script tag

Tag includes JavaScript library and it must contain data-secret or data-token attributes.

- **data-secret** - your API secret. Secret can be found in Control Panel.
- **data-token** - token.
- **data-apikey** - your API key. Must be provided if self generated token is used. API Key can be found in Control Panel.
- **data-selector** - button element selector. Default is: '.convertapi-btn'.
- **data-progressclass** - class that will be set to a button element when conversion takes place. Default: 'convertapi-progress'.
- **data-errorclass** - class that will be set to a button element when conversion fails. Default: 'convertapi-error'.

### Button tag

Tag must have 'convertapi-btn' class or the one that is set by data-selector attribute of the script tag.

- **data-filename** - converted pdf file name (without extension). Default: 'page'.
- **data-format** - conversion result format. Available values: 'pdf', 'png', 'jpg'. Default: 'pdf'.
- **data-view** - to display file in the browser instead of downloading it. Available values: 'true', 'false'. Default: 'false'.
- **data-params** - other conversion parameters. Format is the same as URL query parameter: 'parameter=value&parameter=value&etc...'. All conversion parameters can be found in PDF converter page.

