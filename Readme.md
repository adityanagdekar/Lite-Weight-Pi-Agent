# Lite-Weight Pi Agent

A lightweight, always-on personal AI assistant powered by **Google Gemma**, accessed through **OpenRouter**, and deployed on a **DigitalOcean Droplet**.

The assistant is accessible directly through **Telegram** and can interact with **Gmail, Google Calendar, and Google Drive** using natural-language instructions.

Built for the **Hacktoberfest Weekend Challenge 2026 – Build for a Friend**.

---

## What I Built

I built a lightweight personal AI assistant that runs continuously on a DigitalOcean Droplet and can be accessed directly from Telegram.

At its core, the assistant uses Google's **Gemma open-weight model** through **OpenRouter** for inference. **Pi** acts as the agent runtime, while **pi-gateway** connects Telegram conversations to persistent Pi sessions.

Instead of switching between Gmail, Calendar, Drive, and an AI assistant, I can simply message the bot with requests such as:

> "Summarize my unread emails."

> "Schedule a DSA practice session tomorrow evening."

> "Send this document to my Google Drive."

The assistant determines the required action and uses Google Workspace tools to execute it.

---

## How I Built It

The idea was inspired by the concept of persistent personal AI agents such as **OpenAI's Dots** and **Meta's Muse** — assistants that are continuously available and capable of interacting with the tools people already use.

The project runs on an **Ubuntu DigitalOcean Droplet**, which keeps the agent available continuously without requiring my laptop to stay online.

**Telegram** serves as the user interface, eliminating the need to build a separate frontend application.

Incoming Telegram messages are handled by **pi-gateway**, which maps conversations to persistent **Pi** sessions using **SQLite**.

Pi acts as the agent runtime and sends requests to the following Gemma model through OpenRouter:

```text
google/gemma-4-26b-a4b-it
```

For Google Workspace operations, the agent uses the open-source **Google Workspace CLI (`gws`)** to interact with:

- Gmail
- Google Calendar
- Google Drive

I also extended `pi-gateway` to support Telegram documents and images. Attachments are downloaded to the agent's local workspace and their file paths are passed to Pi, allowing the assistant to perform actions on files received directly through Telegram.

---

## Architecture

```text
                    Telegram
                        |
                        v
                  pi-gateway
                        |
                        v
                       Pi
                  Agent Runtime
                    /       \
                   /         \
                  v           v
            OpenRouter     Google Workspace CLI
                |             |
                v       -------------------
             Gemma       |       |       |
                       Gmail  Calendar  Drive
```

The agent runtime, Telegram gateway, session storage, workspace, and Google Workspace tooling run on **DigitalOcean**, while Gemma inference is provided through **OpenRouter**.

---

## What Can the Agent Do?

The assistant currently supports:

- Read and summarize Gmail messages
- Triage emails
- Send emails
- Read upcoming Google Calendar events
- Create calendar events
- Browse Google Drive
- Create Google Drive folders
- Upload documents and images received through Telegram
- Maintain persistent Telegram conversations
- Handle attachments with instructions
- Handle attachments followed by instructions in a separate message

For example:

```text
User:
[uploads resume.pdf]

Bot:
Received resume.pdf. Tell me what you want me to do with it.

User:
Upload this to my Google Drive.

Agent:
Uploads the document using Google Drive tooling.
```

---

## Tech Stack

| Component | Purpose |
|---|---|
| **Google Gemma** | Open-weight language model |
| **OpenRouter** | Hosted Gemma inference |
| **Pi** | Agent runtime and tool execution |
| **pi-gateway** | Telegram-to-Pi communication |
| **Telegram Bot API** | User interface |
| **Google Workspace CLI** | Gmail, Calendar, and Drive integration |
| **SQLite** | Persistent Telegram-to-Pi session mapping |
| **DigitalOcean** | Always-on agent infrastructure |
| **Python** | Gateway customization |

---

## Open Innovation

This project combines an **open-weight AI model** with **open-source agent tooling** to build a practical personal assistant.

Gemma provides the intelligence layer, while Pi, pi-gateway, and Google Workspace CLI provide the agent orchestration and tool-execution layers.
---

## Repository Structure

```text
Lite-Weight-Pi-Agent/
│
├── AGENTS.md
├── .gitignore
│
└── pi-gateway/
    ├── pi_gateway/
    │   └── telegram_bot.py
    ├── pyproject.toml
    └── ...
```

`AGENTS.md` contains the instructions and tool context used by the Pi agent.

The `pi-gateway` directory contains the modified gateway implementation, including the additional Telegram attachment-handling functionality.

---

