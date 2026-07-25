# 🎙️ Sideline Triage Assistant

**A voice-based AI injury triage tool for anyone on the sideline — coaches, players, parents, or teammates.**

🔴 **Live Demo:** [sideline-triage-assistant-n.onrender.com](https://sideline-triage-assistant-n.onrender.com/)

---

## 🚨 The Problem

When a player goes down during a youth or amateur sports match, the coach is usually the only person there — and they almost never have medical training. They have seconds, not minutes, to decide:

- Can the player walk it off?
- Should they be immobilized?
- Does this need emergency services right now?

A wrong call in that moment can turn a manageable injury into a serious, long-term one. Coaches want to protect their players but have no reliable, real-time guidance on the field.

---

## ✅ The Solution

**Sideline Triage Assistant** closes that gap in under 10 seconds.

1. Anyone on the sideline taps the red button
2. Speaks a few words about what happened — even urgent, fragmented speech like *"Number 7, twisted her ankle bad"* is enough
3. The AI instantly returns:
   - **Injury Risk Level** → Low 🟢 / Moderate 🟠 / High 🔴 (large, color-coded — readable in sunlight)
   - **What To Do Right Now** — plain language, step-by-step protocol
   - **Player & Symptom** extracted from speech
   - **One-tap emergency call** (108 Ambulance / 112 Emergency) auto-surfaces for High-risk results

The tool is explicitly framed as **decision support, not medical treatment** — it never claims to replace a doctor, paramedic, or emergency services.

---

## 🧠 How the AI Works

This is not a chatbot with hardcoded rules. Every decision comes from Gemini.

| Step | What Happens |
|---|---|
| 1 | Raw audio sent directly to **Gemini 3.5 Flash** as inline bytes (no separate speech-to-text step) |
| 2 | Single API call does transcription + player/symptom extraction + risk classification simultaneously |
| 3 | Response constrained to a **strict JSON schema** — always structured, always parseable |
| 4 | **Minimal thinking mode** used for lowest possible latency |
| 5 | When information is sparse, model errs toward **higher risk** (safer default) |

This single-call multimodal approach is what makes it fast enough to be useful in a real emergency.

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| **Backend** | Python, FastAPI, `anyio` (async thread offload) |
| **AI Model** | Google Gemini 3.5 Flash via `google-genai` SDK |
| **AI Features** | Structured JSON output, schema-constrained generation, minimal-thinking mode |
| **Frontend** | Single-page HTML/CSS/JS — no framework, no build step |
| **Audio** | Native browser `MediaRecorder` API |
| **Deployment** | Render (Python web service) |
| **Keep-Alive** | cron-job.org pings `/ping` every 10 min — no cold starts |

---

## 📁 Project Structure

```
sideline-triage-assistant/
│
├── main.py              # FastAPI app: AI logic + /webhook/voice + frontend UI
├── requirements.txt     # Python dependencies
└── README.md
```

---

## 🚀 Run Locally

**1. Clone the repo**
```bash
git clone https://github.com/nishanth-0427/sideline-triage-assistant.git
cd sideline-triage-assistant
```

**2. Create virtual environment & install dependencies**
```bash
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # macOS/Linux
pip install -r requirements.txt
```

**3. Set your Gemini API key**
(Get a free key at https://aistudio.google.com/apikey)
```bash
set GEMINI_API_KEY=your_key_here          # Windows cmd
$env:GEMINI_API_KEY="your_key_here"       # PowerShell
# export GEMINI_API_KEY=your_key_here     # macOS/Linux
```

**4. Run the server**
```bash
uvicorn main:app --reload
```

**5. Open in browser**

Go to `http://localhost:8000`, allow microphone access, and record a report.

---

## ☁️ Deploy on Render

| Setting | Value |
|---|---|
| **Build command** | `pip install -r requirements.txt` |
| **Start command** | `uvicorn main:app --host 0.0.0.0 --port $PORT` |
| **Environment variable** | `GEMINI_API_KEY = your_key_here` |

---

## ⚠️ Disclaimer

This tool provides first-response guidance only and does not replace professional medical advice or emergency services. For any life-threatening injury, call **108 (Ambulance)** or **112 (All Emergencies)** immediately.

---

## 👨‍💻 Built By

**Nishanth P** — Final Year B.E. CSE Student, Sri Krishna College of Technology, Coimbatore

[![Portfolio](https://img.shields.io/badge/Portfolio-nishanth.is--a.dev-blue)](https://nishanth.is-a.dev/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-nishanth0427-blue)](https://www.linkedin.com/in/nishanth0427)
[![GitHub](https://img.shields.io/badge/GitHub-nishanth--0427-black)](https://github.com/nishanth-0427)