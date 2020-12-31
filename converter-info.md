Converter information endpoint https://v2.convertapi.com/info contains the complete and up to date information about our provided converters and their properties, 
types, default values, etc. Using this endpoint you can create a dynamic document converter. 
Visual representation of this file can be found here: https://www.convertapi.com/docx-to-pdf. 
This page and the whole https://www.convertapi.com/converters section is built based on that XML.

Full converters specification:

`[GET]
https://v2.convertapi.com/info
`

Specific converter's parameters (in this case DOCX to PDF):

`[GET] https://v2.convertapi.com/info/docx/to/pdf`

List all converter that supports conversion to a PDF file format:

`[GET] https://v2.convertapi.com/info/*/to/pdf`
