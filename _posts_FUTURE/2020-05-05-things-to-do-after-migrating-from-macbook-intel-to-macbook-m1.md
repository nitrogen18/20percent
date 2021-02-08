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

For Archiving the Production Build of Project, you need the private key and distribution certificate
- for easy export, just look for the source macbook > keychain > system or login, preferred to system > ^Keychain access tabs, look for My Certificates, and look for the right Apple Distribution Certificate and expand it, it includes the private key of the creator of that Apple Distribution Certificate. Import those two and add password, the expected filename is .p12, then you can just use Air drop and navigate to destination macbook and open that .p12. after opening it, put the password of .p12 and this is not finished yet, go to destination macbook keychain and navigate to System Keychains/System, copy the Apple Distribution that uploaded earlier and paste it also to default keychains/login:

NOTE: remove asap the file .p12 after uploading it to your keychain

What are the indications if I uploaded the right private key and distribution certificate
- the indication for me is that, if you validate your app then you have pods, cocoapods. The xcode will request alot of Macbook Username and Password for pod permision.