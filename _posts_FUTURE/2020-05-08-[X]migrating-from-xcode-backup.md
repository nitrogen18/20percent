---
title: Updating Xcode
tags: Tools
comments: true
---

Initial findings were firstly, Xcode12 supports the arm architecture that disabled way back old versions of Xcode. Xcode Simulator runs in ```x86_64 architecture Intel``` because the default processor used by Apple was ```Intel```. Since they're shifting to ```arm```, Xcode12 included the ```arm architecture``` in Simulator. When I shifted to Xcode12, it compiled to ```arm64``` instead of ```x86_64 Intel```. Xcode12 must detect that i'm using ```Intel processor``` and the project must compile in ```x86_64 architecture```, but forces it to compile in ```arm64```. While doing random stuff, I tried to create a new project using latest Xcode12 to check if the problem will come out with my fresh installed Xcode12 since it can't detect my current ```Macbook Intel```, but the result was different from my project built in Xcode11. The new project can detect my current processor ```Intel``` and it compiled by using ``x86_64`` which is right. This means that some of the projects built in Xcode11 may face some problem same as mine. Secondly, Xcode12 deprecate the ```VALID_ARCHS``` option in project build settings that can be seen in Xcode11 and shifts into ```ONLY_ACTIVE_ARCH``` (Build Active Architecture Only) for Xcode12. This might be another problem on why the project failed. Based on some information that I've read, ```Build Active Architecture Only``` is an option to choose what architecture will Xcode integrate in the project. It either automatically adapt what target architecture will be used or make it manual based on the Valid Architecture indicated in the Project Settings. I tried to use the yes option in ```Build Active Architecture Only``` but still there's an error popping out even when I set it to all of my schemes, so I tried the no option, and put the ```VALID_ARCHS``` manually. For my manual configuration, I only set two settings for ```VALID_ARCHS``` and one for ```Exclude Architecture```.


![alt text](/assets/img/update-xcode/1.png)



![alt text](/assets/img/update-xcode/2.png)


<br>
<br>
<br>
