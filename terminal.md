# Terminal

## User Defaults

### Clear user defaults for app

```bash
defaults delete com.emailsignature.Xink
```

You may have to restart your Mac for changes to take effect.

### Read all user defaults for an app

```text
defaults read com.emailsignature.Xink
```

### Set user default value for an app

```text
defaults write com.emailsignature.Xink hideQuitMailInfobox -int 0
```

### Delete named default value for an app

```bash
defaults delete com.emailsignature.Xink hideQuiMailInfobox
```

## Show real iCloud folder on desktop

You may want to view the actual files in your iCloud folder \(also called "Mobile Documents". By default Finder won't let you view the files.  This will create a folder on your desktop called "Real iCloud Drive".

```bash
ln -s ~/Library/Mobile\ Documents/ ~/Desktop/Real\ iCloud\ Drive
```

## Run .sh file from terminal

First grant your .sh file permissions to execute.

```bash
chmod +x myscript.sh
```

Then execute the script.

```bash
./myscript.sh
```

## Get current user

```bash
username=whoami
echo $username
```

You can also use "stat".

```bash
username='stat -f%Su /dev/console'
```

## Reset automation \(AppleEvents\)

```text
tccutil reset AppleEvents
```

## Add app to login items

You can use AppleScript to add an app to login items for automatic startup when you log into your Mac.  Run the AppleScript from Terminal with `osascript`.

```bash
osascript -e 'tell application "System Events" to make login item at end with properties {name:"Xink", path:"/Applications/Xink.app", hidden:false}'
```

## Show codesign certificates

```bash
security find-identity -vp codesigning
```

## Publish app as .pkg

Packaging is done using the pkgbuild tool.  Packaging has two phases:

1. Analyse
2. Build

### Analyse

The analyse phase creates a .plist file with some basic information based on your .app file.  You run the analyse phase like so, assuming your app is called MyApp and it is located in a sub folder called MyAppDeployment:

```bash
pkgbuild --analyze --root "./MyAppDeployment/" MyApp.plist
```

You will now have a file called MyApp.plist.  Double-click it to open it in Xcode.

{% hint style="info" %}
Pay special attention to the`BundleIsRelocatable` setting in the .plist file.  If this setting is true the installer will search for other installations of the .app file and if it finds any it will update the existing file instead of installation to the folder you have specified.

Se this: [https://apple.stackexchange.com/questions/219123/pkgbuild-created-package-does-not-install-correctly?newreg=07f76994de9b4085bef2509004949ac3](https://apple.stackexchange.com/questions/219123/pkgbuild-created-package-does-not-install-correctly?newreg=07f76994de9b4085bef2509004949ac3)
{% endhint %}

### Build

When you are happy with the .plist file you are ready to build the .pkg file.  Run pkgbuild like so to build it.

```bash
pkgbuild --root "./MyAppDeployment/" \
         --component-plist ./MyApp.plist \
         --install-location "/Applications" \
         --identifier "com.MyCompany.MyApp.pkg" \
         --version "3.1.4" \
         MyApp.pkg

```

This will create MyApp.pkg.  When installing the new .pkg file it will install MyApp.app to the Applications folder.

### Sign

Add the --sign flag if you want to sign the .pkg file.  The certificate needs to be an installer certificate name:

```bash
pkgbuild --root "./MyAppDeployment/" \
         --component-plist ./MyApp.plist \
         --install-location "/Applications" \
         --identifier "com.mydomain.MyApp.pkg" \
         --version "3.1.4" \
         --sign "3rd Party Mac Developer Installer: MyCompany" \
         MyApp.pkg
```

### Notarize

The generated pkg file needs to be notarized by Apple.  Otherwise the end user might get the dreaded error "the app is from an unidentified developer" when running the pkg file.  You can upload files for notarization with `xcrun --notarize-app.`

```bash
xcrun altool \
    --notarize-app \  
    --primary-bundle-id "com.eMailSignature.Xink.pkg" \
    --username "[Apple Id email]" \
    --password "[App password for Apple Id]" \
    --file Xink.pkg
```

Go to [https://appleid.apple.com/](https://appleid.apple.com/) to get an application password for your Apple Id.

After uploading the file to the notarization service, you can check the history and status of uploads with `--notarization-history.`

```bash
xcrun altool \
    --notarization-history 0 -u "[Apple Id email]" -p "[App password for Apple Id]"
```

When the notarization is done successfully, you need to stable your file before distributing it to end users.

```bash
xcrun stapler staple "Xink.pkg"
```







