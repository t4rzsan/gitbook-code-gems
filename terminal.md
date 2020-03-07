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

You may want to view the actual files in your iCloud folder \(also called "Mobile Documents". By default Finder won't let you view the files.

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

### Signing

Add the --sign flag if you want to sign the .pkg file.  The certificate needs to be an installer certificate name:

```bash
pkgbuild --root "./MyAppDeployment/" \
         --component-plist ./MyApp.plist \
         --install-location "/Applications" \
         --identifier "com.mydomain.MyApp.pkg" \
         --version "3.1.4" \
         --sign "3rd Party Mac Developer Installer: MyCompany (F23456HVS)" \
         MyApp.pkg
```

