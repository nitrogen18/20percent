---
title: Migrating from Xcode 11 to 12
tags: Xcode
comments: false
---

When Apple introduces Big Sur with adapting their own built-in processor which is the Apple M1 for their upcoming Macbook variant, my working project faced some problems regarding on migration from Xcode11 to Xcode12. It took me few days to figure out of what happened and the reasons why it's failing in the latest Xcode.

Initial findings were first, Xcode12 supports the arm architecture that disabled way back old versions of Xcode. Xcode Simulator runs in **x86_64 architecture Intel** because the default processor used by Apple was **Intel**. Since they're shifting to arm, Xcode12 includes the arm architecture in Simulator. When I shift to Xcode12, it compiles to arm64 instead of x86_64 Intel. Xcode12 must detect that i'm using Intel processor and the project must compile in x86_64 architecture since I'm using Intel mac, but forces it to compile in arm64. While doing random stuffs, I tried to create a new project using latest Xcode12 to check if the problem comes out with my fresh installed Xcode12 since it can't detect my current Macbook Intel but the result was different from my project built in Xcode11. The new project can detect my current processor Intel and compiled by using x86_47 which is right. Meaning, some of the projects built in Xcode11 may face some problem same as me. Second, Xcode12 deprecate the VALID_ARCHS option in project build settings that can be seen in Xcode11 and shifts into ONLY_ACTIVE_ARCH (Build Active Architecture Only) for Xcode12. This might be another problem on why the project fails. Based on some info's that I've read, Build Active Architecture Only is an option to choose what architecture will Xcode integrate in the project, is either automatically adapt of what target architecture to be use or make it manual based on the Valid Architecture indicates in the Project Settings.

**WIP**


<br>
<br>
<br>
