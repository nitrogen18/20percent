---
title: Simple Continuous Integration Ideas (CI)
tags: Tools
comments: false
---

Continuous Integration and Deployment (CI/CD) is a must in developing an apps specially if we want to make our life easier. It automates our daily task in a sense of someone doing our repetitive actions instead of doing it by us.  By integrating Continuous Integration/Deployment, there's a machine that acts as a BOT and do certain acts. There were a lot of rules to be chosen and the most popular were the Unit Tests and Automatic Deployment in Appstore.

I already tried the ```Continuous Deployment``` which automatically deploys ```.ipa``` file to Firebase instead of doing manual steps and wait for XCode's Archive long journey 😆.

These are my current configuration in our CI Server with integrated Unit/UI attached on my project. Also sharing my workflow configurations and some simple ideas of CI.

Bitrise CI/CD

Workflows
1. CHAIN-PRODUCTION-UnitUITest-Automated
2. CHAIN-STAGING-UnitUITest-Automated

First trigger will start on CHAIN-PRODUCTION, when this workflow succeed, at the end of workflow CHAIN-PRODUCTION steps theres a trigger for the next Workflow which is the CHAIN-STAGING

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
- Since my current Xcode is already at 12 (Xcode12), I use this version to mock with my current setup except the OS. I upgrade my OS to BigSur 12 already but currently available stack on bitrise were Catalina, Mojave and High Sierra with already builtin Xcode Version.
    - Xcode 12.2.x, macOS 10.x (Catalina)

Note: I added Sample ENV Login in Xcode
Steps:
Select Scheme > Test > Arguments > Environment Variables > Key Value(KV) Name Value
Values: ID test
USERNAME admin1
PASSWORD notAPassword
ESTA_NAME


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



![alt text](/assets/img/update-xcode/1.png)



![alt text](/assets/img/update-xcode/2.png)


<br>
<br>
<br>
