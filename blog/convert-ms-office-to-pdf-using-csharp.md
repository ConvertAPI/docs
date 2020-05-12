# Convert MS Office documents to PDF using C#

When it comes to .NET Core, the document conversions between different file formats are extremely puzzling and complicated.
While searching for the solution, I saw too many developers going mad in StackOverflow, trying to wrap their heads around it.

Finally, I gave up and decided to write my own file processor that I could share with all of you who struggle with it. 
My goal was a tool that makes the conversion of multiple MS Office documents like .docx, .xlsx, .pptx, and more to PDF simple and quick. And here comes the ConvertAPI REST API service that has a C# library.

## Choosing the right MS Office to PDF REST API converter is simple

We are going to use ConvertAPI Office to PDF Rest API service to convert either your local files or files that are hosted on a separate server by specifying the file URLs. You can also easily apply document manipulations like merge, split, rotate, encrypt your source files as well as the converted file result.

## Let’s begin...

First of all, you need to register to get your FREE account at the ConvertAPI.com website https://www.convertapi.com/a. 
The registration process is intuitive and straightforward. You can use a quick sign up feature using your social account.

Once signed in, you will find your Secret Key in the dashboard. Keep this key within reach - we will need this shortly.

![Retrieve secret](https://user-images.githubusercontent.com/62603039/77777970-f6e72d80-7058-11ea-94d8-6b7f7fe01318.png)

## Creating a blank .NET Core console app for MS Office to PDF conversions

We will create a simple C# console app.

![Create new project](https://user-images.githubusercontent.com/62603039/77762236-e11a3e00-7041-11ea-988f-6823143b7d14.png)

Create a new project and select “Console APP” (.NET Core)”. Once done, a new “hello world” project should be created.

![Simple "Hello world" app](https://user-images.githubusercontent.com/62603039/77763796-496a1f00-7044-11ea-8246-e7b8213f95a5.png)

We will then have to add a [ConvertAPI NuGet package](https://www.nuget.org/packages/ConvertApi/) to the project. 
You can either do that using NuGet Package Manager or NuGet Package Manager Console: ```Install-Package ConvertApi```

![NuGet package](https://user-images.githubusercontent.com/62603039/77763863-656dc080-7044-11ea-91cc-b8eba344378c.png)

You can find the source on GitHub if needed ([https://github.com/ConvertAPI/convertapi-dotnet](https://github.com/ConvertAPI/convertapi-dotnet)).

## The project is ready for MS Office to PDF implementation using C#

Let’s write a simple program MS Office to PDF in C# that converts all files placed on the server into PDFs. 

We will start writing our code by initializing the ConvertApi library and specifying the **secret** that we got from the ConvertAPI.com website.

```csharp
var convertapi = new ConvertApi("YOUR_SECRET_HERE");
```

Now let’s write full code that iterates through our list of MS Office file URLs and convert them into PDF programmatically using C# code provided below.

```csharp
using ConvertApiDotNet;
using System.IO;

namespace MsOfficeToPdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // Creating ConvertApi instance and providing our secret key
            var convertapi = new ConvertApi("YOUR_SECRET_HERE");
            
            // Generating a dummy list of file locations
            var documentUrls = new List<string>()
            {
                "https://cdn.convertapi.com/test-files/sample.docx",
                "https://cdn.convertapi.com/test-files/spreadsheet.xlsx",
                "https://cdn.convertapi.com/test-files/presentation.pptx"
            };

            // iterate files and save converted results on a server
            foreach (var doc in documentUrls)
            {
                var convert = await convertApi.ConvertAsync("*", "pdf",
                    new ConvertApiFileParam("File", new Uri(doc))
                );
                await convert.SaveFilesAsync(@"C:\Documents\");
            }
        }
    }
}
```

All the hard work is done by ```convertapi.ConvertAsync();``` method that takes any MS Office document and converts it to PDF. The "*" is a wildcard for the input file format. You can specify file format explicitly, but that is not necessary.
The method has plenty of overloads for your convenience. You can either pass a file from your local drive instead of URL, run the method synchronously, change the destination file format, or even specify advanced conversion parameters.
The API supports many more properties, complete list can be found at https://www.convertapi.com/ms-office-api.

You can also convert your local files from your machine by using the following code snippet:

```csharp
...
    // Path to source file
    string docxFile = @"C:\Documents\Sample.docx";
    // Path to converted file result
    string pdfFile = Path.GetDirectoryName(docxFile) + @"\" + Path.GetFileNameWithoutExtension(docxFile) + ".pdf";

    // Converting a file
    convertapi.ConvertFile(docxFile, pdfFile);
...
```

## Conclusion

File conversions and manipulations are not a headache anymore. The API supports not just MS Office file formats like DOCX, XLSX, PPTX, but eBooks, iWork, emails, images, and more. You can just sit back and watch the job done for you. 
We keep our library supported and up to date. For this example, we used [ConvertAPI NuGet package](https://www.nuget.org/packages/ConvertApi/). 

Feel free to collaborate on our [Git repository](https://github.com/ConvertAPI/convertapi-dotnet)!
