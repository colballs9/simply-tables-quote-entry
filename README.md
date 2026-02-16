# Simply Tables — Quote Entry App

Voice-powered quote entry tool for the Simply Tables Pricing sheet system. Speak your table specs, let AI parse them, and write directly to Google Sheets.

## How it works

1. **Speak** — Record via mic (interview mode or audio dump)
2. **Transcribe** — OpenAI Whisper converts speech to text with trade-term accuracy
3. **Parse** — Claude interprets the text and maps to exact Pricing sheet fields
4. **Import** — JSON sent directly to Google Sheets via Apps Script

## Setup

### 1. Deploy the Apps Script

Add `quote_entry_webapp_v3.gs` to your Google Sheets Apps Script project:

1. Open your Quote Sheet → Extensions → Apps Script
2. Create a new file called `QuoteEntryWebApp`
3. Paste the contents of `quote_entry_webapp_v3.gs`
4. Add this to your `onOpen()` menu:
   ```javascript
   .addItem('🎤 Quote Entry App', 'openQuoteEntryApp')
   ```
5. Deploy → New deployment → **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone** (or Anyone with Google account)
6. Copy the deployment URL

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
3. Click "Test Connections" to verify
4. Click "Save & Continue"

Keys are saved to your browser's localStorage (local to your device, never transmitted).

### 4. Redeploy Apps Script after changes

If you update the `.gs` file:
1. Apps Script → Deploy → Manage deployments
2. Edit the existing deployment → **New version**
3. Deploy

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
