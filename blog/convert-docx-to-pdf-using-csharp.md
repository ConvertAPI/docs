---
title: How to convert DOCX to PDF using C#?
author_name: Jonas
short_description: Simple C# DOCX to PDF conversion workflow with code snippets to create a C# console app using Visual Studio or JetBrains Rider. All the magic is done by ConvertAPI NuGet library which takes word documents and converts them into PDF. All you need to do is simply paste the complete code snippet into your project and configure it to your own needs. 
meta_description: Convert MS Word documents (DOC/DOCX) to PDF or another file format programmatically using C#. These code snippets demonstrate how to use the REST API library for the .NET Core Console application.
tags: integration,blog post
date_created: 2020-03-27
---
<!--tags: blog post,new,feature,bug,improvements,api,integration-->

When I started using .NET Core framework, I found that document conversions from one file format to another are incredibly tricky. While digging the web, I noticed many people losing their heads about it and no simple solution that suits all. Most of the approaches I found were clumsy and outdated, so I came up with the decision to write my own conversion processor. Since there are so many developers struggling with this issue, I thought it would get me some extra karma points to share it and make it widely accessible. And that's how the ConvertAPI was born.

Maximum efforts were put to craft a tool that makes the conversion of multiple DOCX files to PDF at once intuitive and straightforward. If you develop your code in C#, I'm sure this will be simpler than it sounds. I will explain the process in a few simple steps:

## What exactly is ConvertAPI?

Choosing the right Word to PDF REST API converter is simple. As mentioned above, we will discuss ConvertAPI DOCX to PDF Rest API service. Here are the strengths and features of ConvertAPI:

* No need to have MS Office installed
* Blazing fast conversions from word documents to PDF format
* Convert word to pdf C# without Word interop
* Saving dozens of lines of code, only a couple of C# methods
* No need to rent/buy and maintain servers
* It provides a fully functional FREE version!

## Let’s begin...

First of all, we need to go and register for free at the ConvertAPI.com website https://www.convertapi.com/a. The registration process is quick and simple, you can sign up using your Gmail or Facebook account to make it even faster.

Once registered, you will get your own Secret Key that can be found inside an Overview page. Keep that page open, we will need this key shortly.

![Retrieve secret](https://user-images.githubusercontent.com/62603039/77777970-f6e72d80-7058-11ea-94d8-6b7f7fe01318.png)

## Creating a C# console application to convert a word document to PDF programatically

We will create a C# console app by using Visual Studio. It could also be done with Visual Studio Code or JetBrains Rider.

![Create new project](https://user-images.githubusercontent.com/62603039/77762236-e11a3e00-7041-11ea-988f-6823143b7d14.png)

Create a new project and select “Console APP” (.NET Core)”. Set the path to a project and Voilà! A new “hello world” project is created.

![Simple "Hello world" app](https://user-images.githubusercontent.com/62603039/77763796-496a1f00-7044-11ea-8246-e7b8213f95a5.png)

We will then have to add a [ConvertAPI NuGet package](https://www.nuget.org/packages/ConvertApi/) to the project. To do that, navigate to **Menu > Project > Manage NuGet Packages…** Click on **Browse** and search for “ConvertAPI” NuGet package. Press the Install button. That’s it, there you have it!

![ConvertAPI NuGet package](https://user-images.githubusercontent.com/62603039/77763863-656dc080-7044-11ea-91cc-b8eba344378c.png)

Alternatively, the package can be installed using NuGet Package Manager Console:

```Install-Package ConvertApi```

You can find the source on GitHub if needed ([https://github.com/ConvertAPI/convertapi-dotnet](https://github.com/ConvertAPI/convertapi-dotnet)).

## The project is set up for word docx to pdf implementation using C#

Let’s write a simple program DOCX to PDF in C# that converts all Word files placed in the directory specified  to a PDF file format. 

![Folder structure](https://user-images.githubusercontent.com/62603039/77894440-f5e31580-727d-11ea-8d74-259f24dbd725.png)

We will start coding by initializing the ConvertApi library and specifying our **secret** that we already have from ConvertAPI.com website.

```csharp
var convertapi = new ConvertApi("YOUR_SECRET_HERE");
```

Now let’s write full code that iterates through our Word documents in a C:\Documents folder and convert them into PDF format programmatically using C# code provided below.

```csharp
using ConvertApiDotNet;
using System.IO;

namespace WordToPdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // Creating ConvertApi instance and providing our secret key
            var convertapi = new ConvertApi("YOUR_SECRET_HERE");

            foreach (var docxFile in Directory.EnumerateFiles(@"C:\Documents"))
            {
                // Building path to pdf file
                var pdfFile = Path.GetDirectoryName(docxFile) + @"\" + Path.GetFileNameWithoutExtension(docxFile) + ".pdf";

                // Converting file
                convertapi.ConvertFile(docxFile, pdfFile);
            }
        }
    }
}
```

All the magic is done by line ```convertapi.ConvertFile(docxFile, pdfFile);``` which takes word documents and converts them to PDF.

![Converted results](https://user-images.githubusercontent.com/62603039/77894058-6c334800-727d-11ea-8163-fd88309e9ff8.png)

The API supports a bunch of properties, all of them can be found at https://www.convertapi.com/docx-to-pdf. The ```ConvertApiParam``` object must be created and passed into ```ConvertFile``` method as a parameter. The example below use ```PageRange``` property to limit conversion to 1-3 pages from word document to pdf.

## Complete code

```csharp
using ConvertApiDotNet;
using System.IO;

namespace WordToPdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // Creating ConvertApi instance and providing our secret key
            var convertapi = new ConvertApi("YOUR_SECRET_HERE");

            foreach (var docxFile in Directory.EnumerateFiles(@"C:\Documents"))
            {
                // Building path to pdf file
                var pdfFile = Path.GetDirectoryName(docxFile) + @"\" + Path.GetFileNameWithoutExtension(docxFile) + ".pdf";

                // Creating PageRange parameter. All possible parameters: https://www.convertapi.com/docx-to-pdf
                var pageRange = new ConvertApiParam("PageRange", "1-3");

                // Converting file
                convertapi.ConvertFile(docxFile, pdfFile, new[] { pageRange });
            }
        }
    }
}
```

## Conclusion

There is a really simple and neat way of converting MS Office documents into PDF file formats while leaving all the ugly work for ConvertAPI processor. This API supports not only Microsoft Office file formats like DOCX, XLSX, PPTX, but eBooks, iWork, emails, images and much more. From now on, you simply need to copy your documents into that specified input directory and retrieve the converted results instantly! It really can be set up in less than few minutes, watch a video below and see it in action. In this article we used 
[ConvertAPI NuGet package](https://www.nuget.org/packages/ConvertApi/) ([Git repository](https://github.com/ConvertAPI/convertapi-dotnet)). Try live demo and read more about conversion parameters at https://www.convertapi.com/docx-to-pdf.

That’s it folks, hope you find it helpful!