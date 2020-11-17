---
title: Add Telegram Notification on Bitrise
tags: Bitrise
comments: false
---

If you're using Bitrise and you always use Telegram, this workflow step will help you a lot by sending Bitrise Status build to your Telegram Account. Think about a trigger when you push to specific branch and do a Bitrise task on it. You need to check again to Bitrise Web in order to see the result of that task.

This step adds a flavor in your Bitrise Workflow, and better to put it at the end of all of your steps. It will send notification to your Telegram after finishing the Bitrise Task.

**Example:**
- push to develop branch
- Sit down or do some other task and wait for your phone to notify the build from Bitrise.

**Steps:**
- Choose any of your workflow to put the Telegram Notification to be included at the end of it.

![alt text](/assets/img/send-telegram-message-step.png)

- Click the + button at the end and search for *send telegram message*.

![alt text](/assets/img/input-variables-telegram-step.png)

**Note:**

There are four required input variables in this telegram step which are;
```
$TELEGRAM_BOT_TOKEN (SENSITIVE)
$TELEGRAM_CHAT_ID (SENSITIVE)
$DOWNLOAD_URL
$CUSTOM_MESSAGE
```
**ENV Details:**
```
TELEGRAM_BOT_TOKEN - Your Bot Token.

TELEGRAM_CHAT_ID - Your Telegram Account Chat ID.

DOWNLOAD_URL - Environment if you want to Download your archive.

CUSTOM_MESSAGE - Depending on what you want to show in telegram bot.
```

- After that, search for **BotFather** in Telegram search bar.
- For **$TELEGRAM_BOT_TOKEN** , you can follow my convo with him.

![alt text](/assets/img/godfather-convo.png)

- For **$TELEGRAM_CHAT_ID** , search for **@get_id_bot** in Telegram search bar.
```
/start
/my_id
```

<p align="center">
<img src="/assets/img/telegram-get-id.png" width="380" >
</p>
