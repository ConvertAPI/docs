PDF button makes it easy for your users to save your web site pages as PDF files. There are two types of PDF button:
  
- **Public** - button should be used for pages that are publicly accessible without authentication. This button is simple HTML link tag, no external references needed.
- **Private** - button can be used for any pages even accessible with authentication. This button requires JavaSript library to work.

## Button for public pages

Public PDF button can be placed inside pages that are publicly accessible. This button is simple HTML link. If needed link can be styled with the CSS to look like a button.

Public PDF button example HTML:

```html
<a onclick="this.setAttribute('href', 'https://v2.convertapi.com/convert/web/to/pdf?secret=1234567890123456&download=attachment&url=' + encodeURI(window.location))" href="#">
    Save page as PDF
</a>
```

        <script src="https://cdn.convertapi.com/button.js" data-secret=""></script>
        <link rel="stylesheet" type="text/css" href="https://cdn.convertapi.com/button.css">
        <button class="convertapi-btn">Save page as PDF</button>
