# SuiiSoft-project
That project demonstrates professional AI agent, which assists you organise news or social media information 
# SuiiSoft

Frontend (`static/index.html`) + backend (`main.py`, FastAPI + SQLite).
Features: media-literacy trainer, fact-check bot, email/password and Google sign-in, user profile with stats.

## Run

Python 3.10+ required.

```bash
cd suiisoft
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env        # then fill in the values
uvicorn main:app --reload
```

Open http://localhost:8000 (use `localhost`, not `127.0.0.1`, so it matches the Google origin below).

## Settings (`.env`)

| Variable | What it is |
|---|---|
| `SECRET_KEY` | Random string for signing login tokens. `python -c "import secrets; print(secrets.token_hex(32))"` |
| `GOOGLE_CLIENT_ID` | From Google Cloud Console. It is injected into the page automatically. |
| `ANTHROPIC_API_KEY` | From console.anthropic.com. Needed for the fact-check bot. |
| `CLAUDE_MODEL` | Model for the bot (default `claude-sonnet-5-5`). |
| `DAILY_CHECK_LIMIT` | Bot checks per user per day (default 20). |

## Google sign-in setup

1. Go to https://console.cloud.google.com and create a project.
2. APIs & Services → OAuth consent screen: fill in the app name and your email.
3. APIs & Services → Credentials → Create credentials → OAuth client ID → **Web application**.
4. Under **Authorized JavaScript origins** add `http://localhost:8000` (and your real https domain when you deploy).
5. Copy the Client ID into `GOOGLE_CLIENT_ID` in `.env` and restart the server.

## Before going live

- Host over HTTPS and set a strong `SECRET_KEY`.
- Add your domain to the Google authorized origins.
- Consider rate limiting on `/api/login` and `/api/register`.
- Back up `suiisoft.db` (or move to PostgreSQL if you grow).
[Uploading README.md…]()
