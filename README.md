# 📱 n8n WhatsApp + Google Drive Automation

This project connects **WhatsApp** (via Twilio Sandbox) to **Google Drive** using **n8n**.  
It allows you to **list**, **delete**, **move**, and **summarise** files inside Google Drive directly from WhatsApp commands.

---

## ✨ Features
- ✅ **LIST** files in a Google Drive folder
- ✅ **DELETE** a specific file in Google Drive
- ✅ **MOVE** a file to another folder
- ✅ **SUMMARY** of all documents (PDF/DOCX/TXT) using GPT-4o 
- ✅ **Logging** of all actions to a Google Sheet for auditing

---

## 🛠 Requirements
- A **Twilio** account with WhatsApp Sandbox access
- **Google Cloud Project** with Drive API enabled
- **OpenAI API key** 
- **n8n** (self-hosted or cloud)
- Docker (optional, for self-hosting)
- **ngrok** (for tunneling your local n8n instance to the internet)

---

## 📂 Project Structure
```
n8n-whatsapp-drive-automation/
│
├── workflow.json       # Exported n8n workflow
├── .env-sample         # Example environment variables
├── commands.md         # WhatsApp command syntax
├── README.md           # Setup documentation
└── helper-scripts/     # Any additional scripts (optional)
```

---

## ⚙️ Environment Variables

Copy `.env-sample` → `.env` and fill in your credentials:

```bash
cp .env-sample .env
```

`.env-sample` includes:
```env
# Twilio
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

# Google
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_REDIRECT_URI=https://your-n8n-domain/oauth2/callback
GOOGLE_REFRESH_TOKEN=your_refresh_token

# OpenAI
OPENAI_API_KEY=your_openai_key

# Optional
SAFEWORD=CONFIRMDELETE
```

---

## 🔑 Setup Instructions

### 1️⃣ Twilio Sandbox for WhatsApp
1. Log in to [Twilio Console](https://www.twilio.com/console).
2. Navigate to **Messaging → Try it Out → Send a WhatsApp message**.
3. Join the sandbox by sending the **provided join code** to the Twilio WhatsApp number.
4. In Twilio Sandbox settings:
   - **WHEN A MESSAGE COMES IN** → set your **n8n Webhook URL** (e.g., `https://your-n8n-domain/webhook/whatsapp`).

---

### 2️⃣ Google Drive API Setup
1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create a **new project**.
3. Enable the **Google Drive API**.
4. Go to **APIs & Services → Credentials**.
5. Create **OAuth 2.0 Client ID** (Application type: Web application).
6. Add your **n8n OAuth redirect URI** (e.g., `https://your-n8n-domain/rest/oauth2-credential/callback`).
7. Download your credentials JSON — copy `client_id` and `client_secret` to `.env`.
8. Use n8n’s **Google Drive node** to connect and generate the `refresh_token`.

---

### 3️⃣ OpenAI Setup
- Sign up at [OpenAI](https://platform.openai.com/).
- Create an API key and place it in `.env`.

---


### 4️⃣ Running n8n with Docker

```bash
docker run -it --rm   --name n8n   -p 5678:5678   -v ~/.n8n:/home/node/.n8n   --env-file .env   n8nio/n8n
```

Access n8n at:  
👉 `http://localhost:5678`

---

### 5️⃣ Using ngrok for Local Development

If you’re running n8n locally and want Twilio to reach it:

1. [Download ngrok](https://ngrok.com/download) and install it.
2. Run:
   ```bash
   ngrok http 5678
   ```
3. You’ll get a public HTTPS URL like:
   ```
   https://randomstring.ngrok.io
   ```
4. Use this URL in your Twilio WhatsApp sandbox settings as the webhook endpoint:
   ```
   https://randomstring.ngrok.io/webhook/whatsapp
   ```

---

## 📜 WhatsApp Command Syntax

See [`commands.md`](./commands.md) for full list.

Example:
```
LIST <Folder Name>
DELETE <File Name>
MOVE <File Name>
SUMMARY <File Name>

```

---

# Demo video link
```
https://youtube.com/shorts/dVi3krtPNUU?feature=share
```

---

## 📄 License
MIT License — free to use and modify.
