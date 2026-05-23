⚡ ATS Match Scorer — Frontend
A sleek, 3D-animated frontend for the ATS Match Scorer n8n AI pipeline. Built to be deployed directly from GitHub Pages with zero dependencies beyond a browser.
![ATS Match Scorer](https://img.shields.io/badge/Powered%20by-n8n%20%2B%20Groq%20LLaMA-gold?style=flat-square)
![No Build Step](https://img.shields.io/badge/Build%20Step-None-brightgreen?style=flat-square)
![GitHub Pages Ready](https://img.shields.io/badge/GitHub%20Pages-Ready-blue?style=flat-square)
---
🎯 What It Does
This frontend connects to three n8n webhook workflows in sequence:
Step	Workflow	Endpoint	Input	Output
1	JD Parser	`POST /webhook/jd-ingest`	`{ jd_text }`	Structured JD JSON
2	Resume Parser	`POST /webhook/resume-upload`	`{ resume_text }`	Structured Resume JSON
3	Match Scorer	`POST /webhook/match-score`	`{ parsed_jd, parsed_resume }`	Score + Analysis
Output includes:
Match Score (0–100)
Match Level (Strong / Moderate / Weak)
Strengths list
Gaps list
AI reasoning (2–3 sentences)
Parsed JD breakdown
Parsed Resume breakdown
---
🚀 Quick Deploy to GitHub Pages
Fork this repo (or push these files to a new GitHub repo)
Go to Settings → Pages
Set Source to `main` branch, `/ (root)` folder
Click Save — your site will be live in ~60 seconds
```
https://your-username.github.io/match-scorer-frontend/
```
---
🔧 Setup
1. Configure Your n8n Instance
In the app, enter your n8n base URL:
```
https://your-n8n-instance.com
```
The URL is saved to `localStorage` — you only need to enter it once per browser.
2. Make Sure Your n8n Workflows Are Active
Your three workflows must be active and their webhooks live:
Workflow	Webhook Path	HTTP Method
`01-JD-Parser`	`/webhook/jd-ingest`	POST
`02-Resume-Parser`	`/webhook/resume-upload`	POST
`03-Match-Scorer`	`/webhook/match-score`	POST
3. Enable CORS in n8n
If your frontend is hosted on a different domain, you need n8n to allow cross-origin requests. Add to your n8n environment:
```env
N8N_CORS_ALLOWED_ORIGINS=https://your-github-pages-url.github.io
```
Or for development: `N8N_CORS_ALLOWED_ORIGINS=*`
---
📁 File Structure
```
match-scorer-frontend/
├── index.html      ← Complete single-file application
└── README.md       ← This file
```
No build step. No npm. No configuration files. Just open `index.html`.
---
✨ Features
3D Animated Background — Three.js particle network that reacts to mouse movement
3-Step Wizard UI — Configure → Input → Results
Real-time Score Ring — Animated circular progress indicator
Color-coded Match Level — Green (Strong), Amber (Moderate), Red (Weak)
Strengths & Gaps Tags — Visual breakdown of the AI analysis
Parsed Data Preview — See what the AI extracted from JD and Resume
Demo Data — One-click load of realistic sample content
JSON Export — Download full results as a JSON file
Responsive — Works on mobile and tablet
localStorage — Base URL is remembered between sessions
3D Card Hover Effects — CSS perspective transforms on cards
---
🧩 n8n Workflow API Reference
POST `/webhook/jd-ingest`
```json
{ "jd_text": "Full job description text here..." }
```
Returns:
```json
{
  "job_title": "Senior Engineer",
  "seniority": "senior",
  "required_skills": ["React", "Node.js"],
  "nice_to_have_skills": ["GraphQL"],
  "min_experience_years": 5,
  "location": "Remote",
  "employment_type": "full-time",
  "responsibilities": ["..."],
  "summary": "..."
}
```
POST `/webhook/resume-upload`
```json
{ "resume_text": "Full resume text here..." }
```
Returns:
```json
{
  "candidate_name": "Jane Doe",
  "total_years_experience": 6,
  "core_skills": ["React", "TypeScript", "Node.js"],
  "most_recent_role": "Senior Software Engineer",
  "education_degree": "B.Tech Computer Science"
}
```
POST `/webhook/match-score`
```json
{
  "parsed_jd": { ...jd object... },
  "parsed_resume": { ...resume object... }
}
```
Returns:
```json
{
  "match_score": 85,
  "match_level": "Strong Match",
  "strengths": ["Strong React & Node.js experience", "Cloud expertise matches AWS requirement"],
  "gaps": ["No GraphQL mentioned", "Limited CI/CD experience listed"],
  "reasoning": "The candidate demonstrates strong alignment with core technical requirements. Minor gaps in nice-to-have areas do not significantly impact overall suitability."
}
```
---
🛠 Tech Stack
Layer	Technology
3D Background	Three.js r128
Fonts	Syne (display) + DM Sans (body) via Google Fonts
Styling	Vanilla CSS with CSS custom properties
Logic	Vanilla JavaScript (ES2020)
Hosting	GitHub Pages (static)
Backend	n8n + Groq LLaMA 3.3 70B / LLaMA 3.1 8B
---
🔒 Security Notes
API keys are never stored in the frontend — all AI calls are handled server-side by n8n
The base URL is saved to `localStorage` (client-side only)
For production use, restrict n8n CORS to your specific GitHub Pages domain
---
📄 License
MIT — free to use, modify, and deploy.
