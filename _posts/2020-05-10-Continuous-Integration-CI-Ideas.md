---
title: Simple Continuous Integration Ideas (CI)
tags: Tools
comments: false
---

Continuous Integration and Deployment (CI/CD) is a must in developing an app especially if we want to make our life easier. It automates our daily tasks in a sense of someone doing our repetitive actions instead of us. By integrating Continuous Integration/Deployment, there's a machine that acts as a bot and does certain acts. Some CI/CD Server provides steps for a developer to choose based on their ideal workflow. There were a lot of rules to be chosen and the most popular was the Unit Tests and Automatic Deployment which automatically archive and deploy the app in a certain App platform (Firebase/Appstore/Playstore) etc.

I've already tried the ```Continuous Deployment``` step which automatically deploys the ```.ipa``` (iOS Appstore Package) file to Firebase instead of doing manual steps. It's very helpful especially for the people who are doing a lot of multitasking.

Going back to CI/CD, these are my current configuration in our CI Server with integrated Unit/UI attached to the project. Also sharing this for my current workflow configurations and some simple ideas of CI.

**Bitrise CI/CD**

1. CHAIN-PRODUCTION-UnitUITest-Automated
2. CHAIN-STAGING-UnitUITest-Automated

The first trigger will start on CHAIN-PRODUCTION. At the end of the workflow, it triggers the next Workflow which is ```CHAIN-STAGING```

Workflow: **CHAIN-PRODUCTION**
* **Stack:** ```Xcode11.7.x, on macOS 10.15.6 (Catalina)```
* **Env var:** $BITRISE_GIT_BRANCH = **master**
- Before upgrading my Xcode to 12, my last setup was using XCode Version 11.7, so I change some configurations based on my last Xcode and macOS.
    - *Xcode 11.7 , macOS 10.x (Catalina)*

Workflow: **CHAIN-STAGING**
* **Stack:** ```Xcode 12.2.x on macOS 10.15.6 (Catalina)```
* **Env var:** $BITRISE_GIT_BRANCH = **develop (default)**
- Since my current Xcode is already version 12.x (Xcode12), I used this version to mockup up my current setup except for the OS. I've upgraded my OS to BigSur 12 already but the currently available stacks on Bitrise were Catalina, Mojave, and High Sierra which already have built-in Xcode Version.
    - *Xcode 12.2.x, macOS 10.x (Catalina)*

Note: I added Sample ENV Login in Xcode
Select ```Scheme > Test > Arguments > Environment Variables > Name Value```, then add your ENV Values

**Simple CI Ideas:**

**git push develop**
* trigger Unit/UI Tests
  - every push in Develop Branch, Unit/UI Test CI on Bitrise will trigger. The downside is when we're changing a simple part of the code, this idea will still trigger. For example, just adding a new line or space. This is very inconvenient to do a trigger for just changing a simple part of the code.

**git push with tag**
* trigger auto deployment to firebase or auto deployment to firebase with unit/ui tests
  - every tag included in push, the CI will trigger. There are very ideal CI steps for me since Bitrise CI will only trigger once it detects the tag on my git push. Meaning it will solve the first CI Idea which always triggers when push in the repo. Even if we push a lot on the remote repo, as long as it didn't include any tags, this CI idea will never trigger. The downside is when we have to specify the trigger based on the name of the tags, for example, staging and production, CI will still execute. These CI ideas can't identify particular tags because its primary definition is to ```trigger by tag```

**Specific Remote Branch for deployment**
  - This idea comes with my iOS head, he suggests that there's a specific branch for deployment or production, once a merge request is accepted or someone directly pushes on that branch, the Bitrise CI will trigger. For example Remote Branch:
    * master
    * develop
    * *firebase-deployment
  In this example, we add a specific remote branch for firebase named ```firebase-deployment```. Once we push on that remote branch, the Bitrise CD will archive and deploy the app to firebase. It solves the problem in ```git push with a tag``` since there's a specific remote branch for it. We can create two branches for Unit/UITest and Firebase-Deployment but it violates the Gitflow Concept if we have these branches living in our Remote Repository. I will discuss this Gitflow via iOS in the near future.

**Conclusion:** CI/CD is very beneficial for Mobile Developer since it makes their life easier, also for Enterprise Apps that include a lot of repetitive work. In my current CI Setup, doing daily CI seems unlogical to do instead of just wrap it Unit or UI test on ```Pull Request``` or ```push``` on the remote branch, but there were some benefits of integrating these steps.

**Benefits of Daily CI**
1. It ensures that the User can log in for the rest of the day given that the Unit/UI Test is performed before the starting of app usage, ex. 7:30 am.
2. It gives relief when you step aside from the project for a while. You just need to check Telegram for CI Unit/UI Test Result, and also you can monitor if the app still runs.

Overall, it helps to ensure the app will run daily. Ex. Login, Logout, Update some data on phone, etc. But in the end, it can be solved by doing a Unit Test via endpoints. Both were beneficial which are [Unit and UI Tests] as long as we cover to test the core or critical business logic of the app, we're good ✌🏻.



<br>
<br>
<br>
