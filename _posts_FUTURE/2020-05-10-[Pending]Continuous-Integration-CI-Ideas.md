---
title: Simple Continuous Integration Ideas (CI)
tags: Tools
comments: false
---

Continuous Integration and Deployment (CI/CD) is a must in developing an apps specially if we want to make our life easier. It automates our daily task in a sense of someone doing our repetitive actions instead of us.  By integrating Continuous Integration/Deployment, there's a machine that acts as a bot and do certain acts. Some CI/CD Server provides steps for developer to choose based on their ideal workflow. There were a lot of rules to be chosen and the most popular are Unit Tests and Automatic Deployment which automatically archive and deploys the app in a certain App platform (Firebase/Appstore/Playstore).

I've already tried ```Continuous Deployment```step which automatically deploys ```.ipa``` (iOS Appstore Package) file to Firebase instead of doing manual steps. It's very helpful specially for Enterprise App Projects.

Going back to CI/CD, these are my current configuration in our CI Server with integrated Unit/UI attached on project. Also sharing this for my current workflow configurations and some simple ideas of CI.

Bitrise CI/CD

Workflows
1. CHAIN-PRODUCTION-UnitUITest-Automated
2. CHAIN-STAGING-UnitUITest-Automated

First trigger will starts on CHAIN-PRODUCTION. At the end of workflow, it triggers the next Workflow which is ```CHAIN-STAGING```

Configurations:
Workflow: CHAIN-PRODUCTION
* Stack: Xcode11.7.x, on macOS 10.15.6 (Catalina)
* Env var: $BITRISE_GIT_BRANCH = master
Info:
- Before upgrading my Xcode to 12, my last setups were “”, so i change some configuration based on the last workflow setup.
    - Xcode 11.7 , macOS 10.x (Catalina)

Workflow: CHAIN-STAGING
* Stack: Xcode 12.2.x on macOS 10.15.6 (Catalina)
* Env var: $BITRISE_GIT_BRANCH = develop (default)
Info:
- Since my current Xcode is already version 12.x (Xcode12), I used this version to mock up with my current setup except the OS. I've upgraded my OS to BigSur 12 already but the currently available stacks on Bitrise were Catalina, Mojave and High Sierra which already have builtin Xcode Version.
    - Xcode 12.2.x, macOS 10.x (Catalina)

Note: I added Sample ENV Login in Xcode
Steps:
Select Scheme > Test > Arguments > Environment Variables > Name Value

Simple CI Ideas:

git push develop
* trigger Unit/UI Tests
  - every push in Develop Branch, Unit/UI Test CI on Bitrise will trigger. The downside is when we just change simple part of the code, for example, just adding a newline or space, this trigger will still execute.

git push with tag
* trigger auto deployment to firebase or auto deployment to firebase with unit/ui tests
  - every tag included in push, the CI will trigger. This is very ideal CI steps for me since Bitrise CI will trigger only once it detects tag included in push. Meaning it will solve the ```CI Trigger every push step```. Even if we push a lot, as long as it didn't include tags, the CI will never trigger. The downside is when we have specific tags for staging and production, CI cant specify those tags and execute as long as there's included tag on git push.

Specific Remote Branch for deployment
  - This idea comes with my iOS head, he suggest that there's specific branch for  deployment, once merge request accepted and put it on that remote branch, or someone directly push on that branch, the Bitrise CI will trigger. For example
  Remote Branch:
    * master
    * develop
    * *firebase-deployment
  In this example, we add new specific remote branch for firebase. Once we push on that remote branch, the Bitrise CD will archive and deploy the app to firebase. It solves ```git push with tag``` since theres specific remote branch for it. We can create two branch for Unit/UITest and for Firebase-Deployment.

  ++++

Conclusion: Doing daily CI seems unlogical to do instead just wrap it Unit or UI test on ```Pull Request``` or ```push``` on remote branch, but there were some benefits of integrating this steps. First is that it helps to ensure the app will run on a daily basis. The app must enable to login, logout, perform actions, etc. but this can be solve using Unit Test via endpoints.


 The first impression is after we pull or push, there were new changes pushed in the repo and the projection is that the preceding test would be no value at all since theres no changes and just repeating the CI stuffs. But how about the other dependency provider? The latest OS installed? does it still run if someone updates their iOS phone to latest and some of 3rd party dependency library affected by the update.

For me, benefits of Daily CI
1. It ensures that the User can login for the rest of the day given that the Unit/UI Test perform Before starting the average time the user will use the App.
2. Gives relief when you stay aside the project for a while with integrated CI. You just need to check Telegram for CI Unit/UI Test Result and you can monitor if the app still run.






=======================================================================================================================================

Telegram:
Jonorsky Navarrete, [Oct 12, 2020 at 11:51:43 AM (Oct 12, 2020 at 11:52:09 AM)]:
ini si mga workflow ko si, iba test lng RND-, ining may prefix na PROD- si inut si pagdeploy sa firebase tas si ikaduwa si unit/ui na may telegram notif. pwede magpili kung anung workflow.

pwedeng ang pattern

git push develop
* trigger Unit/UI Tests
  - every push sa develop branch matrigger si Unit/Ui Test sa bitrise pero kung makaskas mag commit tas push maqqueue si mga task sa bitrise.

git push with tag
* trigger auto deployment to firebase or auto deployment to firebase with unit/ui tests
  - since ang pagdeploy to firebase nagdedepende sa tag. example review30. pag push ning develop branch pa gitlab na may tag na kaiba, matrigger si bitrise ning unit/ui test + deploy to firebase duman sa develop branch ta may kaiba tag. pero kung ang pagpush sa develop branch mayong kaibang tag, ang ma trigger lang ining inut na trigger, si unit/ui lng.

or arug kang sinabi ni heli na dedicated branch.
* branch for deploying to firebase
  - bale mayo pa trigger sa develop branch, tas commit commit, pag okay na ang develop branch, ipupush na or merge si develop branch dun sa dedicated branch na pang deploy to bitrise, pagkamerge matrigger si bitrise na may nadetect na changes sa dedicated branch tas marun si bitrise workflow na may unit/ui + deploy to firebase.


  Since kaiba naman ang Linter (Swiftlint) for Swift Language conform

=======================================================================================================================================

![alt text](/assets/img/update-xcode/1.png)



![alt text](/assets/img/update-xcode/2.png)


<br>
<br>
<br>
