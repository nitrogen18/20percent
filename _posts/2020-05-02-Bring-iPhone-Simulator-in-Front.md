---
title: Bring iPhone Simulator in Front
tags: Simulator
comments: false
---

When I do some *build and run* via Xcode, sometimes the **Simulator** stuck at the back of IDE and it needs to be click manually in order to show. In this script, it will bring the simulator in front every time we build and run our project. Very convenient for Simulator Users like me. 😉

Steps: **Xcode > Project > Build Phases > Targets > New Run**

![alt text](/assets/img/bring-to-front.jpg "Logo Title Text 1")

```
tell application "iPhone Simulator"
activate
end tell
```

<br>
<br>
