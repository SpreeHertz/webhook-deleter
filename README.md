# webhook-deleter

A simple Vue-based web application that simplifies the process of deleting Discord webhooks.

## Purpose

- You can prevent unknown @everyone webhook spams
- Most scams on discord get your information by sending some form of malicious media to the victim, grabbing the information from the webpage, and finally sending the victim's data via a webhook. You can obtain that webhook URL by going on your Developer Tools (record the Network requests), copy the webhook URL and you can delete it from here.

To the admin looking at the audit logs of the server that the webhook belongs to, it will look like this:
![image](https://github.com/user-attachments/assets/041ab250-cb91-4430-8f8c-83725ffec54a)


## Built with

- Vue 3 + Vite
- Vanilla CSS
