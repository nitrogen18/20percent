---
title: Stuck at Unit Test via MVC
tags: Architecture
comments: true
---

Hello, Good day! gonna share my thoughts about this Unit Test topic. I feel there's somethings wrong, so I look up and explore
about it. Looking back of what i'm pointing, I tried to do Unit Test since theres something benefits of creating
this test, it makes the code more reliable and bug free since we can do click Unit Test after doing some changes in codebase.
But then I have this struggle on how do I unit test my Modules which are UIViewControllers. I can't test them since some of my
function and logics were tightly coupled. It means that in one function there were two or more business logic.

**Unit Test** via testable import need a return function in order to test it but since my functions were already coupled, I need to
decompose/breaks them into a smaller pieces which I have my own trust issues. I feel there something strange bug will pop out
elsewhere since I will move some of the business logic from my codebase. So what I did is **UI Test**, its an actual test on a simulator of physical device, It's somehow resembles in Selenium which automates the action on simulator. We can just click record and do some clicks on simulator, then XCode will provide the action code. That's the one of alternative of testing my codebase since I have this trust
issues on breaking them down into smaller pieces/functions.

Meanwhile, while reading some stuffs on the internet. I found this feedback which I relate of what he said.

![alt text](/assets/img/someone.png)

In his case, he had this PhotoListViewController with a lot of business logic like converting date, start/stop activity indicator,
showing/hiding table view, also with a dependency API Service. He points out its too complicated since there were different kind of
presentation logic in one file which resembles in my case(MVC), thats why the MVC is also called as **Massive View Controller**.

Based on my readings there were good solution for this; is to implement a Software Architecture Pattern that implements **Presentation/Domain Layer** which all business process will be put in here. There are some of Software Architecture Pattern that implements it, the **MVP** and **MVVC** are widely know for this that has the **Separation of Concern** to other layer which gives benefit to implement an extensive **Unit Test** for every Data/UI component.

<br>
<br>
<br>
