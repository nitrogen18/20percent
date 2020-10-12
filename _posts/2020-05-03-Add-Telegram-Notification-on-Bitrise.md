---
title: Add Telegram Notification on Bitrise
tags: Bitrise
comments: false
---

If you're using Bitrise and you always use Telegram, this workflow step will help you a lot by sending Bitrise Status build to your Telegram Account. Think about a trigger when you push to specific branch and do a Bitrise task on it. You need to check again to Bitrise Web in order to see the result of that task.

This step adds a flavor in your Bitrise Workflow, and better to put it at the end of all of your steps. It will send notification to your Telegram after finishing the Bitrise Task.

Example:
- push to develop branch
- Sit down or do some other task and wait for your phone to notify the build from Bitrise.
