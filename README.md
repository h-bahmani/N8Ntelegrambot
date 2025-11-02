# N8Ntelegrambot
🏥 Doctor Appointment Telegram Bot

📘 Overview

This project is an AI-powered medical appointment assistant built with n8n and Google Gemini (PaLM).
The bot communicates with users on Telegram, collects appointment details (date, time, doctor/department, full name, email), and can respond in text or voice using TTS.

⚙️ Technologies Used
n8n
 – workflow automation platform

Google Gemini (PaLM API) – conversational AI

Cloudflare AI TTS (melotts) – text-to-speech generation

Telegram Bot API – chat interface

Gmail API – sends appointment confirmations


🧠 Features

Handles both text and voice messages

Automatically detects user language (Persian/English) and replies accordingly

Generates short, natural, and polite responses

Maintains conversational memory for continuity

Converts responses to audio (MP3) via Cloudflare TTS

Sends confirmation emails through Gmail


🔄 Workflow Logic

Telegram Trigger
The workflow starts when a message is received from a Telegram user.

Set (normalize)
Extracts key fields such as chatId, text, and command flags (/start, /mode).

IF Conditions
Determines whether the message is a start command, text, or voice message.

Voice Flow

Downloads the voice file from Telegram

Normalizes audio metadata (e.g., MIME type)

Sends it to Google Gemini for speech-to-text transcription

Uses the transcribed text for the AI response

AI Agent (Text / Voice)
A fine-tuned AI agent named “Miro” acts as a friendly booking assistant, following predefined conversation rules.
It remembers previous messages using memory buffers.

Prepare Reply
Cleans the AI output (removes <think> blocks, JSON, or formatting) to generate plain text.

Translate for TTS (optional)
Converts Persian output into short, clean English text for better TTS quality.

HTTP Request → Cloudflare AI TTS
Sends the cleaned English text to Cloudflare to generate an MP3 audio response.

Telegram Output
Sends either the text reply or the audio file (or both) back to the user.
