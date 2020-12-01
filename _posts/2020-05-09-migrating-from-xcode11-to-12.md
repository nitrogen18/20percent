---
title: Migrating from Xcode 11 to 12
tags: Xcode
comments: false
---

When Apple introduced Big Sur with adapting their own built-in processor, which is the Apple M1 for their upcoming Macbook variants, my working project faced some problems regarding on migration from Xcode11 to Xcode12. It took me few days to figure out what happened and the reasons why the latest Xcode was failing.

![alt text](/assets/img/apple-m1.png)

Initial findings were firstly, Xcode12 supports the arm architecture that disabled way back old versions of Xcode. Xcode Simulator runs in x86_64 architecture Intel because the default processor used by Apple was Intel. Since they're shifting to arm, Xcode12 included the arm architecture in Simulator. When I shifted to Xcode12, it compiled to arm64 instead of x86_64 Intel. Xcode12 must detect that i'm using Intel processor and the project must compile in x86_64 architecture, but forces it to compile in arm64. While doing random stuff, I tried to create a new project using latest Xcode12 to check if the problem will come out with my fresh installed Xcode12 since it can't detect my current Macbook Intel, but the result was different from my project built in Xcode11. The new project can detect my current processor Intel and it compiled by using x86_47 which is right. This means that some of the projects built in Xcode11 may face some problem same as mine. Secondly, Xcode12 deprecate the VALID_ARCHS option in project build settings that can be seen in Xcode11 and shifts into ONLY_ACTIVE_ARCH (Build Active Architecture Only) for Xcode12. This might be another problem on why the project failed. Based on some information that I've read, Build Active Architecture Only is an option to choose what architecture will Xcode integrate in the project. It either automatically adapt what target architecture will be used or make it manual based on the Valid Architecture indicated in the Project Settings. I tried to use the yes option in Build Active Architecture Only but still there's an error popping out even when I set it to all of my schemes, so I tried the no option, and put the VALID_ARCHS manually. For my manual configuration, I only set two settings for VALID_ARCHS and one for Exclude Architecture.

```
Build Active Architecture = no

Excluded Architecture
Any iOS Simulator SDK = arm64

VALID_ARCHS
Any iOS Simulator SDK = x86_64
Any iOS SDK = arm64 armv7s armv7
```

The reasons why I exclude the ```arm64``` in Any iOS Simulator is that to force the Xcode to avoid compile it as an ```arm64``` because I'm not using ```Apple M1 chip```. To complete the ```VALID_ARCHS``` configuration, I include the ```x86_64``` too in the ```VALID_ARCHS``` for iOS Simulator which is ```x86_64```. For the the iOS SDK, I include all valid archs for iOS which are ```arm64 armv7s armv7```.

![alt text](/assets/img/upgrade-xcode/exclude.png)

![alt text](/assets/img/upgrade-xcode/valid.png)

The drawbacks of this configuration is that if someone build it using their Xcode12, it will fail since the default project settings were already modified specially using Xcode 11. It will conflict since the Xcode11 ```VALID_ARCHS``` shifts to ```ONLY_ACTIVE_ARCH``` for Xcode12. If someone needs to build this project, the first step would be doing a ```pod install``` or for totally clean pod build, execute the ```pod deintegrate``` first before proceeding to ```pod install```. After that if the user wants to shift to their current projects, they must do the ```pod deintegrate``` ```pod install``` to revert back their default pod build settings configuration.



<br>
<br>
<br>
