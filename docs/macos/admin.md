# Admin

## Boot modes

## WD MyCloud NAS:

Finder > Connect to server (cmd + k)
smb://wdmycloud


## Disk Utility (old)

Disk Utility has many formats:

- OS X Extended (Journaled): for casual Mac user
- OS X Extended (Case-sensitive, Journaled): for using with Mac Servers
- MS-DOS (FAT): outdated MS file system, can be used for PC/Mac compatibility but with files less than 4Gb
- ExFAT: more modern MS file system any file size can be used

It also has schemes for when you erase a drive:

- GUID Partition Map (modern Macs and Windows PC)
- Master Boot Record (old Windows PC)
- Apple Partition Map (old PowerPC Macs)

## Command line settings

Remove the Auto-Hide Dock Delay:

    $ defaults write com.apple.Dock autohide-delay -float 0 && killall Dock

Make Hidden App Icons Translucent in the Dock:

    $ defaults write com.apple.Dock showhidden -bool YES && killall Dock

Stop Full Names from Copying with Email Addresses in OS X Mail:

    $ defaults write com.apple.mail AddressesIncludeNameOnPasteboard -bool false

Enable Text Selection in Quick Look Windows: (does not work in El Capitan)

    $ defaults write com.apple.finder QLEnableTextSelection -bool TRUE;killall Finder

(El Capitan) Hide sidebar in Preview when opening a file

    $ cd ~/Library/Containers/com.apple.Preview/Data/Library/Preferences/
    $ defaults write com.apple.Preview PVPDFSuppressSidebarOnOpening true

Always Show Hidden Files in the Finder:

    $ defaults write com.apple.finder AppleShowAllFiles -bool YES && killall Finder

or

    $ defaults write com.apple.finder AppleShowAllFiles True; killall Finder 
    $ defaults write com.apple.finder AppleShowAllFiles False; killall Finder (to restore)

Hide Desktop Icons Completely:

    $ defaults write com.apple.finder CreateDesktop -bool false && killall Finder

Change the Default Screen Shot Image Type:

    $ defaults write com.apple.screencapture type jpg && killall SystemUIServer

Set Plain Text As The Default Format In TextEdit

    $ defaults write com.apple.TextEdit RichText -int 0

Prevent Textedit from saving by default to iCloud

    $ defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false

Override the auto-detection performed by setting `force.LANG' defaults setting
if you use a non-standard setup (e.g. different language than formats)

    $ defaults write org.R-project.R force.LANG en_US.UTF-8

Show only open apps in dock

    $ defaults write com.apple.dock static-only -bool TRUE; killall Dock
    $ defaults write com.apple.dock static-only -bool FALSE; killall Dock  # restore to original state

Stop Adobe Creative Cloud app form auto-launching on login
(loaded by default on `/Library/LaunchAgents/com.adobe.AdobeCreativeCloud.plist`)

    $ launchctl unload -w /Library/LaunchAgents/com.adobe.AdobeCreativeCloud.plist

to set it back again:

    $ launchctl load -w /Library/LaunchAgents/com.adobe.AdobeCreativeCloud.plist

Set, disable, and check sleep status
```
$ sudo systemsetup -setcomputersleep 60
$ sudo systemsetup -setcomputersleep Never
$ sudo systemsetup -getcomputersleep
Computer Sleep: Never
```

## MySQL on macOS

Install MySQL on a Mac OX X

Get the appropriate DMG file from:
http://dev.mysql.com/downloads/mysql/

If you need MySQL for PQLX make sure that you get a Development Release
if not Generally Available (GA) Releases are ok

Click on the pkg installer and follow the instructions

To start the MySQL server, launch System Preferences

Uninstall MySql on a Mac OS X

http://community.jaspersoft.com/wiki/uninstall-mysql-mac-os-x

To completely uninstall MySql OS X it is neccessary to remove numerous files.

Symptom: You unable to install an older version of MySql even though you thought you have removed everything.

Resolution: To uninstall MySQL and completely remove it (including all databases) from your Mac do the following:

Open a terminal window
Use mysqldump to backup your databases to text files!
Stop the database server (e.g. System Preferences)


    sudo rm /usr/local/mysql
    sudo rm -rf /usr/local/mysql*
    sudo rm -rf /Library/StartupItems/MySQLCOM
    sudo rm -rf /Library/PreferencePanes/My*

edit /etc/hostconfig and remove the line MYSQLCOM=-YES-

    rm -rf ~/Library/PreferencePanes/My*
    sudo rm -rf /Library/Receipts/mysql*
    sudo rm -rf /Library/Receipts/MySQL*
    sudo rm -rf /private/var/db/receipts/*mysql*

The last three lines are particularly important as otherwise, you can't install an older version of MySQL
even though you think that you've completely deleted the newer version!  
