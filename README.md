# Customer Support Ticket Bot with n8n, Telegram, and Local Gemma 4

An AI-powered customer support automation built with n8n, Telegram, Ollama, Gemma 4, Google Sheets, and Open-Meteo.

The workflow receives support requests through Telegram, classifies them locally using Gemma 4, routes them into different support categories, logs tickets to Google Sheets, automatically replies to users, and calls an external API when required.

## Architecture

Telegram Bot
→ Telegram Trigger
→ Normalize Input
→ Validate Text Input
→ Gemma 4 Classification through Ollama
→ Parse and Validate AI Output
→ Google Sheets Logging
→ Switch Category

The category router contains:

- Billing
- Technical
- General
- Fallback

The General branch can additionally call the Open-Meteo API for live weather information.

The Technical branch also sends an administrator notification when a technical support ticket is received.

## Technologies

- n8n
- Docker
- Telegram Bot API
- Ollama
- Gemma 4 e2b
- Google Sheets
- Open-Meteo REST API
- Cloudflare Tunnel

## AI Classification

Gemma 4 runs locally through Ollama.

The n8n HTTP Request node communicates with Ollama using:

```text
http://host.docker.internal:11434/api/chat
