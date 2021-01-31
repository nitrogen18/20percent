---
title: things-to-do-when-cloning-other-swift-projects
tags: refactoring
comments: true
---

1. copying the UI via scene found in document outline
2. when paste in new project, make sure that the custom class is clear. probably in module theres value, just remove it.

NOTE:

copy pasting the screen from storyboard

1. copy from original project and paste it to new project
2. get the class of that original project and paste it too to new project
3. remove all connections from the new screen 
4. connect all iboutlets and ibactions from custom class to new screen
5. comment all content of all functions, note: inside the functions, not the full function.

When build and running the cloned project, make sure that you delete the git remote to avoid pushing to the real github repo

Next, is to change the production URL to staging from project to avoid accidentally do some .post