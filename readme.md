# Dropbox Uploader

Forked from https://github.com/andreafabrizi/Dropbox-Uploader

This script is now modified to support OAuth 2.0, multi user access with unique accounts and updated dropbox API. 


Dropbox Uploader is a **BASH** script which can be used to upload, download, delete, list files (and more!) from **Dropbox**, an online file sharing, synchronization and backup service. 

It's written in BASH scripting language and only needs **cURL**.

## Features

* Cross platform
* Support for the official Dropbox API
* No password required or stored
* Simple step-by-step configuration wizard
* Simple and chunked file upload
* File and recursive directory download
* File and recursive directory upload
* Shell wildcard expansion (only for upload)
* Delete/Move/Rename/Copy/List files
* Create share link

## Installation
````bash
$ wget https://code.stats.io/dropbox-sync.sh
$ chmod 755 dropbox-sync.sh
$ mv dropbox-sync.sh /usr/bin
$ echo "dropbox_oauth_token" > /home/username/.dropbox````

## Usage

The syntax is quite simple:

```
./dropbox-sync.sh COMMAND [PARAMETERS]...

[%%]: Optional param
<%%>: Required param
```

**Available commands:**

* **upload** &lt;LOCAL_FILE/DIR ...&gt; &lt;REMOTE_FILE/DIR&gt;  
Upload a local file or directory to a remote Dropbox folder.  
If the file is bigger than 150Mb the file is uploaded using small chunks (default 4Mb); 
in this case a . (dot) is printed for every chunk successfully uploaded and a * (star) if an error 
occurs (the upload is retried for a maximum of three times).
Only if the file is smaller than 150Mb, the standard upload API is used, and if the -p option is used
the default curl progress bar is displayed during the upload process.  
The local file/dir parameter supports wildcards expansion.

* **download** &lt;REMOTE_FILE/DIR&gt; [LOCAL_FILE/DIR]  
Download file or directory from Dropbox to a local folder

* **delete** &lt;REMOTE_FILE/DIR&gt;  
Remove a remote file or directory from Dropbox

* **move** &lt;REMOTE_FILE/DIR&gt; &lt;REMOTE_FILE/DIR&gt;  
Move or rename a remote file or directory

* **copy** &lt;REMOTE_FILE/DIR&gt; &lt;REMOTE_FILE/DIR&gt;  
Copy a remote file or directory

* **mkdir** &lt;REMOTE_DIR&gt;  
Create a remote directory on DropBox

* **list** [REMOTE_DIR]  
List the contents of the remote Dropbox folder

* **share** &lt;REMOTE_FILE&gt;  
Get a public share link for the specified file or directory
 
* **info**  
Print some info about your Dropbox account

* **unlink**  
Unlink the script from your Dropbox account


**Optional parameters:**  
* **-f &lt;FILENAME&gt;**  
Load the configuration file from a specific file

* **-s**  
Skip already existing files when download/upload. Default: Overwrite

* **-d**  
Enable DEBUG mode

* **-q**  
Quiet mode. Don't show progress meter or messages

* **-p**  
Show cURL progress meter

* **-k**  
Doesn't check for SSL certificates (insecure)


**Examples:**
```bash
    ./dropbox-sync.sh -t username upload /etc/passwd /myfiles/passwd.old
    ./dropbox-sync.sh -t username upload *.zip /
    ./dropbox-sync.sh -t username download /backup.zip
    ./dropbox-sync.sh -t username delete /backup.zip
    ./dropbox-sync.sh -t username mkdir /myDir/
    ./dropbox-sync.sh -t username upload "My File.txt" "My File 2.txt"
    ./dropbox-sync.sh -t username list
```