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



