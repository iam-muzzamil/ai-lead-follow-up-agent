# 🤖 AI Lead Follow‑Up Agent

An autonomous AI agent that monitors a Gmail inbox, scores incoming leads with **Gemini**, sends personalized replies to qualified leads (with a Calendly booking link), logs everything to Google Sheets, and alerts the sales team via Slack.

---

## ✨ Features

- **📬 Inbox Monitoring** – Automatically watches for new lead emails (website forms, referrals, LinkedIn)
- **🧠 AI Qualification** – Uses Gemini to score leads as **Hot / Warm / Cold** based on budget, urgency, and project clarity
- **✉️ Auto‑Reply** – Sends a personalized, AI‑written reply with a Calendly booking link to Hot/Warm leads
- **📊 Lead Tracking** – Logs every lead into a Google Sheets dashboard (date, name, email, message, score, status, reply sent, meeting booked)
- **💬 Slack Alerts** – Instant notification in a dedicated `#new-leads` channel
- **❄️ Cold Lead Nurture** – Cold leads are automatically added to a separate nurture list for future follow‑up

---

## 🧱 Tech Stack

| Tool | Role |
|------|------|
| [n8n](https://n8n.io) | Workflow automation (no‑code/low‑code) |
| [Google Gemini](https://ai.google.dev) | AI brain – qualification & reply generation |
| Gmail API | Email trigger & sending |
| Google Sheets | Lead tracking database |
| Slack | Real‑time alerts |
| Calendly | Meeting booking link |

---

## ⚙️ How It Works

1. **Gmail Trigger** detects a new email in the monitored inbox.
2. **Extract** node pulls out the sender’s name, email, and message body.
3. **Gemini** receives a detailed prompt containing the lead message and replies with a JSON:
   - Score (`Hot`, `Warm`, `Cold`)
   - Personalised email subject and body (references the lead’s project, avoids personal names, detects competitors)
4. **IF node** routes the lead:
   - **Hot / Warm** → Sends the AI‑generated reply with a Calendly link via Gmail.
   - **Cold** → Logs to a cold nurture sheet (no reply sent).
5. **All leads** are logged to a master Google Sheet and a Slack notification is fired.

---

## 📂 Workflow Structure

<div align="center">
  <img src="[SCREENSHOT_LINK]" alt="n8n workflow screenshot" width="800"/>
</div>

*(Add a screenshot of your n8n canvas here. You can upload an image to the repo and use its raw URL.)*

---

## 🛠️ Setup Instructions

1. **Download** the `ai-lead-follow-up-agent.json` file from this repository.
2. **Import** it into your n8n cloud or self‑hosted instance.
3. **Set up credentials** for:
   - Gmail (OAuth2)
   - Google Sheets (OAuth2)
   - Slack (OAuth2)
4. **Replace placeholders** in the imported workflow:
   - `YOUR_GEMINI_API_KEY` – get a free Gemini API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
   - `YOUR_GOOGLE_SHEET_URL` – paste your own Google Sheet URL (must have headers: Date, Name, Email, Message, Score, Status, Reply Sent, Meeting Booked)
   - `YOUR_SLACK_CHANNEL_ID` – channel ID for `#new-leads`
   - Calendly link – replace `https://calendly.com/yourusername/30min` with your own booking link
5. **Activate** the workflow and send a test email to the monitored inbox.

---

## 📈 Use Cases

- Software houses & IT agencies handling client inquiries
- Marketing agencies qualifying leads from contact forms
- Freelancers automating initial follow‑up
- Any B2B business wanting to **save 10+ hours/week** on manual lead replies

---

## 👤 About the Creator

**Muzzamil Anwaar** – AI Automation Specialist | Python Developer | Electrical Engineer

I build AI‑powered automation that helps businesses scale without adding headcount.  
If you’d like a custom deployment of this agent or a similar automation, feel free to reach out.

📧 anwaarmuzzamil@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/muhammad-muzzamil-anwaar-57a0402aa/)

---

## 📄 License

This project is open‑source under the [MIT License](LICENSE).  
Feel free to use, modify, and share it. Attribution is appreciated.
