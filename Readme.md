# Lite-Weight Pi Agent

A lightweight personal AI assistant powered by **Google Gemma**, accessed through **OpenRouter**, and deployed on a **DigitalOcean Droplet**.

The assistant is accessible through **Telegram** and can interact with **Gmail, Google Calendar, and Google Drive** using natural-language instructions.

Built for the **Hacktoberfest Weekend Challenge 2026 – Build for a Friend**.

---

## What I Built

I built a lightweight personal AI assistant that runs continuously on a DigitalOcean Droplet and can be accessed from Telegram.

The assistant uses **Google's Gemma open-weight model** through **OpenRouter** for inference, **Pi** as the agent runtime, and **pi-gateway** to connect Telegram messages with persistent Pi sessions.

It can perform tasks such as summarizing emails, sending emails, reading and creating calendar events, browsing Google Drive, creating folders, and uploading files received through Telegram.

---

## How I Built It
This was actually inspired from the OpenAI's Dots & Meta's Muse
The project runs on an Ubuntu DigitalOcean Droplet.
Telegram acts as the user interface, allowing the assistant to be used directly from a phone without building a separate frontend.
pi-gateway receives Telegram messages and maps each conversation to a persistent Pi session using SQLite.
Pi acts as the agent runtime and sends requests to:
google/gemma-4-26b-a4b-it through OpenRouter.
For Google Workspace operations, Pi uses the gws CLI to interact with Gmail, Calendar, and Drive.
I also modified pi-gateway so Telegram documents and photos are downloaded to the local agent workspace and their paths are provided to the agent for further processing.

---

## Tasks that can be done
Read and summarize Gmail messages
Send emails
Read upcoming Google Calendar events
Create calendar events
Browse Google Drive
Create Drive folders
Upload documents and images from Telegram
Persistent Telegram conversations
Attachment support with follow-up instructions
