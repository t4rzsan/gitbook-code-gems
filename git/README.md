# Git

## Cloning

Start by cloning a repo from Github or Bitbucket.org.

```text
git clone https://github.com/hocuspocus/icsharp.git
```

This will create a subfolder of the current folder name "aspnet-core-with-webpack" containing all the code.

## Edit configuration

On Windows the Git configuration file is usually placed under "c:\Users\\[user\]". You can also start an editor from the command prompt.

```text
git config --global -e
```

### Set editor for commit messages

To change the default editor for commit messages to Notepad++, add a \[core\] section to the config file looking like this.

```text
[core]
    editor = 'C:/put-your-folder-here/Notepad++/notepad++.exe' -multiInst -notabbar
```

From now on Notepad++ will open when ever you run git commit without the -m switch.

### Set merge tool to Visual Studio

```text
[diff]
    tool = vsdiffmerge
[difftool]
    prompt = true
[difftool "vsdiffmerge"]
    cmd = \"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Professional\\Common7\\IDE\\CommonExtensions\\Microsoft\\TeamFoundation\\Team Explorer\\vsDiffMerge.exe\" \"$LOCAL\" \"$REMOTE\" //t
    keepbackup = false
    trustexistcode = true
[merge]
    tool = vsdiffmerge
[mergetool]
    prompt = true
[mergetool "vsdiffmerge"]
    cmd = \"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Professional\\Common7\\IDE\\CommonExtensions\\Microsoft\\TeamFoundation\\Team Explorer\\vsDiffMerge.exe\" \"$REMOTE\" \"$LOCAL\" \"$BASE\" \"$MERGED\" //m
    keepbackup = false
    trustexistcode = true
```

## Submodules

### Cloning submodules

If the repo contains submodules, and you want to bring the code in the submodules down, you'll need to clone recursively.

```text
git clone --recursive https://github.com/hocuspocus/icsharp.git
```

### Change submodule to own fork

If you have cloned a repo with a submodule and you want to change the submodule to a different fork \(if for example you have forked the submodul\), you need to edit the URL in the file .gitsubmodule.

```text
[submodule "Engine"]
    path = Engine
    url = https://github.com/scriptcs/scriptcs.git
```

After saving .gitsubmodule, run the command.

```text
git submodule sync
```

It seems that this may detach from HEAD, so a checkout may be necessary \(before making any local changes\).

```text
git checkout
```

If you have trouble downloading the code for the submodule, try running the command:

```text
git submodule update --remote
```

## Start merge tool

If there is a merge tool, you can start your merge tool \(set in the config file\).

```text
git mergetool
```

## Compare to remote

Start by fetching all from the remote repo:

```text
git fetch origin
```

Then compare with local:

```text
git log HEAD..origin/master --oneline
```

If you are happy with the results, you may merge the remote changes with the local repo:

```text
git merge
```

## Show remote URL

Show remote URL for "origin":

```text
git remote get-url origin
```

For at bit information you may use:

```text
git remote show origin
```

I your remote has moved, you can change the URL using _set-url_:

```text
git remote set-url origin https://hocuspocus@bitbucket.org/myteam/myproject.git
```

## Delete branch

Delete the remote branch:

```text
git push -d <remote_name> <branch_name>
```

For example:

```text
git push -d origin my-feature-branch
```

You may also use:

```text
git push <remote_name> :<branch_name>
```

Delete the local branch:

```text
git branch -d <branch_name>
```

## Delete local changes

Undo all unstaged local changes:

```text
git checkout .
```

Undo git add for at single file:

```text
git reset folder/file.cs
```

Undo `git add .` :

```text
git reset .
```

## Undo latest commits

To undo the latest commit\(s\) use reset.

```bash
git reset @~N
```

Here _N_ is the number of commits to undo.  To undo the latest commit use reset @~1.

```bash
git reset @~1
```

A reset will leave changed files unstaged.

## Fix untracked files

```bash
git rm . -r --cached
git add .
git commit -m "Fixed untracked files"
```

## Create an alias for a command

If you are tired of typing long hard-to-forget commands you can create aliases.

```text
git config --global alias.a "add ."
git config --global alias.c "commit"
```

You can now just type `git a` to add unstaged files.

Aliases can also be added directly to the config file.

```text
[alias]
    a = add .
    c = commit
```

