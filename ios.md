<img src="./images/ios_logo.svg" width=120>


# Unity iOS

[![Documentation](https://img.shields.io/badge/Documentation-818589?style=for-the-badge&logo=unity&logoColor=white)](https://docs.unity3d.com/Manual/iphone.html)

# xcodebuild

```
{BUILD OUTPUT DIR}
   ├── Unity-iPhone.xcworkspace
   ├── Unity-iPhone.xcarchive
   ├── exportOptions.plist
   ├── {Product Name}.ipa
```

## Generate xcarchive from xcodeworkspace

```shell
xcodebuild \
-workspace Unity-iPhone.xcworkspace \
-scheme Unity-iPhone \
-configuration Release \
-sdk iphoneos \
IPHONEOS_DEPLOYMENT_TARGET=12.0 \
CODE_SIGN_IDENTITY="Apple Development: Po Keum Cho (**********)" \
PROVISIONING_PROFILE_APP="********-****-****-****-************" \
-archivePath $PWD/Unity-iPhone.xcarchive \
clean archive
```

> [!NOTE]  
> [![Documentation](https://img.shields.io/badge/Documentation-Build_an_iOS_application-818589?style=for-the-badge&logo=unity&logoColor=white)](https://docs.unity3d.com/Manual/iphone-BuildProcess.html)
>
> When building with xcodebuild, use suffixed versions for the following build settings:
> | Xcode build setting	 | Suffixed version |
> | -- | -- |
> | PRODUCT_NAME | PRODUCT_NAME_APP |
> | PROVISIONING_PROFILE | PROVISIONING_PROFILE_APP |
> | PROVISIONING_PROFILE_SPECIFIER | PROVISIONING_PROFILE_SPECIFIER_APP |
> | OTHER_LDFLAGS | OTHER_LDFLAGS_FRAMEWORK |

## Convert xcarchive to ipa

#### exportOptions.plist

> [!TIP]
> 1. Execute the `xcodebuild -h` command.
> 2. In the output, it says `Available keys for -exportOptionsPlist:` and goes on to describe what is available as keys for `exportOptions.plist`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>method</key>
    <string>debugging</string>
    <key>teamID</key>
    <string>{TEAM ID}</string>
    <key>provisioningProfiles</key>
    <dict>
      <key>{Bundle ID}</key>
      <string>{PROVISIONING PROFILE NAME}</string>
    </dict>
  </dict>
</plist>
```

#### Execute command

```shell
xcodebuild \
-exportArchive \
-archivePath $PWD/Unity-iPhone.xcarchive \
-exportOptionsPlist $PWD/exportOptions.plist \
-exportPath $PWD
```

<details>
<summary>⚙️ <i>automatic signing</i></summary><br/>

`exportOptions.plist` :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>method</key>
    <string>debugging</string>
    <key>signingStyle</key>
    <string>automatic</string>
  </dict>
</plist>
```

Execute command :

```shell
xcodebuild \
-exportArchive \
-archivePath $PWD/Unity-iPhone.xcarchive \
-exportOptionsPlist $PWD/exportOptions.plist \
-exportPath $PWD \
-allowProvisioningUpdates
```

</details>

