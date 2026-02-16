# Simply Tables — Quote Entry App

Voice-powered quote entry tool for the Simply Tables Pricing sheet system. Speak your table specs, let AI parse them, and write directly to Google Sheets.

## How it works

1. **Speak** — Record via mic (interview mode or audio dump)
2. **Transcribe** — OpenAI Whisper converts speech to text with trade-term accuracy
3. **Parse** — Claude interprets the text and maps to exact Pricing sheet fields
4. **Import** — JSON sent directly to Google Sheets via Apps Script

## Setup

### 1. Deploy the Apps Script (one-time — works with every sheet)

This is a **standalone** deployment — not tied to any specific spreadsheet.

1. Go to [script.google.com](https://script.google.com) → New project
2. Delete the default `Code.gs` content
3. Paste the contents of `quote_entry_webapp_v3.gs`
4. Deploy → New deployment → **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone** (or Anyone with Google account)
5. Copy the deployment URL — this is your permanent endpoint for all sheets

### 2. Host the web app

**Option A: GitHub Pages (recommended)**
1. Fork or clone this repo
2. Go to Settings → Pages → Source: Deploy from branch → `main` / `root`
3. Your app URL: `https://yourusername.github.io/simply-tables-quote-entry/`

**Option B: Local**
Just open `index.html` in Chrome.

### 3. First launch

1. Open the app URL
2. Enter your API keys:
   - **OpenAI API key** — get one at [platform.openai.com/api-keys](https://platform.openai.com/api-keys)
   - **Anthropic API key** — get one at [console.anthropic.com](https://console.anthropic.com)
   - **Apps Script URL** — the deployment URL from step 1
3. Click "Test Connections" to verify all three
4. Click "Save & Continue"

Keys and the Apps Script URL are saved to your browser's localStorage (local to your device, never transmitted). You enter them once per device.

### 4. Using it with any quote sheet

1. Open the app
2. Paste any Google Sheets URL into the "Google Sheet URL" field
3. The app detects all Pricing tabs (Pricing 1, Pricing 2, etc.)
4. Pick the tab, see the next available column
5. Record your quote → sends directly to that sheet

Recent sheets are remembered — next time, just pick from the dropdown instead of pasting a URL.

### 5. Redeploy Apps Script after changes

If you update the `.gs` file:
1. Go to [script.google.com](https://script.google.com) → open your Quote Entry project
2. Deploy → Manage deployments
3. Edit the existing deployment → **New version**
4. Deploy

## Modes

### Interview
Guided question-by-question flow. App reads each question aloud (TTS), you answer via mic, Whisper transcribes, Claude parses. Auto-advances through all sections.

### Audio Dump
Describe all tables in natural language. Hit stop. Whisper transcribes the full recording. Claude parses everything into structured products with confidence indicators.

## Cost

- **Whisper:** ~$0.006/minute → 10 min quote ≈ $0.06
- **Claude Sonnet:** ~$0.02–0.07 per quote
- **Total:** ~$0.08–0.13 per quote

## Cell color coding

After import, the Pricing sheet cells are color-coded:
- **Yellow** — Claude was uncertain about the value
- **Light red** — Field expected but not mentioned

## Files

- `index.html` — The complete web app (single file)
- `quote_entry_webapp_v3.gs` — Apps Script server-side code

## Requirements

- Chrome browser (for mic access)
- OpenAI API account
- Anthropic API account
- Google Sheets with V5 Pricing sheet structure
