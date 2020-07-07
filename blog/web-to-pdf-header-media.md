# WEB to PDF converter header and footer images and fonts

In this short blog post we will describe how to use `web` to `pdf` converter header and footer with the images and custom fonts.

## Adding an image to the PDF header

Converter parameter `header` and `footer` accepts string with the HTML.
Unfoturnatly it is impossible to use any remote assets (images, fonts, etc..).
HTML string should contain all the assets as a [data URI](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs).
