# webhook-deleter

A simple Vue-based web application that simplifies the process of deleting Discord webhooks.

## Purpose

- You can prevent unknown @everyone webhook spams
- Most scams on discord get your information by sending some form of malicious media to the victim, grabbing the information from the webpage, and finally sending the victim's data via a webhook. You can obtain that webhook URL by going on your Developer Tools (record the Network requests), copy the webhook URL and you can delete it from here.

To the admin looking at the audit logs of the server that the webhook belongs to, it will look like this:
![unknown-user-deleted-webhook](https://media.discordapp.net/attachments/718700239212773386/1295028895682134080/image.png?ex=670d2925&is=670bd7a5&hm=82f74bde886453dee1dbc28a1162781b16fdcdf0a5a9fc153692f325494d410b&=&format=webp&quality=lossless)

## Built with

- Vue 3 + Vite
- Vanilla CSS
