---
title: Apply watermark to PDF programatically
author_name: Kostas
short_description: When working with documents, you might want to watermark them at some point. Some of the widespread use cases include marking invoices as paid, watermarking documents as a copy or a draft, etc. Our fast and secure ConvertAPI library allows you easily apply custom watermarks to your PDF using any programming language of your choice.
meta_description: Apply Watermark to PDF programmatically. Mark invoices as paid, watermark documents as a copy or a draft, etc., using a ConvertAPI library with any programming language you choose. 
tags: integration,api,blog post
date_created: 2021-02-18
---
<!--tags: blog post,new,feature,bug,improvements,api,integration-->

When working with documents, you might want to watermark them at some point. Some of the widespread use cases include marking invoices as paid, watermarking documents as a copy or a draft, etc.
Our fast and secure ConvertAPI library allows you easily apply custom watermarks to your PDF using any programming language of your choice. ConvertAPI provides three different endpoints to watermark your PDF:

- [PDF to WATERMARK API](https://www.convertapi.com/pdf-to-watermark)
- [PDF to WATERMARK-OVERLAY API](https://www.convertapi.com/pdf-to-watermark-overlay)
- [PDF to WATERMARK-TEXTBOX API](https://www.convertapi.com/pdf-to-watermark-textbox)

Each of these endpoints has its specific use cases. Let's discuss these options.

## Prerequisites

First of all, if you haven't used ConvertAPI yet, please [sign up](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and get your free secret key. We will use it later in the process. 
Then, feel free to grab a ConvertAPI library for your programming language: [DotNet](https://www.convertapi.com/doc/dotnet-library), 
[Java](https://www.convertapi.com/doc/java-library), [Python](https://www.convertapi.com/doc/python-library), [Ruby](https://www.convertapi.com/doc/ruby-library), 
[PHP](https://www.convertapi.com/doc/php-library), [Go](https://www.convertapi.com/doc/go-library), [NodeJS](https://www.convertapi.com/doc/node-library), 
[CLI](https://www.convertapi.com/doc/cli-library), or even use [Zapier](https://www.convertapi.com/labs/zapier). Connect it to your ConvertAPI account using [a secret key](https://www.convertapi.com/a/auth).

## PDF to WATERMARK API

[PDF to WATERMARK API](https://www.convertapi.com/pdf-to-watermark) allows adding a textual watermark to your document with a bunch of useful options.
You can style your watermark by choosing your font family, size, color, stroke width, watermark text rotation in angles, page range where watermarks should be applied, the watermark position, alignment, opacity, etc.
You can even apply a link to the watermark, so when it's clicked, it can open a specified web page or jump to a page in the document.
The text itself can be a static string or a dynamic value, like page number, file name, many formats of the current date, author, title, or other document's metadata property.
The complete list of properties as well as auto-generated code snippets can be found under the development section of our [live demo](https://www.convertapi.com/pdf-to-watermark).

## PDF to WATERMARK-TEXTBOX API

[PDF to WATERMARK-TEXTBOX API](https://www.convertapi.com/pdf-to-watermark-textbox) is very similar to the above, except that it allows injecting a new line (**%N%**) command to your watermark text.
It is useful if your watermark text contains a long text string or simply if you want to format it nicely. 
If you want to watermark the document with a dynamic piece of content, where the text is entered into a text area or an RTE, this option should be the option of your choice.

## PDF to WATERMARK-OVERLAY API

Another common use case is to watermark a PDF with an image or even another document. 
You can watermark it with any label, badge, stamp, etc., that can be passed as a PDF file or a PDF URL if you host your documents online.
You can position, align and scale it to fit your needs. You can also make your watermark a link, pointing to a website or the section of the document.

## Watermarked PDF examples

![PDF Watermark Examples](https://user-images.githubusercontent.com/62603039/108332087-18ed1f80-71d8-11eb-91ab-3f0ccce0dad9.png)

## Conclusion

Watermark your PDFs easily and anyway you like using our reliable REST API service. 
You can apply multiple watermarks to your documents by setting up a [conversion workflow](https://www.convertapi.com/blog/conversion-workflow).
Once you have an account ready and an SDK library set up in your project, 
visit our [live demo](https://www.convertapi.com/pdf-to-watermark) tool and grab an automatically generated code snippet based on your parameter inputs. You don't need any expert knowledge to watermark your PDFs programmatically. We are here to do it for you!
