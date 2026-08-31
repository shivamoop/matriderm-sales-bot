# Master Sales Agent

A private, enterprise-grade AI Chatbot for querying Sales data.

## Features
- **Pure HTML/JS Frontend:** A lightning-fast, pixel-perfect clone of the ChatGPT Desktop application.
- **Enterprise Security:** Secured by Google Identity Services. Access is strictly locked down to `@healthaids.in` employees.
- **Permanent Memory:** Uses a local SQLite database to persist chat history locally so conversations are never lost.

## Architecture
- `index.html`: The frontend UI (TailwindCSS) and Google Authentication flow.
- `server.py`: A lightweight local Python proxy server. It serves the HTML file and proxies API requests to n8n to bypass browser CORS policies during local testing.
- `chat_history.db`: A local SQLite database generated dynamically to store message history. (This file is ignored by git to keep your chat logs private).

## Local Development
1. Start your `ngrok` tunnel for n8n.
2. Start the n8n application.
3. Run the local proxy server:
   ```bash
   python3 server.py
   ```
4. Open your browser and navigate to `http://localhost:8000`.

## Deployment (Vercel)
To host this publicly on Vercel without needing `server.py`:
1. Create a `vercel.json` file in the root directory:
   ```json
   {
     "rewrites": [
       {
         "source": "/api/chat",
         "destination": "https://laurel-fraternal-subsonic.ngrok-free.dev/webhook/chat"
       }
     ]
   }
   ```
2. Upload this repository to GitHub.
3. Import the repository into Vercel. Vercel will automatically host `index.html` and use the rewrite rule to proxy your requests safely!

## Security Notice
The Google Client ID embedded in `index.html` is a public identifier. It is strictly tied to your authorized domains (e.g. localhost, Vercel) via your Google Cloud Console. Your actual `client_secret` JSON file should never be uploaded to this repository.
