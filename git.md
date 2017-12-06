# Git

## Cloning

Start by cloning a repo from Github or Bitbucket.org.

```
git clone https://github.com/t4rzsan/icsharp.git
```

This will create a subfolder of the current folder name "aspnet-core-with-webpack" containing all the code.

## Submodules

### Cloning submodules

If the repo contains submodules, and you want to bring the code in the submodules down, you'll need to clone recursively.

```
git clone --recursive https://github.com/t4rzsan/icsharp.git
```

### Change submodule to own fork

If you have cloned a repo with a submodule and you want to change the submodule to a different fork \(if for example you have forked the submodul\), you need to edit the URL in the file .gitsubmodule.

```
[submodule "Engine"]
    path = Engine
    url = https://github.com/scriptcs/scriptcs.git
```

After saving .gitsubmodule, run the command.

```
git submodule sync
```

It seems that this may detach from HEAD, so a checkout may be necessary \(before making any local changes\).

```
git checkout
```

If you have trouble downloading the code for the submodule, try running the command:

```
git submodule update --remote
```

## Change default editor

To change the default editor for commit messages to Notepad++, open the file .gitconfig \(usually located under "c:\Users\\[user\]" on Windows\) and make sure it has a \[core\] section looking like this.

```
[core]
    editor = 'C:/put-your-folder-here/Notepad++/notepad++.exe' -multiInst -notabbar
```

From now on Notepad++ will open when ever you run git commit without the -m switch.

## Compare to remote

Start by fetching all from the remote repo:

```
git fetch origin
```

Then compare with local:

```
git log HEAD..origin/master --oneline
```

If you are happy with the results, you may merge the remote changes with the local repo:

```
git merge
```

## Delete branch

Delete the remote branch:

```
git push -d <remote_name> <branch_name>
```

For example:

```
git push -d origin my-feature-branch
```

You may also use:

```
git push <remote_name> :<branch_name>
```

Delete the local branch:

´\` 

```
git branch -d <branch_name>
```





