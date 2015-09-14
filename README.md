# iCommands
This is a short tutorial on using icommands on iPlant Atmosphere instance 

#iPlant Data Store Tutorial

There are multiple ways to access files and directories on the iPlant [Data Store][iPlant_Data] (aka [iRODS][iRods]).  Here we will cover three methods, each with their pros and cons.

1. **Browser-based Access** --- User-friendly, but low throughput and 2GB upload limit
- **iCommands** --- High throughput with maximum user control, but must be comfortable with the Command-Line Interface
- **iDrop** --- High-throughput desktop client with the ability to schedule periodic transfers, but iDrop is in beta release and may have bugs

Additionally...

- **Mounting iRods via Atmosphere Instance** --- iPlant's [Atmosphere][atmosphere] cloud service allows you to run analyses on virtual machines (VMs). You can access files on iRods (using any of the three approaches above) when using Atmosphere. This section explains how to mount iRods as a 'normal' volume accessible by your VM.

Regardless of which way you access your data, you need to know where it is located:  
The path to a user's home directory is `/iplant/home/username/` (replace "username", of course).  
The path to shared directories accessible by a user is `/iplant/home/shared/`.

***If you don't have an iPlant account:*** You can register for your account at <https://user.iplantcollaborative.org/register/>.  After registering, go to <https://user.iplantcollaborative.org/dashboard/> to request access to the Atmosphere service by clicking on 'Request Access'.

A couple useful links:

- [iPlant Data Store Cheatsheet][iPlant_DataStore_CheatSheet]
- [iPlant Data Store Quick Start][iPlant_DataStore_QuickStart]

##1. Browser-based Access

The iPlant Data Store can be accessed via your browser at <https://data.iplantcollaborative.org> or <https://data.iplantc.org> (you may get a warning that the latter link is attempting to redirect you to the former, but that's okay).  The browser-based method of access is arguably the most intuitive way to access your iPlant data and requires the least amount of setup.  However, there are two major limitations that accompany this convenience: (1) you cannot upload files >2GB and (2) it is difficult or impossible to manipulate or transfer multiple files at the same time via the browser.

#####Navigation:

- Quickly change to your home directory by clicking the Home icon in the upper-right of the Data Store interface.
- Click on directory names or `... Parent Directory` to navigate to other directories *(see note below)*

#####Uploading and downloading files

- Click on a file name to download the file *(see note below)*
- Click `Upload File` to upload file

#####Checking and modifying access permissions

- Click in the white space to the right of a file/directory name and then click `Access Control` *(see note below)*
- From here, you can set different combinations of read/write access
- When setting permissions for directories, the recursive option will change the permission settings for all files and subdirectories
- Setting a directory to 'sticky' means that any new files/directories created within will inherit the permission settings of the parent directory

#####QuickSharing files with anyone (including non-iPlant users):

Although you can alter permissions to allow other iPlant users to have access to your files, this doesn't help if you want to share files via the iPlant Data Store with colleagues that don't have an iPlant account.  To share with the general public, do the following:

- Click in the white space to the right of a file name and then click `Share/Unshare` *(see note below)*
- After confirming your choice, you will see a URL to the right of the file name in the 'QuickShare' Column.

You can share the URL with people and when they click it, the shared file will download.  Sharing of a file can be stopped by selecting the file and clicking `Share/Unshare` again.  Entire directories cannot be shared in this manner, only individual files.

#####Other types of file manipulation are also possible and include:

- creating directories
- renaming, coping, moving, and deleting files/directories

#####Deleted Files

Deleted files remain (at least temporarily) in your trash folder until you empty the trash.  Click on the Trash icon to view these files.  Here, you can `Restore` deleted files or `Empty Trash`.

*__Note #1__: There is one file/directory per row. Clicking on the name or the icon for a file/directory has a different function than clicking on the white space in that row. Clicking on the white space to the right of the names doesn't change directories or download files, rather it selects the corresponding file or directory for further manipulation. See above for when to click on the name and when to click on the white space.*

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

*__Note #1__: As of August 2012, the current version of iCommands is v3.1; however, the installation files provided by iPlant are v2.5. Version 2.5 seems to work fine and comes available pre-compiled on iPlant. If you want the current version, you can get it directly from [iRods][iCommands_current_download] (but you'll have to compile it yourself).*  
*__Note #2__: If you are on a shared computer, type `iexit` to terminate your iCommands session when finished.*
*__Note #2__: You should only have to initiate an iRODS connection once (unless you are on a shared machine and use `iexit` to terminate your session.*

#####Available iCommands

iCommands for transferring files are like their analogous commands, but more robust due to threading:

- [`iput`][iput] ≈ ftp `put` - upload
- [`iget`][iget] ≈ ftp `get` - download
- [`irsync`][irsync] ≈ unix `rsync` - synchronize and keep up-to-date

Other [Unix-like iCommands][iCommands_unix]

- [`ils`][ils] - list attributes of a file or the contents of a directory
- [`icp`][icp] - copy
- [`imv`][imv] - move or rename
- [`irm`][irm] - remove/delete
- [`imkdir`][imkdir] - make directories
- [`ipwd`][ipwd] - print working directory
- [`ichmod`][ichmod] - modify permissions

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
- `-b` performs bulk uploading and is useful when transferring many small files *(__WARNING...__ see note below)*
- `-r` transfer all files and subdirectories within the directory being uploaded
- `-T` renews socket connection after 10 minutes (helps keep things stable and robust)
- `-X` turns on the checkpointing function; must specify a temporary checkpoint file *(see note below)*

*__Note #1__: __WARNING...__ regarding the use of `-b`: a while ago we had some issues when we used bulk uploading of small files. It seems like there was a problem with excessive disk activity; however, I haven't spent much time looking into this and it may or may not be an issue. Just keep it in mind if you use `-b`.*  
*__Note #2__: When checkpointing with `-X`, be careful about running multiple uploads at the same time. If you do have simultaneous uploads in progress, be sure to use unique names for your `checkpoint_file`. For example, I use a script that names the `checkpoint_file` based on the current date, time, and file/directory being transferred. This ensures that I always have unique names and I also have a record of uploads.*  
*__Note #4__: If your upload fails and you used checkpointing, you can restart from the last successful file uploaded simply by rerunning the `iput` command with the original parameters.*  
*__Note #4__: In addition to checkpointing with `-X` (which keeps track of which files you've already uploaded), the current version of iCommands allows you to do another type of checkpointing that keeps track of how much of the current file has been uploaded. This can be useful when an upload of very large files fails. To turn this type of checkpointing on, use `--lfrestart checkpoint_lf_file` in addition to `-X checkpoint_file`.*

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

##3. iDrop

iDrop is a program that allows the transfer of large files in a high throughput manner. It also has the capability for scheduling periodic transfers:

- [Normal iDrop (download & tutorial)][iDrop_Tutorial] - Allows access to user's home directory
- ["Expert" iDrop (download only)][iDrop_Expert_Download] - Allows access to shared resources, too

*__Note #1__: iDrop is in beta release and may have bugs.*

##Bonus Material: Mounting iRods via Atmosphere Instance

- Full instructions are located [here][iRODS_Mount]. Below is a summary.

#####Summary:

1. After connecting to your Atmosphere instance via `VNC` (and opening `Terminal`) or via `SSH`, type: `iinit` to start initiate iCommands.

- Enter the following information if asked:
>Enter the host name (DNS) of the server to connect to: `data.iplantcollaborative.org`  
Enter the port number: `1247`  
Enter your irods user name: `_YOUR_iplantusername`  
Enter your irods zone: `iplant`  
Enter your current iRODS password: `_YOUR_iplantpassword`  

- Specify where to mount your iRODS volume by typing, for example: `mkdir $HOME/irods_home`

- Mount your iRODS volume by typing: `irodsFs $HOME/irods_home -o max_readahead=0`
	- Type `ipwd` to show the the directory of your iRODS volume that will be mounted.
	- To change select an alternative mount point, use `icd` to change the directory *before* using the `irodsFs` command, for example: `icd /iplant/home/shared/ucd.tomato`.

When I start a new Atmosphere instance and need to mount the iRODS volume at different points, I use the following:

    iinit    #if I haven't already initiated iCommands

    mkdir $HOME/irods_home
    icd /iplant/home/mfc    #use your own iPlant username instead of "mfc"
    irodsFs $HOME/irods_home -o max_readahead=0

    mkdir $HOME/tomato
    icd /iplant/home/shared/ucd.tomato
    irodsFs $HOME/tomato -o max_readahead=0

    mkdir $HOME/brassica
    icd /iplant/home/shared/ucd.brassica
    irodsFs $HOME/brassica -o max_readahead=0

    mkdir $HOME/plantbio
    icd /iplant/home/shared/ucd.plantbio
    irodsFs $HOME/plantbio -o max_readahead=0

*__Note #1__: You may not have access to all of these directories.*  
*__Note #2__: Mounting iRODS volumes like this requires installation of FUSE. This is installed by default on the Atmosphere instances and can be installed elsewhere, too.*
*__Note #3__: If you mount the wrong volume, etc., you can unmount it with `umount $HOME/irods_home`, for example.*

Slightly off topic, if you are using an EBS volume, you can mount it with the following commands (see *Note#1* below if this is the first time using your EBS volume):

    sudo mkdir /mydata    #the mount point doesn't have to be called "mydata"
    sudo chown mfc /mydata    #use your own iPlant username instead of "mfc" (when you make the /mydata directory using sudo, it will belong to 'root'; chown is used to change ownership)
    sudo mount /dev/vdc /mydata

*__Note #1__: Your volume must be formatted before using the first time. You can do this with `sudo /sbin/mkfs /dev/vdc` as described in the [iPlant wiki][iplant_ebs_mount].*  
*__Note #2__: `/dev/vdc` should be the default device if you are only using one EBS volume. If you are using more than one (or `/dev/vdc` doesn't work), check the device in the [Atmosphere][atmosphere] dashboard under "Volume storage management".*

___

___

>>last updated by mike covington @ 2012-07-30  
*if you notice any typos, broken links, etc. or something isn't clear, please contact me!*

<!--
forced spacing: 
a &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; b
-->

<!-- links -->

[iPlant_DataStore]: https://data.iplantcollaborative.org/ "iPlant Data Store"
[iPlant_Data]: http://www.iplantcollaborative.org/discover/data-store "iPlant Data"
[iPlant_DataStore_QuickStart]: https://pods.iplantcollaborative.org/wiki/display/start/Data+Store+Quick+Start "iPlant Data Store Quick Start"
[iPlant_DataStore_CheatSheet]: https://pods.iplantcollaborative.org/wiki/download/attachments/7525221/DataStoreCheatSheet.pdf?version=1&modificationDate=1324329532000 "DataStoreCheatSheet.pdf"
[iCommands]: https://www.irods.org/index.php/icommands "iCommands"
[iCommands_autocomplete]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands#Usingicommands-SettingupBashautocompleteforicommands "iCommands autocomplete"
[iCommands_current_download]: https://www.irods.org/index.php/Downloads "Download the current version of iCommands"
[iCommands_install]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands#Usingicommands-Downloadingandconfiguringicommands "iCommands installation"
[iCommands_iPlant]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands "Using iCommmands"
[iCommands_unix]: https://www.irods.org/index.php/icommands#Unix-like_commands "Unix-like iCommands"
[iDrop_Tutorial]: https://pods.iplantcollaborative.org/wiki/display/start/Using+the+iDrop+Desktop+and+iDrop+Lite+Java+applets "iDrop Tutorial"
[iDrop_Expert_Download]: https://pods.iplantcollaborative.org/wiki/download/attachments/7519648/idrop-expert.jar "iDrop 'Expert'"
[iRods]: https://www.irods.org "iRods.org"
[iRODS_initiate]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands#Usingicommands-InitiateconnectiontoiRODS%3Aiinit "initiating iRODS connection"
[iRODS_QuickStart]: https://pods.iplantcollaborative.org/wiki/display/docs/iRODS+Quick+Start+Examples "iRods Quick Start"
[iRODS_Mount]: https://pods.iplantcollaborative.org/wiki/display/start/Mounting+the+iRODS+Directory+with+FUSE "Mounting iRODS"
[ils]: https://www.irods.org/index.php/ils "ils"
[imv]: https://www.irods.org/index.php/imv "imv"
[icp]: https://www.irods.org/index.php/icp "icp"
[imkdir]: https://www.irods.org/index.php/imkdir "imkdir"
[ipwd]: https://www.irods.org/index.php/ipwd "ipwd"
[irm]: https://www.irods.org/index.php/irm "irm"
[ichmod]: https://www.irods.org/index.php/ichmod "ichmod"
[iput]: https://www.irods.org/index.php/iput "iput"
[iput_example]: https://pods.iplantcollaborative.org/wiki/display/start/Using+icommands#Usingicommands-Uploadingmultiplefilesoradirectory%28withrecursion%29 "Uploading multiple files or a directory (with recursion)"
[iget]: https://www.irods.org/index.php/iget "iget"
[irsync]: https://www.irods.org/index.php/irsync "irsync"
[atmosphere]: https://atmo-beta.iplantcollaborative.org/ "Atmosphere"
[iplant_ebs_mount]: https://pods.iplantcollaborative.org/wiki/display/atmman/Attaching+an+EBS+Volume+to+an+Instance#AttachinganEBSVolumetoanInstance-AttachinganEBSvolumetoaninstance
