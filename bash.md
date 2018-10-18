# Bash

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



