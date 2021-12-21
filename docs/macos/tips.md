# Tips

Reset iCloud bookmarks:

http://sheepsystems.com/discuss/YaBB.pl?num=1327319559/0#0

## Screen capture

`cmd + SHIFT + 3`			: capture entire desktop to file

`cmd + ctrl + SHIFT + 3`		: copy entire desktop to clipboard

`cmd + SHIFT + 4 , selection`	: capture selection

`cmd + SHIFT + 4 , space bar`	: capture selected window


Change the Default Screen Shot Image Type:

    defaults write com.apple.screencapture type jpg && killall SystemUIServer
    defaults write com.apple.screencapture type png && killall SystemUIServer

## Shortcuts

Alternative shortcuts for copy, paste, etc:

    Cut = Ctrl+X = Shift+Delete
    Copy = Ctrl+C = Ctrl+Insert
    Paste = Ctrl+V = Shift+Insert
    Undo = Ctrl+Z = Alt+Backspace


## Safari

Save Web Pages as PDF files (Mac, iPad and iPhone)
javascript:pdf_url=location.href;location.href='http://pdfmyurl.com?url='+escape(pdf_url)

## Word

Default font in Word: Cambria
Change default:

Formato > Fuente > Predeterminar	(then click "OK")
Format > Font > Set Default

Add line numbers for manuscript:

Formato > Diseño de documento | Diseño | Números de línea | Agregar numeración de línea | Continuo

Default fone in TextEdit: Monaco

## Mail

Signature with font/images in Mail:

create with TextEdit an rtf file using fonts, etc
copy signature from TextEdit and paste it in Mail > Preferences > Signatures

Capture signature with Preview

Preferences > Signatures (take picture with camera)

To add signature:

Use Preview. Annotations toolbar > Signature button (click and drag for signature size and location)

Customize folder (or file) icon:

- Copy image for icon in clipboard (from preview, photoshop, ...)
- Open "Get Info"
- Select small icon on top (not large one in preview)
- Paste image

To delete, select again small icon and hit delete.

Do not show updates to new operating system:

    $ sudo softwareupdate --ignore "macOS Catalina"
    $ defaults write com.apple.systempreferences AttentionPrefBundleIDs 0 # this eliminates red circle in Dock icon
    $ killAll Dock

To reset

$ sudo softwareupdate --reset-ignored

## Command line tools to free space

Docker:

    $ docker system prune --all

Conda:

    $ conda clean --all

Git:

    $ git gc --aggressive --prune=now

Homebrew:

    $ brew cleanup -s

Mac/Linux Cache Folder:

    $ rm -r ~/.cache

Create space in a Time Machine disk that is almost full:

```console
$ sudo tmutil delete /Volumes/Time\ Machine\ Backups/Backups.backupdb/Antonio’s\ iMac/2016-0?-*
Password:
Deleting: /Volumes/Time Machine Backups/Backups.backupdb/Antonio’s iMac/2016-01-07-125646
.
.
.
```

Set file as template:

Get Info > Stationery 

Clicking on file duplicates it.

Versions in TextEdit:

File > Revert Document... > Browse versions

Setup a shortcut for Launchpad

System Preferences > Keyboard > Keyboard shortcuts > Launchpad & Dock
(double click and hit enter in "Show Launchpad" and introduce new shortcut, e.g. alt + cmd + l)


## Dropbox

- Make soft links to Dropbox folders:

% ln -s ~/Dropbox/Documentos ~/Documentos

- Text notes

- Copy DNI, passport, etc. Folder "Travel" with travel documents
- Contacts(?): ~/Library/Application Support/Address Book

- Folder with photos (shared with family's iPad)

## Google Earth

To fix error "Unable to contact the login server"

```console
$ rm -rf ~/Library/Caches/Google\ Earth
$ rm -rf ~/Library/Caches/com.Google.GoogleEarth*
$ rm -f ~/Library/Preferences/com.google.GoogleEarth*
$ rm -f ~/Library/Preferences/com.google.GECommonSettings.plist
```

## Misc commands


To create the locate database (/var/db/locate.database)
run the following command: 

    $ sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist

Needed another command to update it regularly??

Remove duplicate entries from "Open with" menu

    $ /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain user
    $ killall Finder

Always Show the User Library Folder:

    $ chflags nohidden ~/Library/

## Shortcuts

cmd + tab		toggle between applications
cmd + `	(backtick)	toggle between windows of same application	
cmd + shift + H		Finder goes to home directory


select elements in same folder ; cmd + ctrl + N ; creates a new folder and moves selected elements 


Delete key (delete following character): fn + backspace or ctrl + D
Delete word:                             
Delete paragraph

ctrl + alt + backspace: delete previous word
cmd + backspace: delete until beginning of line

(dock) - show all windows

## Setup a shortcut for Launchpad

System Preferences > Keyboard > Keyboard shortcuts > Launchpad & Dock
(double click and hit enter in "Show Launchpad" and introduce new shortcut, e.g. alt + cmd + l)


## SPOTLIGHT

cmd + Space			open/close Spotlight search field
cmd + alt + Space		open/open  Spotlight window (Finder)

click opens document
while preview press cmd key to see path, text, etc.
cmd + alt shows path
cmd + click opens finder window pointing to document

on popover preview you can "pre listen", FaceTime, email, ...

you can drag an element of the search to the Desktop or to an Application

cmd + alt + drag creates a link in the destination folder

cmd + ctrl + F = search "filename contains"

## TEXT

cmd + up	inicio del documento
cmd + down	final del documento

cmd + left	inicio de línea
cmd + right	final de línea

alt + left	inicio de palabra
alt + right	final de palabra

## SAFARI

cmd + L		selects url (useful to delete it or copy it)
cmd + alt + F	move input to search field
cmd + alt + 2	show history

space bar	scroll down
shift + space 	scroll up

cmd + click		open link in new tab of foreground
cmd + shift + click	open link in new tab on background

cmd + shift + left/right	move between tabs

cmd + I			mail entire web page
cmd + shift + I		mail link to web page

cmd + shift + D		add page to reading list
shift + click		add link to reading list (no need to open page)
cmd + shift + L		open reading list

Look for more by checking the menus on Safari

## Application shortcuts

Create shortcuts for specific applications:

System preferences | Keyboard | Keyboard shortcuts | Application shortcuts


SPACES/DESKTOPS

(fn +) F8			shows/hides all Spaces/Desktops

(fn +) F11			shows/hides Desktop

ctrl + arrow			changes Space
ctrl + 1			changes to Space 1

cmd + shift + 3			captures entire screen to png file
cmd + shift + 4			captures selected area to png file
cmd + shift + 4	Spacebar	captures selected Application window

(cmd + ctrl + ...		copies capture to clipborad)		

Do not work (in Lion)

(fn +) F9			shows/hides all Applications in current Space (also minimized)
				if pressed after (fn +) F8 shows all Applications in all Spaces
(fn +) F10			shows/hides all windows of current Application

2 fingers up/down		scroll
2 fingers left/right		back/next in Safari (behavior in other apps?)
				(both work with one finger in Magic Mouse)

3 fingers up/down		opens/closes Mission Control (same as clicking Mission Control on the Dock)
				(does not work on Magic Mouse)
3 fingers right/left		changes between full screen apps and the Desktop(s)
				(two fingers on the Magic Mouse)

Default font in Word: Cambria
Change default:

Formato > Fuente > Predeterminar	(then click "OK")
Format > Font > Set Default

Add line numbers for manuscript:

Formato > Diseño de documento | Diseño | Números de línea | Agregar numeración de línea | Continuo

Default fone in TextEdit: Monaco

## For work

Java (not installed by default)

Office, Adobe CSS5.X, Adobe Acrobat 10, EndNote

Papers2

Vdl, Unarchiver
iTerm2

## For Home

Handbrake:		rip DVDs/CDs
Calibre:		eBooks

## Settings

Import Gmail calendars in iCal
Firefox Sync
Enable home sharing (?) 
Mail?

## Command-line preferences

Change capture file format from png to jpg:

    $ defaults write com.apple.screencapture type jpg
    $ killall SystemUIServer

Disable all animations:

    $ defaults write com.apple.finder DisableAllAnimations -bool true

Disable widgets:

    $ defaults write com.apple.dashboard mcx-disabled -boolean YES
    $ killall Dock

Display iTunes tracks in the Dock

    $ defaults write com.apple.dock itunes-notifications -bool TRUE ; killall Dock

Add recent items stack:

    $ defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }' ; killall Dock 

Run maintenance scripts:
```console
$ ls -la /var/log/*.out
-rw-r--r--  1 root  wheel  366451 Jul 10 11:34 /var/log/daily.out
-rw-r--r--  1 root  wheel    1832 Jul 10 11:34 /var/log/monthly.out
-rw-r--r--  1 root  wheel    3814 Jul 10 11:34 /var/log/weekly.out
$ sudo periodic daily weekly monthly
```


## Searchable PDF - OCR

Scanners: Fujitsu ScanSnap S1300 (includes software Abbyy FineReader)
          Epson WorkForce Pro    (")

Abbyy FineReader
DevonThink Pro Office - includes PDF manager
PDFpen

Prizmo for iPhone

## Convert EPS to PNG

```console

# EPSTOPNG

#####
#    convert  ImageMagick
#    gm convert GraphicsMagick
#
#    this script will convert an EPS to a PNG with 150 dots/inch ~ 90 dots/cm which is OK
#    for PowerPoint
#  
#    The background is forced to be white and the transparency removed
#####


EPS=$1
BASE=`basename ${EPS} .eps`
#gm convert -trim -density 150x150 -resize 1000x1000 -verbose ${BASE}.eps ${BASE}.png
convert -trim -density 150x150 -resize 1000x1000 -background white -alpha remove -verbose ${BASE}.eps ${BASE}.png




# EPSTOPNG30

#####
#    convert  ImageMagick
#    gm convert GraphicsMagick
#
#    this script will convert an EPS to a PNG with 300 dots/inch ~ 120 dots/cm which is OK
#    for PowerPoint
#  
#    The background is forced to be white and the transparency removed
#####


EPS=$1
BASE=`basename ${EPS} .eps`
#gm convert -trim -density 300x300 -resize 2000x2000 -verbose ${BASE}.eps ${BASE}.png
convert -trim -density 300x300 -resize 2000x2000 -background white -alpha remove -verbose ${BASE}.eps ${BASE}.png



# EPSTOPNGWHITE

EPS=$1
BASE=`basename ${EPS} .eps`
convert -trim ${EPS} -background white -alpha remove -alpha off ${BASE}.png
```


## More tips

- FileVault encripts data
- Verify and repair disk permissions
- Disk utility can create partitions

- Textedit opens rtf, Word (doc/docx) and OpenOffice documents
  Can create pdf directly (Export as PDF)
  Can toggle between rtf and txt
  Can create tables and lists

- VoiceOver install additional voices!!!

- Preview can export to PDF
  Can add annotations to PDF
  Can add signature to PDF
  Can convert color to B/W
  Can make screen capture
  Select images and convert them to same height and width (Tools > Adjust Size)
  Can edit images, crop
