Converting DOCX to PDF might be a tricky process sometimes. Especially if you want to convert multiple DOCX files at once. Most of the desktop software doesn’t give you this kind of functionality and you can only convert files one by one. What if I told you that in just a few easy steps you could code your own batch DOCX to PDF converter using C#? Sounds complicated? Well, it’s really way easier than it sounds! I will explain the process in a few simple steps:

## Choosing the right Word to PDF REST API converter

For this task we will use ConvertAPI DOCX to PDF Rest API service. Here are the main reasons for it:

* No need to have MS Office installed
* Blazing fast docx to pdf conversions
* Convert word to pdf C# without Word interop
* Saving dozens of lines of code, only a couple of C# methods
* No need to rent/buy and maintain servers
* It provides a fully functional free version!

## Let’s begin...

First of all, we need to go and register for free at the ConvertAPI.com website https://www.convertapi.com/a. The registration process is quick and simple, you can sign up using your Gmail or Facebook account to make it even faster.

Once registered, you will get your own Secret Key that can be found inside an Overview page. Keep that page open, we will need this key shortly.

![Retrieve secret](https://user-images.githubusercontent.com/62603039/77777970-f6e72d80-7058-11ea-94d8-6b7f7fe01318.png)

## Creating a C# console application for DOCX to PDF conversion

We will create a C# console app by using Visual Studio. It could also be done with Visual Studio Code or JetBrains Rider.

![Create new project](https://user-images.githubusercontent.com/62603039/77762236-e11a3e00-7041-11ea-988f-6823143b7d14.png)

Create a new project and select “Console APP” (.NET Core)”. Set the path to a project and Voilà! A new “hello world” project is created.

![Simple "Hello world" app](https://user-images.githubusercontent.com/62603039/77763796-496a1f00-7044-11ea-8246-e7b8213f95a5.png)

We will then have to add a ConvertAPI NuGet package to the project. To do that, navigate to **Menu > Project > Manage NuGet Packages…** Click on **Browse** and search for “ConvertAPI” NuGet package. Press the Install button. That’s it, there you have it!

![ConvertAPI NuGet package](https://user-images.githubusercontent.com/62603039/77763863-656dc080-7044-11ea-91cc-b8eba344378c.png)

Alternatively, the package can be installed using NuGet Package Manager Console:

```Install-Package ConvertApi```

You can find the source on GitHub if needed ([https://github.com/ConvertAPI/convertapi-dotnet](https://github.com/ConvertAPI/convertapi-dotnet)).

## The project is set up for word docx to pdf implementation using C#

Let’s write a simple program DOCX to PDF in C# that converts all Word files placed in the directory specified  to a PDF file format. 

![Folder structure](https://user-images.githubusercontent.com/62603039/77764482-62bf9b00-7045-11ea-82e2-7ca72d3637b8.png)

We will start coding by initializing the ConvertApi library and specifying our **secret** that we already have from ConvertAPI.com website.

```csharp
var convertapi = new ConvertApi("YjBOvutSdT9eVtfa");
```

Now let’s write full code that iterates through our Docx files in a C:\Documents folder and convert them into PDF programmatically using C# code provided below.

```csharp
using ConvertApiDotNet;
using System.IO;

namespace ConsoleApp2
{
    class Program
    {
        static void Main(string[] args)
        {
            // Creating ConvertApi instance and providing our secret key
            var convertapi = new ConvertApi("YjBOvutSdT9eVtfa");

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

All the magic is done by line convertapi.ConvertFile(docxFile, pdfFile); which takes word documents and converts them to PDF.
![Converted results](https://user-images.githubusercontent.com/62603039/77764764-d661a800-7045-11ea-8f32-f0808d6b030f.png)
The API supports a bunch of properties, all of them can be found at https://www.convertapi.com/docx-to-pdf. The ConvertApiParam object must be created and passed into ConvertFile method as a parameter. The example below use PageRange to limit conversion to 1-3 pages from word document to pdf.

## Complete code

```csharp
using ConvertApiDotNet;
using System.IO;

namespace ConsoleApp2
{
    class Program
    {
        static void Main(string[] args)
        {
            // Creating ConvertApi instance and providing our secret key
            var convertapi = new ConvertApi("YjBOvutSdT9eVtfa");

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

To sum up, there is a really simple and neat way of converting multiple Word documents into PDF file formats while leaving all the ugly work for the ConvertAPI processor. From now on, you simply need to copy your documents into that specified input directory and get the converted results instantly! It really can be set up in just a few minutes, watch a video below and see it in action. That’s it folks, hope you enjoy it!
