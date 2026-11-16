# AI Expense Tracker - Secure Backend Proxy

This optional Node.js microservice serves as a secure proxy between the **AI Expense Tracker** Android client and the AI Provider API (Google Gemini).

## Architecture

```text
Android Client (Java / XML)
         │
         ▼ (HTTP POST /api/chat)
Backend Proxy Server (Node.js / Express)
         │
         ▼ (Gemini API with secret GEMINI_API_KEY)
Google Gemini API
```

## Security Rationale

1. **Zero Secret Leakage:** The Android client APK does **not** contain API keys.
2. **Rate Limiting & Abuse Prevention:** The proxy server can enforce IP and user-rate limits.
3. **Data Sanitization:** Only relevant summary numbers (monthly totals, category aggregations) are forwarded to the AI; sensitive raw personal identifiers remain locally on the device's SQLite database.

## Running Locally

1. Install dependencies:
   ```bash
   npm install
   ```

2. Create a `.env` file:
   ```env
   PORT=3000
   GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
   ```

3. Start the server:
   ```bash
   npm start
   ```

4. In the Android App:
   Open **Settings -> AI Backend Server Endpoint** and enter:
   `http://10.0.2.2:3000/api/chat` (if using Android Emulator) or your deployed backend URL.
