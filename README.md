# Unity CI/CD

## UBuilder

[![GH Pages](https://img.shields.io/badge/GitHub-IvanMurzak/UBuilder-blue?logo=github&logoColor=white)](https://github.com/IvanMurzak/UBuilder)

Place the `UBuilder` under the `Assets/Editor` folder.

## Build script

[![OS - macOS](https://img.shields.io/badge/OS-macOS-blue?logo=apple&logoColor=white)](https://www.apple.com/macos/ "Go to Apple homepage")
![Generic badge](https://img.shields.io/badge/Unity-2022.3.31f1-black.svg?logo=unity&logoColor=FFFFFF)

### Unity Editor command line arguments

[![Documentation](https://img.shields.io/badge/Documentation-818589?style=for-the-badge&logo=unity&logoColor=white)](https://docs.unity3d.com/Manual/EditorCommandLineArguments.html)

### Android

`build-android.sh` :

```shell
#!/bin/zsh

UnityEditor=/Applications/Unity/Hub/Editor/2022.3.31f1/Unity.app/Contents/MacOS/Unity

# Android related variables
export android_BUILD_APP_BUNDLE=false
export android_KEYSTORE_PATH=***************
export android_KEYSTORE_PASSWORD=***************
export android_KEYALIAS_NAME=***************
export android_KEYALIAS_PASSWORD=***************

"$UnityEditor" \
-projectPath *************** \
-logFile build-android.log \
-executeMethod UBuilder.CommandAndroid.Build \
-quit \
-accept-apiupdate \
-batchmode \
-nographics
```

```shell
$ ./build-android.sh &
$ tail -f build-android.log
```

### iOS

`build-ios.sh` :

```shell
#!/bin/zsh

UnityEditor=/Applications/Unity/Hub/Editor/2022.3.31f1/Unity.app/Contents/MacOS/Unity

"$UnityEditor" \
-projectPath *************** \
-logFile build-ios.log \
-executeMethod UBuilder.CommandiOS.Build  \
-quit \
-accept-apiupdate \
-batchmode \
-nographics
```

```shell
$ ./build-ios.sh &
$ tail -f build-ios.log
```

#### Generating an iOS Apple Store Package (IPA) : [`🔗`](ios.md)

## Build output

### Build output directory

| Platform | Directory |
| -- | -- |
| [Android](UBuilder/Command.Android.cs#L70) | `Builds/Android/buildDefault.apk[/aab]` |
| [iOS](UBuilder/Command.iOS.cs#L41) | `Builds/iOS/buildDefault` |

### Change the build output directory

```shell
# Global variables
export output=***************
```
