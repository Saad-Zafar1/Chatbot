# Browser AI Chatbot

A Python chatbot with a Chainlit browser interface. It uses the OpenAI Agents SDK with an externally configured compatible model endpoint and maintains conversation history during each user session.

## Features

- A welcome message when a chat starts.
- Browser-based message input and model responses through Chainlit.
- Conversation context stored in the current Chainlit user session.
- A temporary thinking message updated with the final response.
- Error feedback when a model request fails.
- Conversation export to `chat_history.json` when the chat ends.

## Requirements

- Python 3.13 or newer.
- uv.
- An API key and compatible endpoint/model, plus internet access.

Declared dependencies are Chainlit, OpenAI Agents SDK, python-dotenv, and Rich. The repository includes `uv.lock`.

## Setup

```sh
git clone https://github.com/Saad-Zafar1/Chatbot.git
cd Chatbot
uv sync
```

Use [`.env.example`](.env.example) as a template for a local `.env` file, or set the following environment variables:

```dotenv
GEMINI_API_KEY=your_gemini_api_key
GEMINI_API_URL=https://generativelanguage.googleapis.com/v1beta/
GEMINI_API_MODEL=your_available_model_name
```

The names are read by `mystery.py`. All three values must be nonempty. Use a model available to your API account.

## Run the browser application

```sh
uv run chainlit run chatbot.py
```

Open the local URL printed by Chainlit. `main.py` is a starter greeting script; the chatbot application is `chatbot.py`.

## Project structure

| Path | Purpose |
| --- | --- |
| `chatbot.py` | Chainlit chat lifecycle, agent setup, and message processing |
| `mystery.py` | Loads and validates API environment variables |
| `.chainlit/config.toml` | Chainlit UI configuration |
| `.chainlit/translations/` | UI translation files |
| `chainlit.md` | Chainlit welcome content |
| `chat_history.json` | Last saved session history |
| `chat-in-browser.png` | Recorded browser screenshot |
| `pyproject.toml`, `uv.lock` | Dependencies |

## Scope and limitations

- History is held in memory during the session. It is not loaded from the saved JSON file when a new chat starts.
- Ending a chat writes to one shared `chat_history.json` file, overwriting the previous export.
- The asynchronous message callback uses a synchronous model run, so it can block message handling while waiting for the API.
- The source does not add application-level account management, a database-backed chat archive, tool calling, or streaming model output.
- The original `gitignore` file is retained. The root `.gitignore` excludes local environments, credentials, bytecode, and chat exports; it does not remove files already tracked. The tracked `.env` currently contains an empty API key; configure credentials locally and avoid committing real secrets.

Current API execution and browser behaviour have not been revalidated as part of this documentation update.
