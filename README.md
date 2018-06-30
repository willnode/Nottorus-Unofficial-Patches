# [Nottorus](http://u3d.as/qVo) Unofficial Patches

### [Read my post for preamble about what is going on](https://blog.wellosoft.net/en/nottorus-after-2-years.html)

Nottorus is a powerful plugin, first of its kind. Sadly the plugin author has walked away, and we're afraid of losing this masterpiece.

## About This Repo

This repo contains `patch.diff` which contains patches that made from original Nottorus source code.
See changes [in a table here](https://blog.wellosoft.net/en/nottorus-after-2-years.html#edit-post-mortem), additionaly [CHANGES.txt](CHANGES.txt) contains a copy of 	`git log` from patches repo that I maintained locally.

## Installing the Patch

*(Requires [Git-SCM](https://git-scm.com/))*

0. Extract Nottorus v2.0 into your project
1. Extract `SourceCode.rar` in `Assets\Nottorus\src\SourceCode.rar` to `Assets\Nottorus\` (There should be `Editor` folder after extraction)
2. Rename `Editor` to `.Editor` (Unity ignores any files/folder with a dot in beginning)
3. Normalize Ending: Save [this script (use normalize-lf)](https://gist.github.com/willnode/a6e76fcb9ac5d150df4a356b818a0ffe) to `.Editor` folder and run it, then delete the script.
3. Delete `Nottorus_Plugin.dll` and `Addon_CSP.dll` from `Plugins`
4. Open Bash/Git Bash in folder `Assets\Nottorus\` and run `git clone https://github.com/willnode/Nottorus-Unofficial-Patches .Patches` (There should be `.Patches` folder after cloning)
5. In `Assets\Nottorus\` Folder, write this script to file:

Mac/Linux (`UpdatePatch.sh`) (also Windows with Git-SCM's Bash Mingw)

```sh
cd .Patches
git pull origin master
cd ..
cp -R .Editor/ Editor/
cd Editor
patch --binary -p1 < ../.Patches/patch.diff
exit
```

Windows (`UpdatePatch.bat`) using [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

```bat
cd .Patches
REM git pull origin master
cd ..
del /S /Q /F Editor>nul
xcopy /I /E /Y .Editor Editor>nul
cd Editor
bash -c "patch --binary -p1 < ../.Patches/patch.diff"
cd ..
```

Now if things are done correctly you can just double-click the script and it'll be automatically updated in instant.

## Why the .diff file??

The [original Nottorus](http://u3d.as/qVo) still alive in Asset Store, so I can't publish the source code it contained. However patches is mine, so I can give it away freely.

## Technical Limitation (Windows only)

Windows uses CRLF ending, however I found that `patch` is broken whenever I try to push CRLF during patching session, so at the end all Nottorus script is patched with Unix (LF) ending. If you want to modify Nottorus scripts, I advise you to renormalize it back to CRLF (otherwise, don't :smile: )

## Contributing

You can submit Issues here (Yes, including editor features). I'll figure the solution as helpful as I can.

If you have problem with installation, please check existing issues first before starting new one.

If you want to contribute, here's how I create the patch:

```sh
diff -x '*.meta' -ur --strip-trailing-cr .Editor Editor > .Patches/patch.diff
```

<!--

## Donation

[Link Here](https://paypal.me/WelloSoft)

I'm just one of many Nottorus Customer and I don't have any kind of relation with Nottorus author. I can't give 100% support but your donation can be a signal of how much importance of continuing Nottorus Development, so thank you.

-->
