# Tips

Reset iCloud bookmarks:

http://sheepsystems.com/discuss/YaBB.pl?num=1327319559/0#0

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

