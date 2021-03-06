---
title: Convert a list of images to PDF document using Python
author_name: Kostas
short_description: Having the ability to control all document conversions from a single place is a relief both for developers as well as project managers. This article shows how simple it is to configure and use our Python ConvertAPI library to create a PDF document from multiple images like jpg, png, webp, bmp, gif and others as well as chaining the conversions into a single workflow for all performance benefits. 
meta_description: A quick and simple example demonstrating how to create a PDF Document from multiple images like jpg, png, webp, bmp, gif, etc using our Python ConvertAPI library.
tags: integration,blog post
date_created: 2020-12-30
---
<!--tags: blog post,new,feature,bug,improvements,api,integration-->

In complex information systems, we often need to process document flows and in some cases aggregate and convert documents to other file formats. 
These advanced techniques require lots of time and effort to develop and it becomes a headache to maintain such project infrastructure. In these cases, it is wise to
use a 3rd party tool that specializes in these complex computations and provides an easily maintainable flexible solution to manipulate all sorts of structured data. 
That's where [ConvertAPI Pyhton library](https://github.com/ConvertAPI/convertapi-python) comes in handy.

In this example, we will take a look at how to create a PDF document from a list of images in just a few lines of code.

First, let's install a [ConvertAPI Pyhton library](https://github.com/ConvertAPI/convertapi-python) into our project using [pip](https://pypi.org/project/pip/):

`pip install --upgrade convertapi`

Then, simply paste this code below to your project:

```python
convertapi.api_secret = '<YOUR SECRET HERE>'
convertapi.convert('pdf', {
    'File': '/path/to/1.png'
}, from_format = 'png').save_files('/path/to/dir')
```

That's it, just replace [your secret](https://help.convertapi.com/en/article/how-to-create-a-free-account-2wr644/) and path to your file and it should work straight away. 
Notice that we are using a PNG file in this example. 
To take full advantage of this particular conversion, please refer to the [PNG to PDF converter](https://www.convertapi.com/png-to-pdf) parameters. 
You can set up the conversion there and get the generated code snippet at the bottom of the page.

Conversion can be applied for multiple image file formats like jpg, bmp, gif, webp, and many others in the same manner. 
Simply change the "from_format" parameter to whatever you choose and you are good to go.

In some cases, you might need to generate a PDF document from multiple sources like images and documents. 
To do that, simply convert each document to PDF and merge them into a single document using [PDF -> MERGE](https://www.convertapi.com/pdf-to-merge) conversion.
This conversion accepts a list of files and produces a single PDF output. 
In order to achieve all the performance benefits, you might want to check the [workflows](https://www.convertapi.com/doc/workflows).

Using this simple to use, yet powerful conversion service you can convert your files to 200+ file formats!