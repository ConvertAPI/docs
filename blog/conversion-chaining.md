One of our feature-rich conversion service advantages is conversion chaining. 
We've seen so many services implementing it in wrong, anti-pattern ways that make the code slow and hardly reusable.

We solved this issue by what we call a REST API Conversion Chaining. 
It simply means applying multiple conversions to a file uploaded to our server by calling the appropriate conversion methods 
via REST API. There is no need to download a partial result and reupload it. 
This simple data flow diagram below describes the process of the real-world example we will discuss in a moment.

![Data flow diagram](https://user-images.githubusercontent.com/62603039/82210296-74bc0c80-9917-11ea-9164-eb951413eea0.png)

## Why use conversion chaining?

Conversion chaining improves the performance and provides you the flexibility to process your file conversions step by step. 
This way, you gain the ability to handle all of the exceptions you might encounter at any point during the conversion flow. 
This best-practice driven REST API pattern allows you to continue the communication from where it failed without the need to rerun the whole process again. 
Sounds complicated? It's actually more straightforward than it sounds. Let's dive into a real-world demo!

## Real-world example

For this demonstration we will use a pretty common PDF to JPG conversion example. This conversion produces multiple files as 
each PDF page is split into a separate JPEG image. Let's say you want to ZIP the images into a single archive and download it. 
You can achieve that by uploading a single file and specifying further conversions.

All of our libraries support this feature. Let's use PHP language for this particular example.
For other programming languages, please refer to [our Docs](https://www.convertapi.com/doc/chaining).
Please note that the StoreFile=true parameter must be set when calling the conversion endpoint to store the file on our server for further processing.

```php
<?php
require __DIR__ . '/../lib/ConvertApi/autoload.php';

use \ConvertApi\ConvertApi;

# set your API secret
ConvertApi::setApiSecret(getenv('CONVERT_API_SECRET'));

# Short example of conversions chaining, the PDF pages extracted and saved as separated JPGs and then ZIP'ed
# https://www.convertapi.com/doc/chaining

$dir = sys_get_temp_dir();

echo "Converting PDF to JPG and compressing result files with ZIP\n";

$jpgResult = ConvertApi::convert('jpg', ['File' => 'files/test.pdf']);

$cost = $jpgResult->getConversionCost();
$count = count($jpgResult->getFiles());

echo "Conversions done. Cost: ${cost}. Total files created: ${count}\n";

$zipResult = ConvertApi::convert('zip', ['Files' => $jpgResult->getFiles()]);

$cost = $zipResult->getConversionCost();
$count = count($zipResult->getFiles());

echo "Conversions done. Cost: ${cost}. Total files created: ${count}\n";

$savedFiles = $zipResult->saveFiles($dir);

echo "File saved to\n";

print_r($savedFiles);
```

## Conclusion

To put it in a nutshell, conversion changing is the best practice for processing documents with the performance and flexibility perks. 
It is implemented in all of our libraries. Use this approach to write a clean, reusable and performance-oriented code! 
Read more about conversion chaining in our [Documentation](https://www.convertapi.com/doc/chaining). Happy coding!
