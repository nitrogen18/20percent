---
title: Simple Continuous Integration Ideas (CI)
tags: Tools
comments: false
---

Continuous Integration and Deployment (CI/CD) is a must in developing an apps specially if we want to make our life easier. It automates our daily task in a sense of someone doing our repetitive actions instead of us. By integrating Continuous Integration/Deployment, there's a machine that acts as a bot and do certain acts. Some CI/CD Server provides steps for developer to choose based on their ideal workflow. There were a lot of rules to be chosen and the most popular were the Unit Tests and Automatic Deployment which automatically archive and deploy the app in a certain App platform (Firebase/Appstore/Playstore) etc.

I've already tried ```Continuous Deployment``` step which automatically deploys ```.ipa``` (iOS Appstore Package) file to Firebase instead of doing manual steps. It's very helpful specially for the people who are doing a lot of multitasking.

Going back to CI/CD, these are my current configuration in our CI Server with integrated Unit/UI attached on project. Also sharing this for my current workflow configurations and some simple ideas of CI.

**Bitrise CI/CD**

1. CHAIN-PRODUCTION-UnitUITest-Automated
2. CHAIN-STAGING-UnitUITest-Automated

First trigger will starts on CHAIN-PRODUCTION. At the end of workflow, it triggers the next Workflow which is ```CHAIN-STAGING```

Workflow: **CHAIN-PRODUCTION**
* **Stack:** ```Xcode11.7.x, on macOS 10.15.6 (Catalina)```
* **Env var:** $BITRISE_GIT_BRANCH = **master**
- Before upgrading my Xcode to 12, my last setup was using XCode Version 11.7, so i change some configuration based on my last Xcode and MacOS.
    - *Xcode 11.7 , macOS 10.x (Catalina)*

Workflow: **CHAIN-STAGING**
* **Stack:** ```Xcode 12.2.x on macOS 10.15.6 (Catalina)```
* **Env var:** $BITRISE_GIT_BRANCH = **develop (default)**
- Since my current Xcode is already version 12.x (Xcode12), I used this version to mock up with my current setup except the OS. I've upgraded my OS to BigSur 12 already but the currently available stacks on Bitrise were Catalina, Mojave and High Sierra which already have builtin Xcode Version.
    - *Xcode 12.2.x, macOS 10.x (Catalina)*

Note: I added Sample ENV Login in Xcode
Select ```Scheme > Test > Arguments > Environment Variables > Name Value```, then add your ENV Values

**Simple CI Ideas:**

**git push develop**
* trigger Unit/UI Tests
  - every push in Develop Branch, Unit/UI Test CI on Bitrise will trigger. The downside is when we're changing simple part of the code, this idea will still trigger. For example, just adding a newline or space. This is very inconvenient to do a trigger for just changing a simple part of the code.

**git push with tag**
* trigger auto deployment to firebase or auto deployment to firebase with unit/ui tests
  - every tag included in push, the CI will trigger. This is very ideal CI steps for me since Bitrise CI will only trigger once it detects tag on my git push. Meaning it will solve the first CI Idea which always trigger when push in the repo. Even if we push a lot on the remote repo, as long as it didn't include any tags, this CI idea will never trigger. The downside is when we have to specify the trigger based on the name of the tags, for example staging and production, CI will still executes. This CI ideas can't identify particular tags because it's primary definition is to ```trigger by tag````

**Specific Remote Branch for deployment**
  - This idea comes with my iOS head, he suggest that there's specific branch for deployment or production, once merge request accepted or someone directly push on that branch, the Bitrise CI will trigger. For example
  Remote Branch:
    * master
    * develop
    * *firebase-deployment
  In this example, we add specific remote branch for firebase named ```firebase-deployment```. Once we push on that remote branch, the Bitrise CD will archive and deploy the app to firebase. It solves the problem in ```git push with tag``` since theres specific remote branch for it. We can create two branch for Unit/UITest and for Firebase-Deployment but it violates the **Gitflow Concept** if we have this branches living in our Remote Repository. I will discuss this Gitflow via iOS in the near future.

**Conclusion:** CI/CD is very beneficial for Mobile Developer since it makes their life more easier, also for Enterprise Apps that include a lot of repetitive work. In my current CI Setup, doing daily CI seems unlogical to do instead just wrap it Unit or UI test on ```Pull Request``` or ```push``` on remote branch, but there were some benefits of integrating this steps.

**Benefits of Daily CI**
1. It ensures that the User can login for the rest of the day given that the Unit/UI Test performed before the starting of app usage, ex. 7:30am.
2. It gives relief when you step aside the project for a while. You just need to check Telegram for CI Unit/UI Test Result, and also you can monitor if the app still run.

Overall, it helps to ensure the app will run on a daily basis. Ex. Login, Logout, Update some data in phone, etc. But in the end, it can be solve by doing Unit Test via endpoints. Both were beneficial which are [Unit and UI Tests] as long us we cover to test the core or critical business logic of the app, we're good ✌🏻.



<br>
<br>
<br>
