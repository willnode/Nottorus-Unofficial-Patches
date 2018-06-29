# [Nottorus](http://u3d.as/qVo) Unnoficial Patches

### [Read my post for preamble of what is going on](https://blog.wellosoft.net/en/nottorus-after-2-years.html)

Nottorus is a powerful plugin, first of its kind. Sadly the plugin author has walked away, and we're afraid of losing this masterpiece.

## About This Repo

This repo contains `patch.diff` which contains patches that made from original Nottorus source code.
See changes [in a table here](https://blog.wellosoft.net/en/nottorus-after-2-years.html#edit-post-mortem), additionaly [CHANGES.txt](CHANGES.txt) contains a copy of 	`git log` from patches repo that I maintained locally.

## Installing the Patch

1. Download the [patch](patch.diff) (or Clone this repo)
2. Extract `SourceCode.rar` in `Assets\Nottorus\src\SourceCode.rar` to `Assets\Nottorus\Editor`
3. Put the `patch.diff` in `Assets\Nottorus\Editor`
4. Open Unix Bash Shell in that `Editor` folder
5. Run `patch < patch.diff`

For Windows you can use WSL or Cygwin to run Unix bash Shell.

## Setup One-Click-Update-Via-Script

*(Requires [Git-SCM](https://git-scm.com/))*

If you want to keep listening for updates, patch steps above may require a tedious work. Here I figured an automated way to do this:

1. Extract `SourceCode.rar` in `Assets\Nottorus\src\SourceCode.rar` to `Assets\Nottorus\Editor`
2. Rename `Editor` to `.Editor` (Unity ignores any files/folder with a dot in beginning)
3. Open Bash/Git in folder `Assets\Nottorus\` and run `git clone https://github.com/willnode/Nottorus-Unnoficial-Patches .Patches`
4. In `Assets\Nottorus\` Folder, write this script to file:

Mac/Linux (`UpdatePatch.sh`)

```sh
cd .Patches
git pull origin master
cd ..
cp -R .Editor/ Editor/
cd Editor
patch -p1 < ../.Patches/patch.diff
exit
```

Windows (`UpdatePatch.bat`) (Requires [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10))

```bat
cd .Patches
git pull origin master
cd ..
xcopy /Y .Editor Editor
cd Editor
bash -c "patch -p1 < ../.Patches/patch.diff"
exit
```

Now if things are done correctly you can just double-click the script and it'll be automatically updated in instant.

## Why the .diff file??

The [original Nottorus](http://u3d.as/qVo) still alive in Asset Store, so I can't publish the source code it contained. However patches is mine, so I can give it away freely.

## Contributing

You can submit Issues here (Yep, including editor features). I'll figure the solution as helpful as I can.

If you want to contribute, here's a way to create the patch:

```sh
diff -x '*.meta' -uB .Editor Editor > .Patches/patch.diff
```

<!--

## Donation

[Link Here](https://paypal.me/WelloSoft)

I'm just one of many Nottorus Customer and I don't have any kind of relation with Nottorus author. I can't give 100% support but your donation can be a signal of how much importance of continuing Nottorus Development, so thank you.

-->
