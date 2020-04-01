## Automate file conversion on your desktop or server

The ConvertAPI Automator is a tool for converting from one file format to another (e.g. `docx` -> `pdf`).
Using is as simple as copying files to input directory and getting results from output directory.
Supports creating PDF and Images from various sources like Word, Excel, Powerpoint, images, web pages or raw HTML codes.
Merge, Encrypt, Split, Repair and Decrypt PDF files are also supported as well as many other file manipulations.
You can setup and start converting files in less than a minute .

The ConvertAPI Automator is using an online Convert API service that is processing all the conversions (get your free secret at https://www.convertapi.com/a).
Files are sent using the secure `https` protocol to convertapi.com and are converted in the cloud. Once finished the result is sent back to your computer.
Files can also be supplied in the `zip` archive, automator will unzip it for you automatically.  

## Installation

Download compressed executable

* Linux: [convertapi-automator_linux.tar.gz](https://github.com/ConvertAPI/convertapi-automator/releases/download/v4/convertapi-automator_linux.tar.gz)
* Mac OS X: [convertapi-automator_osx.tar.gz](https://github.com/ConvertAPI/convertapi-automator/releases/download/v4/convertapi-automator_osx.tar.gz)
* Windows: [convertapi-automator_win.zip](https://github.com/ConvertAPI/convertapi-automator/releases/download/v4/convertapi-automator_win.zip)

(this utility can also be built from the source code for many other CPU and OS)

Unzip executable 

```shell
unzip convertapi-automator_*.zip
```

And you are done.
Optionally you can move the executable file to a more appropriate place and make the utility accessible for all local users.
On Linux it would be:   

```shell
sudo mv convertapi-automator /usr/local/bin
```

### Docker
Run docker image:

```shell
docker run -e "CONVERTAPI_SECRET=YOUR_SECRET_HERE" -v /tmp/caa:/var/lib/caa baltsoftcorp/convertapi-automator --watch --dir=/var/lib/caa
```
- **<YOUR_SECRET_HERE>** replace with your secret. If you sing-in the secret will be replaced automatically.
- **/tmp/caa** replace with your local input directory path


### Windows service
`convertapi-automator_win.zip` should contain Windows service installation script `register-win-service.bat`.
To run convertapi-automator as a Windows service follow these steps:

- Edit `register-win-service.bat` and replace `<SECRET>` with your convertapi.com secret.
- Set `--dir=` parameter to your input directory (parameter can be used multiple times).
- Run `register-win-service.bat` **as administrator**.


## Usage

### Before you start
In order to be able to use this utility you must create your free trial account on https://www.convertapi.com site.  
After the sign up process you will get your secret key at https://www.convertapi.com/a .
Secret must be supplied as a command line argument.

### Simple conversion
Short usage example demonstrating how to convert DOCX file to PDF.
Prepare input directory before conversion (MS Windows):

- Create input directory where you will copy files for conversion (e.g. `C:\path\to\convertdir`).
- Copy `docx` file to the input directory.
- Create a subfolder `pdf` inside the input directory.

**IMPORTANT READ CAREFULLY!!!** All files that are located inside the input directory will be **DELETED** during the conversion.
Make sure that the input directory contains no other files but a **copy** of your original document.

```shell
convertapi-automator.exe --secret=YOUR_SECRET_HERE --dir=C:\path\to\convertdir 
```

After the program is finished you will find your `pdf` file inside `C:\path\to\convertdir\pdf`


### Command line arguments 

#### --secret
Your convertapi.com secret.
If not set CONVERTAPI_SECRET environment variable will be used.
It can be obtained from https://www.convertapi.com/a for free.

_Example:_

```shell
--secret=YOUR_SECRET_HERE
```

#### --dir
Input directory with output directories structure inside.
This parameter can be set multiple times to have multiple input directories.

**IMPORTANT READ CAREFULLY!!!** All files that are located inside the input directory will be **DELETED** during the conversion.

_Example:_

```shell
--dir=/path/to/inputdir --dir=/other/inputdir
```

#### --level
Argument `--dir` may be used for the directory that has subdirectories as input directories.
`--level` defines the level of subdirectories that should be treated as input directories.
Default value is `0` (`--dir` is the direct input directory).    

_Example:_ 

```shell
--dir=/conversions --level=2
```

Then the directory structure could be:

```text
/conversions
    ├ user1
    │   └ topdf
    │       └ pdf
    └ user2
        └ tojpg
            └ jpg
```

As `level` is set to `2`, `/conversions/user1/topdf` and `/conversions/user2/tojpg` is going to be treated as input directories.
More subdirectories can be added inside `/conversions` without convertapi-automator service restart.
This structure is convenient for a multiuser environment.
`/conversions/user1` and `/conversions/user2` can be shared with read write permissions on the local network.
This way users can add more conversion input directories by themselves.


#### --watch
Run convertapi-automator in input directories watching mode.
All files that are placed inside the input directories will be converted and **deleted**.

If convertapi-automator is used as an integrated part of other software, STDOUT can be read to get a converted file’s full path.

_Example:_ 

```shell
--watch
```

#### --concurrency
Defines how many file conversions can run at once.
Value too high can cause failing conversions.
The default value is `10`.

_Example:_ 

```shell
--concurrency=15
```


### Configuration files
Each output directory can contain `config.txt` file with the conversion parameters used during the conversion.
Each parameter is declared in a new line separating parameter name and value using `=` sign.

_Example:_ 

```text
/my/conversions
    ├ encrypt
    │   └ config.txt
    └ jpg
```

_config.txt_
```text
PdfOwnerPasswordNew=mysecretpass1
PdfUserPasswordNew=mysecretpass2
EncryptType=AES256ISO
```

Parameters are specific to conversion type.
Parameters with the description can be found on [convertapi.com](https://www.convertapi.com/conversions) site.

There are built in parameters that are used just by convertapi-automator:
- **JoinFiles** - wait for all files from the parent directory and use them in one conversion (must be used with `merge` conversion). Default: `JoinFiles=false` 
- **SaveIntermediate** - if conversions are chained but intermediate results are also needed set this parameter to `true`. Default: `SaveIntermediate=false`

### Examples

#### DOCX to PDF and JPG
`docx` files copied to `/my/conversions` will be converted to `pdf` and `jpg` formats.
All files that are located inside the input directory will be **DELETED** during the conversion.

Directory structure:

```text
/my/conversions
    ├ pdf
    └ jpg
```
Command:

```shell
convertapi-automator --secret=YOUR_SECRET_HERE --dir=/my/conversions 
```


#### PPT to PNG and TIFF in "watcher" mode
`ppt` files copied to `/my/conversions` will be converted to `png` and `tiff` file formats.
All files that are located inside the input directory will be **DELETED** during the conversion.

Directory structure:

```text
/my/conversions
    ├ png
    └ tiff
```
Command:

```shell
convertapi-automator --secret=YOUR_SECRET_HERE --dir=/my/conversions --watch 
```

#### Multiple input directories example
Multiple input directories are useful for having many different conversion scenarios.
convertapi-automator can run on a server watching multiple input directories assigned (shared) to separate users.
This way you only need one running instance of the tool to automate all your organisation.
All files that are located inside the input directories will be **DELETED** during the conversion.

Directory structure:

```text
/user1/imgconv
    ├ png
    └ tiff

/user1/splitpdf
    └ split

/user2/topdf
    └ pdf

/user3/totext
    └ txt
```
Command:

```shell
convertapi-automator --secret=YOUR_SECRET_HERE --dir=/user1/imgconv --dir=/user1/splitpdf --dir=/user2/topdf --dir=/user3/totext --watch 
```

#### Conversion chaining
Sometimes one conversion is not enough and several conversions must be applied to a single file.
Conversion chaining solves this problem with ease. 
Create subdirectories inside your output directories named by further conversion format.
Directory structure for converting `docx` to `pdf` and compressing pdfs to make them smaller (`docx` -> `pdf` -> `compress`).
All files that are located inside the input directories will be **DELETED** during the conversion.

```text
/convert/topdf
    └ pdf
        └ compress
```

Command:

```shell
convertapi-automator --secret=YOUR_SECRET_HERE --dir=/convert/topdf --watch 
```

Output directories can contain multiple subdirectories. The results will then be converted into each of them.
There is no limitation on conversion chain length, so any number of directories can be nested.


#### Chaining and configuration

This example illustrates hypothetical conversion `docx` -> `pdf` -> `merge` -> `rotate`. 
Converted files are stored inside the `merge` directory before rotation and rotated versions of the files will be stored in the `rotate` directory.  

```text
/conversion/splitandrotate
    └ pdf
        └ merge
            ├ config.txt
            └ rotate   
                └ config.txt
```

`/conversion/splitandrotate/pdf/merge/config.txt`
```text
JoinFiles=true
SaveIntermediate=true
```

`/conversion/splitandrotate/pdf/merge/rotate/config.txt`
```text
RotatePage=180
```

Command:

```shell
convertapi-automator --secret=YOUR_SECRET_HERE --dir=/conversion/splitandrotate --watch 
```

When running in `--watch` mode and merging files, input files must be provided in the `zip` archive.
The archive provides information to the automator that all files inside the zip must be merged.


### Issues &amp; Comments
Please leave all comments, bugs, requests, and issues on the Issues page. We'll respond to your request ASAP!

### License
The ConvertAPI Automator is licensed under the [MIT](http://www.opensource.org/licenses/mit-license.php "Read more about the MIT license form") license.
Refer to the [LICENSE](https://github.com/ConvertAPI/convertapi-automator/blob/master/LICENSE) file for more information.
