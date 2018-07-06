# Bash

## Clear user defaults for app

```bash
defaults delete com.emailsignature.eMS365
```

Restart your Mac for changes to take effect.

## Show real iCloud folder on desktop

You may want to view the actual files in your iCloud folder \(also called "Mobile Documents". By default Finder won't let you view the files.

```text
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



