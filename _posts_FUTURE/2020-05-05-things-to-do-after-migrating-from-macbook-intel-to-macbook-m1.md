---
title: Things to do after migrating from Macbook Intel to Macbook M1
tags: swift
comments: false
---

![alt text](/assets/img/changestoryboard.png)

1. Update the Macbook M1 first
2. Download Xcode on App Store
3. If your projects were using Cocoapods, this must be follow
- https://armen-mkrtchian.medium.com/run-cocoapods-on-apple-silicon-and-macos-big-sur-developer-transition-kit-b62acffc1387

If you run into an issue with running Cocoapods on Apple Developer Transition Kit, this easy fix worked for me.
Locate Terminal.app in Finder. (Applications->Terminal.app)
Right-click and choose Get Info
Check the “Open using Rosetta”
Quit all instances of Terminal app and run it again
Run sudo gem install ffi
Run pod install 🎉
