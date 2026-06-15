# [CYBERBOT] — Security & IT Assistant

> A hacker-aesthetic, AI-powered cybersecurity chatbot that runs entirely in the browser. No backend, no server, no setup — just drop it in a folder and fire it up.

---

## What It Is

**CyberBot** is a single-page web application that wraps the **Groq API** (LLaMA 3.3 70B) inside a cyberpunk terminal UI, purpose-built for cybersecurity and IT conversations. It enforces strict topic scope — ask it about OWASP, Nmap, SQL injection, CTF tricks, privilege escalation, or Linux internals and it delivers clean, formatted answers. Ask it about anything else and it bites back.

---

## Features

- **AI-powered Q&A** via Groq's `llama-3.3-70b-versatile` model — fast, free tier available
- **Domain-locked responses** — strictly cybersecurity & IT only; off-topic queries get a one-liner shutout
- **Prompt injection defense** — a security wrapper around every user message blocks system prompt extraction, jailbreaks, DAN/developer mode attempts, and privilege escalation tricks
- **Multi-session chat history** — saved to `localStorage`, survives page refresh; switch between past conversations from the sidebar
- **Auto-titling** — sessions are named from the first message automatically
- **Markdown rendering** — responses render with headers, bullet lists, code blocks, and inline code properly styled
- **Copy button** — hover any bot message to copy the raw markdown content
- **Auto-resizing input** — textarea grows with your message up to a comfortable cap
- **Responsive layout** — sidebar hides on mobile, chat stays fully functional
- **API key modal** — key stored locally in `localStorage`, never leaves the browser, prompts on first launch

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML5 / CSS3 / JavaScript (ES6+) |
| AI Backend | [Groq API](https://console.groq.com) — `llama-3.3-70b-versatile` |
| Fonts | Google Fonts — Share Tech Mono, Inter |
| Storage | Browser `localStorage` |
| Dependencies | **Zero** — no npm, no build step, no frameworks |

---

## Getting Started

### 1. Get a free Groq API key

Sign up at [console.groq.com](https://console.groq.com), create an API key (it's free), and copy it.

### 2. Open the app

Just open `index.html` in any modern browser — Chrome, Firefox, Edge, Brave. Works from the filesystem or any static host.

```bash
# Option A: open directly
open index.html

# Option B: serve locally (avoids any browser fetch quirks)
python3 -m http.server 8080
# then visit http://localhost:8080
```

### 3. Enter your API key

On first load, the settings modal opens automatically. Paste your `gsk_...` key and hit **Save Key**. You're in.

---

## File Structure

```
cyberbot/
├── index.html     # App shell, layout, modal
├── style.css      # Full dark theme, animations, responsive rules
└── script.js      # Chat logic, session management, API calls, markdown renderer
```

---

## How It Works

```
User types message
       │
       ▼
Security wrapper prepended to prompt
(blocks jailbreaks, prompt injection, system prompt extraction)
       │
       ▼
Groq API called with:
  - system: CyberBot persona + topic scope rules
  - messages: full conversation history
       │
       ▼
Response rendered as Markdown
Session saved to localStorage
```

The conversation history is maintained in-memory and persisted per session in `localStorage`. Every user message is wrapped in a hardened security envelope before being sent to the API — the visible chat shows the clean original text, but the API receives the protected version.

---

## Topic Scope

CyberBot **only** responds to questions about:

- Penetration testing, VAPT, ethical hacking
- Web app security — OWASP Top 10, SQLi, XSS, CSRF, SSRF, XXE
- Network security — TCP/IP, DNS, Wireshark, Nmap, Metasploit
- CTF challenges — forensics, crypto, pwn, web, OSINT
- Malware analysis, reverse engineering, digital forensics
- Linux & Windows administration, privilege escalation
- Cloud security, Docker, DevSecOps
- Programming for security — Python, Bash, C
- CVEs, exploit development, cryptography

Anything outside this scope gets rejected with a single savage line.

---

## Security Design

The app implements several layers against prompt injection and jailbreak attempts:

- **Instruction hierarchy enforcement** — system prompt always takes priority over user input
- **Mode-change blocking** — DAN, developer mode, unrestricted mode, and similar attempts are rejected
- **Confidentiality guardrails** — system prompt contents, internal reasoning, and API config cannot be extracted
- **Escalating pushback** — repeated extraction attempts get progressively less polite responses
- **Untrusted input treatment** — all user content is treated as untrusted data, never as instructions

> ⚠ **Note:** These are application-level defenses. The model is still a general LLM; no prompt-based guardrail is unconditionally secure. Do not use this to process sensitive data.

---

## Deployment

CyberBot is a pure static site — deploy anywhere:

| Platform | Command / Method |
|---|---|
| GitHub Pages | Push to repo → enable Pages in settings |
| Netlify | Drag-and-drop the folder into Netlify Drop |
| Vercel | `vercel` CLI or import from GitHub |
| Any web host | Upload 3 files — done |

No environment variables, no build process, no server config needed.

---

## Customization

**Change the AI model** — edit `script.js`:
```js
model: 'llama-3.3-70b-versatile'  // swap for any Groq-supported model
```

**Adjust response length** — edit `max_tokens` in the API call (default: 1024).

**Modify topic scope** — edit `SYSTEM_PROMPT` at the top of `script.js`.

**Re-enable quick topic buttons** — the sidebar has pre-built topic buttons commented out in `index.html`. Uncomment the `<div class="topics">` block to restore them.

---

## Limitations

- No streaming — responses appear all at once after the full completion
- No file upload support
- Chat history is browser-local; no cloud sync or cross-device access
- Groq free tier has rate limits; heavy use may hit them
- Mobile layout hides the sidebar (sessions accessible via "New Chat" flow only)

---

## License

MIT — use it, fork it, embed it in your own tools. Credit appreciated but not required.

---

## Author

Built by **[Roshan Das](https://github.com/ROSHAN-Z89)** — ECE undergrad, offensive security enthusiast, VAPT practitioner.

- Portfolio: [roshan-z89.github.io/Portfolio](https://roshan-z89.github.io/Portfolio)
- Blog: [rootiq.hashnode.dev](https://rootiq.hashnode.dev)
- LinkedIn: [rouson-das-563b52284](https://linkedin.com/in/rouson-das-563b52284)

---

*Educational use only. Practice only in authorized environments.*
