---
title: Firebase Uploading dSYM Manually
tags: Crashlytics
comments: false
---

I have this problem in my **Production Scheme** when someone user crashes their app and
the dSYM's were not uploaded in our Firebase. It seems that it needs a lot of work to do in order to upload the dYSM's.
Based on the guidelines provided by Firebase, there are two ways to upload the dYSM's. The first is to include script before build the iOS Projects and the second is to do it manually. What I did is to do it manually by doing some minimal bash commands.

These are my most used **BASH** commands.
```
ls
ls -l
cd *folder name
cd ~
cd ..
```

For the steps:
- First, navigate to Appstore Connect and choose your app
- Go to Activity Tab > Latest Version > Include Symbol > download dSYM
- Put it on Desktop for easy reference
- Go here [https://firebase.google.com/docs/crashlytics/get-deobfuscated-reports?platform=ios](https://firebase.google.com/docs/crashlytics/get-deobfuscated-reports?platform=ios)
- Check **Upload your dSYM Topic**

These are the Placeholders
dSYM_directory = the dSYM zip that you've downloaded in appstoreconnect
$PODS_ROOT/FirebaseCrashlytics/upload-symbols = the firebase upload-symbols in the current project
- You can get this by creating a script in Build Phases and add script "echo $PODS_ROOT/FirebaseCrashlytics/upload-symbols"
- After building, navigate to Report Navigator in the left of xcode and click the first hammer icon. Scroll down at the bottom and you will find the current directory of $PODS_ROOT
- /path/to/GoogleService-Info.plist = you can also get the path of this using the steps above
platform = ios

##### NOTE: Login in firebase cli first before executing this script

```
# BASH
# First time install firebase on MacOS Terminal? use this
curl -sL https://firebase.tools | bash

# Start

firebase login
firebase projects:list # To check the projects, for verification
```

First Script:

```
find dSYM_directory -name "*.dSYM" | xargs -I \{\} $PODS_ROOT/FirebaseCrashlytics/upload-symbols -gsp /path/to/GoogleService-Info.plist -p platform \{\}
```

Second Script:

```
/path/to/pods/directory/FirebaseCrashlytics/upload-symbols -gsp /path/to/GoogleService-Info.plist -p ios /path/to/dSYMs
```

![alt text](/assets/img/crashlytics-upload.png)

I used the second script and shows success on my Terminal but the Firebase still reflects the warning. Maybe it works or maybe not.

Note: "upload-symbols" can't be opened because Apple cannot check it for malicious software.
[https://technuisance.com/crashlytics/upload-symbols-cant-be-opened-because-apple-cannot-check-it-for-malicious-software.html](https://technuisance.com/crashlytics/upload-symbols-cant-be-opened-because-apple-cannot-check-it-for-malicious-software.html)
Allow it via System Preferences > Security & Privacy > Click Allow

<br>
PS: It works! If we manually upload the dSYM before this image below occurs, the error alert will still remain, but the following errors will not produce an error alert anymore and the future errors will be preceded, and process by the Firebase/Crashlytics.
![alt text](/assets/img/dsym-error.png)

Better to have a script when we archive the project that automatically uploads the dSYM into Crashlytics. Possible solutions would be putting a script in Xcode after building the Production, or automate it via CI/CD Bitrise.
<br>
<br>
<br>
