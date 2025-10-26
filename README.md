# 🧠 Nodemations Workflow (n8n + Vapi Integration)

## 📘 Overview
The *Nodemations* workflow is a fully automated AI-powered meeting assistant built using **n8n** and **Vapi**.  
It integrates *Zoom, Google Drive, Google Sheets, Gmail, and Gemini AI* — with *Vapi* acting as the conversational interface that triggers and controls n8n workflows.

---

## ⚙ Process Overview
This system combines **Vapi’s assistant interface** and **n8n’s automation workflow**:

1. **Create a Vapi account**  
   - Sign up at [Vapi.ai](https://vapi.ai).
   - Create a new **Assistant** in your Vapi dashboard.

2. **Paste the provided prompts**  
   - Copy the text prompts from the `prompts.txt` file in this repo.  
   - Paste them into the Vapi assistant configuration under the **Prompt** section.  
   - Include the **tool format** exactly as described in the file.

3. **Add your n8n webhook as a Tool**  
   - In your Vapi assistant settings, go to **Tools** → **Add Tool**.  
   - Paste your n8n webhook URL (from the workflow trigger node) in the **Server URL** field.  
   - This allows the assistant to trigger n8n workflows directly when you speak or type commands.

4. **Interact with your Assistant**  
   - You can now “talk” to your Vapi assistant.  
   - When you say something like *“Schedule a meeting at 5 PM with the tech team,”*  
     → Vapi will call the linked n8n webhook and start the automation workflow.

---

## 🧩 n8n Workflow Details

### Workflow 1: **Meeting Creation**
Triggered by Vapi via the webhook.
- **Webhook Node** — Receives meeting data (topic, date, participants).
- **Date & Time Node** — Parses and formats the date/time.
- **Zoom Node** — Creates a meeting automatically.
- **Google Sheets Node** — Fetches email list for invites.
- **Gmail Node** — Sends meeting invite and reminder.

🕐 **Reminder Logic:**  
If the meeting is scheduled less than 10 minutes ahead, the reminder email is sent immediately; otherwise, it waits until 10 minutes before the start time.

---

### Workflow 2: **Post-Meeting Summary**
Triggered when a new meeting folder is created in Google Drive (recording uploaded).

- **Drive Trigger Node** — Detects new recording folder.
- **File Node** — Fetches the `.m4a` recording file.
- **Gemini Node** — Transcribes the audio to binary text format.
- **Code Node** — Extracts clean text from Gemini’s response.
- **Gemini Summarization Node** — Generates structured meeting summary.
- **Gmail Node** — Sends the final summary to all team members.

---

## 📦 How to Import the Workflow

1. Open **n8n** → *Workflows* → *Import from File*  
2. Upload the `Nodemations.json` file provided in this repository.  
3. Configure your credentials:
   - *Google Sheets OAuth2*
   - *Gmail OAuth2*
   - *Zoom OAuth2*
   - *Google Gemini API*
4. Save and *Activate* the workflow.

---

## ▶ Full Flow Summary

1. You talk to the **Vapi Assistant** → it triggers the n8n webhook.  
2. n8n **creates and schedules** the meeting automatically.  
3. When the host starts and ends the meeting, the **recording is saved** to Drive.  
4. n8n detects the new folder and starts **Workflow 2**.  
5. Gemini **transcribes** and **summarizes** the meeting audio.  
6. A **summary email** is automatically sent to all members.

---

## 🧠 Tech Stack
- **n8n** (Automation Platform)
- **Vapi** (AI Assistant Interface)
- **Zoom API**
- **Google Drive**
- **Google Sheets**
- **Gmail API**
- **Google Gemini (PaLM API)**

---

## 💡 Example Use Case

Imagine your assistant “Ava” on Vapi:
> You: “Ava, schedule a project sync with the frontend team tomorrow at 11.”  
> Ava: “Sure! I’ve scheduled it and sent out invites.”  
> — (Later) —  
> The meeting ends, recording uploads, and Ava emails a summary automatically.

---

## 🏁 Conclusion
The *Nodemations Workflow (Vapi + n8n)* unites **AI conversations** with **automated workflow execution**.  
It’s a next-generation meeting assistant that can *schedule, summarize, and share* — all hands-free effortlessly!

###  Watch on Youtube
Here is a sample demo of the work and how it gives the reponse in a youtube video
🔗link : [Nodemations](https://youtu.be/dXQwjDspVw0)
