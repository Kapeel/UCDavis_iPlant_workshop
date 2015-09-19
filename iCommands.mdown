# iCommands
This is a short tutorial on using icommands 

#iPlant Data Store 

There are multiple ways to access files and directories on the iPlant [Data Store][iPlant_Data] (aka [iRODS][iRods]) each with their pros and cons.

- **Browser-based Access** --- User-friendly, but low throughput and 2GB upload limit
- **iCommands** --- High throughput with maximum user control, but must be comfortable with the Command-Line Interface
- **iDrop** --- High-throughput desktop client with the ability to schedule periodic transfers
- **API's** --- APIs for programmers

For the list of access methods for [uploading & downloading][UP_and_DOWN]


Regardless of which way you access your data, you need to know where it is located:  
The path to a user's home directory is `/iplant/home/username/` (replace "username", of course).  
The path to shared directories accessible by a user is `/iplant/home/shared/`.

***If you don't have an iPlant account:*** You can register for your account at <https://user.iplantcollaborative.org/register/>.  After registering, go to <https://user.iplantcollaborative.org/dashboard/> to request access to the Atmosphere service by clicking on 'Request Access'.

 useful link:

- [iPlant Data Store Quick Start][iPlant_DataStore_QuickStart]

##1. Browser-based Access

The iPlant Data Store can be accessed via your browser at <https://data.iplantcollaborative.org>. The browser-based method of access is arguably the most intuitive way to access your iPlant data and requires the least amount of setup.  However, there are two major limitations that accompany this convenience: (1) you cannot upload files >2GB and (2) it is difficult or impossible to manipulate or transfer multiple files at the same time via the browser.


##2. [iCommands][iCommands]

iCommands allow you to manipulate the files and directories to which you have access on the iPlant Data Store.

#####Installing and Configuring iCommands

- [Download and install binaries][iCommands_install]
- [Setup auto-complete (for Bash shell --- optional, but nice)][iCommands_autocomplete]
- [Initiate an iRODS connection][iRODS_initiate] by typing: `iinit` and entering the following information if asked:

>Enter the host name (DNS) of the server to connect to: `data.iplantcollaborative.org`  
Enter the port number: `1247`  
Enter your irods user name: `_YOUR_iplantusername`  
Enter your irods zone: `iplant`  
Enter your current iRODS password: `_YOUR_iplantpassword`  


#####Available iCommands

iCommands for transferring files are like their analogous commands, but more robust due to threading:

-  `iput`≈ ftp `put` - upload
-  `iget`≈ ftp `get` - download
-  `irsync`≈ unix `rsync` - synchronize and keep up-to-date

Other [Unix-like iCommands][iCommands_unix]

- `ils` - list attributes of a file or the contents of a directory
- `icp` - copy
- `imv` - move or rename
- `irm` - remove/delete
- `imkdir` - make directories
- `ipwd` - print working directory
- `ichmod` - modify permissions

For more detailed usage information, click on the iCommands above, visit the [iCommands website][iCommands], or type the iCommand followed by `-h` in a Terminal window.  For example, `iput -h` outputs the following:

<!-- begin ils example --> 
>Usage : `ils [-ArlLv] dataObj|collection ...`  
Display data Objects and collections stored in irods.  
Options are:  

>|||
| --- | --- |
| `-A` | ACL (access control list) and inheritance format  |
| `-l` | long format  |
| `-L` | very long format  |
| `-r` | recursive - show subcollections  |
| `-v` | verbose  |
| `-V` | Very verbose  |
| `-h` | this help|
 
>iRODS Version 2.5 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Feb 2011 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ils
<!-- end ils example --> 

#####Uploading files with `iput`

Sample command: `iput -PVbrT` `-X checkpoint_file` `local_directory_or_file` `remote_destination_directory`

Breakdown of sample:

- `iput` uploads a file/directory
- `-P` outputs the progress of the upload
- `-V` turns on 'Very verbose' mode (use `-v` for a less gregarious `iput`)
- `-b` performs bulk uploading and is useful when transferring many small files 
- `-r` transfer all files and subdirectories within the directory being uploaded
- `-T` renews socket connection after 10 minutes (helps keep things stable and robust)
- `-X` turns on the checkpointing function; must specify a temporary checkpoint file 


#####Downloading files with `iget`

Sample command: `iget -PVrT` `-X checkpoint_file` `remote_directory_or_file` `local_destination_directory`

Breakdown of sample:

- `iget` downloads a file/directory
- `-P` outputs the progress of the download
- `-V` turns on 'Very verbose' mode (use `-v` for a less gregarious `iput`)
- `-r` transfer all files and subdirectories within the directory being downloaded
- `-T` renews socket connection after 10 minutes (helps keep things stable and robust)
- `-X` turns on the checkpointing function; must specify a temporary checkpoint file *(see notes for `iput` regarding checkpointing)*

#####Syncing files with `irsync`

Sample commands:

- `irsync -rV` `local_file_or_directory` `i:remote_target_file_or_directory`
- `irsync -rV` `i:remote_file_or_directory` `local_target_file_or_directory` 
- `irsync -rV` `i:remote_file_or_directory` `i:remote_target_file_or_directory` 



<!--
forced spacing: 
a &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; b
-->

<!-- links -->

[iPlant_DataStore]: https://data.iplantcollaborative.org/ "iPlant Data Store"
[iPlant_Data]: http://www.iplantcollaborative.org/discover/data-store "iPlant Data"
[iPlant_DataStore_QuickStart]: https://pods.iplantcollaborative.org/wiki/display/DS/Data+Store+Quick+Start "iPlant Data Store Quick Start"
[UP_and_DOWN]: https://pods.iplantcollaborative.org/wiki/display/DS/Data+Store+Quick+Start "uploading and downloading"
[iCommands]: https://www.irods.org/index.php/icommands "iCommands"
[iCommands_autocomplete]: https://pods.iplantcollaborative.org/wiki/display/DS/Using+iCommands "iCommands autocomplete"
[iCommands_current_download]: https://www.irods.org/index.php/Downloads "Download the current version of iCommands"
[iCommands_install]: https://pods.iplantcollaborative.org/wiki/display/DS/Using+iCommands "iCommands installation"
[iCommands_iPlant]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands "Using iCommmands"
[iCommands_unix]: https://www.irods.org/index.php/icommands#Unix-like_commands "Unix-like iCommands"
[iRods]: https://www.irods.org "iRods.org"
[iRODS_initiate]: https://pods.iplantcollaborative.org/wiki/display/DS/Using+iCommands "initiating iRODS connection"
[atmosphere]: https://atmo-beta.iplantcollaborative.org/ "Atmosphere"
