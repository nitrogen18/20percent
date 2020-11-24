---
title: Pod Install via No Internet
tags: Cocoapod
comments: false
---

What will happen if we ```pod install``` without an internet?. By adding parameter ```--verbose``` we can check on what happens inside the pod command. In verbose log, pod checks the pod cache library first if the pod library exists; If not, then it will search the pod library on the internet.

Steps:

* Add ```--verbose``` to ```pod update```
* Look for pod cache library path and change on its directory ```bash command: cd *path```

![alt text](/assets/img/podinstall/podinstall.png)

![alt text](/assets/img/podinstall/podinstall-part2.png)

* Print the availabe folders via ```ls```

![alt text](/assets/img/podinstall/pod-cache.png)

* These are the pod library cache available for offline use. This pod cache exist because of our past ```pod install``` in other project.

Note: If we have a lot of pod written in our Podfile and one of its pod didn't exist in our pod cache library. Then it will force to fetch via Internet, making the ```pod install``` fail.



<br>
<br>
<br>
