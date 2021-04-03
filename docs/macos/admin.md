# Admin

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

