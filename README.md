![](https://cdn.linuxct.info/Spotify/images/icon.png)

# Spotify Dogfood
> The Spotify Dogfood mod provides an ad-free Spotify experience on Android devices.

[![Build Status][travis-image]][travis-url] [![GitHub release][version-image]][version-url]

Welcome to the repo of the Spotify Dogfood mod. Here you'll find each release's patches divided by branches, as well as binaries in the Releases.

## Installation of a prebuilt version

* Remove previous installations of Spotify.
* Download the latest version from the [releases section](https://github.com/sergiocastell/spotify-dogfood/releases). 
* [Enable 'Unknown sources'](https://android.stackexchange.com/questions/77280/allow-unknown-sources-from-terminal-without-going-to-settings-app) under [Android Settings > Security](https://www.androidcentral.com/unknown-sources).
* Install just like any other APK via any File manager or, if you plan to use this app with an Android Auto car, [read this article](https://www.xda-developers.com/psa-spotify-and-other-apps-not-working-with-android-auto-heres-a-fix/).
* ???
* Profit!

## Development setup

To apply the patchsets manually, you need the following tools: 
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), and preferably [GitHub's app for Windows](https://desktop.github.com/).
* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and it's [environment variables properly set-up](https://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/)
* [APKtool](https://ibotpeaches.github.io/Apktool/)
* [An Android Keystore to sign your APKs](https://developer.android.com/studio/publish/app-signing.html#signing-manually)
* The version you wish to apply the patchset to, from [APKmirror](http://www.apkmirror.com/apk/spotify-ltd/spotify/).
* [Android Debugging Bridge](http://www.androidauthority.com/about-android-debug-bridge-adb-21510/) installed (perferably system-wide), as well as [it's drivers](https://adb.clockworkmod.com/) if you're on Windows.

Once you meet all of the above, it's as easy as it follows:

```
#unpack the apk
java -jar apktool_WhateverVersion.jar d NameOfTheApk.apk && cd NameOfTheApk
#now copy the patch file to the dir you're on
git apply --stat NameOfThePatch.path #checks the stats
git apply --check NameOfThePatch.path #sees if it's compatible with the environment
git apply NameOfThePatch.path #applies the patch
#compile the result
java -jar apktool_WhateverVersion.jar b NameOfTheDirectory
#sign with your key
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore /path/to/your/keystore NameOfTheDirectory/dist/NameOfTheResultingFile.apk YOURALIAS
#install the final apk
adb install -r NameOfTheDirectory/dist/NameOfTheResultingFile.apk
```
If you want to review the patch itself, you can use [git-am](https://stackoverflow.com/a/6948876).
If you want to review the mod to the liborbit-jni file, check the [wiki] page.

## Meta

LinuxCT – [@linuxct](https://twitter.com/linuxct) – Telegram Group [@spotifydogfood](https://t.me/spotifydogfood) – iamlinuxct@linuxct.info  
[Project webpage](https://cdn.linuxct.info/Spotify/) – [Project repo](https://github.com/spotify-dogfood) – [Updater for Spotify](https://github.com/spotify-dogfood/updater-for-spotify)

## Contributing

1. Fork it (<https://github.com/sergiocastell/spotify-dogfood/fork>)
2. Create your branch (`git checkout -b yourname/version`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin yourname/version`)
5. Create a new Pull Request

## Disclaimer

This repo, as well as the provided patches are just for demonstrative & educational purposes. They should not be used for illegal actions, and/or any action that can imply a violation in the ToS of the software used and mentioned in the repo. It is you, the final user, the one who takes the responsibility of using it wisely, as a functional PoC, and not for piracy or any other illegal actions.

<!-- Markdown link & img dfn's -->
[travis-image]: https://img.shields.io/circleci/project/github/badges/shields.svg?style=flat-square
[travis-url]: https://travis-ci.org
[wiki]: https://github.com/sergiocastell/spotify-dogfood/wiki/The-liborbit-jni-spotify.so-file
[version-image]: https://img.shields.io/github/release/sergiocastell/spotify-dogfood.svg?style=flat-square
[version-url]: https://github.com/sergiocastell/spotify-dogfood/releases/latest
