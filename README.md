<div align="center">

# 📬 Inboxly

### Your inbox already knows how your job search is going. This just tells you.

*An AI job-search command center that reads your Gmail every morning, figures out what actually happened, and hands you a report before your coffee's done.*

[![Cost](https://img.shields.io/badge/cost-%240%2Fmonth-brightgreen)](#-cost)
[![Read Only](https://img.shields.io/badge/mailbox-read--only-blue)](#-privacy-first)
[![License: MIT](https://img.shields.io/badge/license-MIT-lightgrey)](#-license)
[![Powered by](https://img.shields.io/badge/powered%20by-Claude-orange)](https://claude.com)

By - Anuj Wadi
</div>

---

## 😩 The problem

You're applying to 10+ jobs a week. Somewhere in your inbox, buried under "10 jobs you may like" and LinkedIn noise, is the one email that actually matters — a recruiter asking about your availability, an assessment deadline in 48 hours, an interview time in a timezone you have to convert twice.

You're not going to find it by scrolling. Nobody does.

## ✨ The fix

Two scheduled AI runs. Zero manual searching. Ever.

| ⏰ When | 📬 What you get |
|---|---|
| **Every morning, 10:00 AM** | Everything that happened in your inbox in the last 24 hours — interviews, assessments, recruiter replies, rejections, deadlines — sorted by what actually matters |
| **Every Sunday, 10:00 AM** | Your weekly scoreboard: applications, response rates, a real funnel, and week-over-week trend |

No dashboards to babysit. No spreadsheet to update by hand. It just... knows.

---

## 🔍 What it actually catches

```
📩 "A Google recruiter contacted you"        →  🚨 flagged, summarized, linked
📩 "10 jobs you might like"                  →  🗑️  silently ignored
📩 "Thank you for applying to Acme Corp"     →  ✅ logged as a new application
📩 Interview invite, 3rd message in a thread →  🧵 tracked as ONE event, not three
📩 "Unfortunately, we've moved forward..."   →  ❌ logged as a rejection
```

It doesn't grep for keywords — it reads the email the way you would, understands context, and tells the difference between noise and signal.

---

## 🧠 How it works

```
        ⏰ scheduled trigger (cron, your local time)
                    │
                    ▼
        📥 read Gmail — search + fetch threads
           (read-only: no send, no reply, no delete)
                    │
                    ▼
        🧩 classify + extract, semantically
           (company, role, dates, links, stage — never guessed)
                    │
                    ▼
        🧵 thread-aware dedupe
           (one conversation ≠ five separate events)
                    │
                    ▼
        💾 update job-search-tracker.json
           (your permanent, growing job-search history)
                    │
                    ▼
        📊 render the report + publish
```

No servers. No database to host. No API keys to manage beyond the AI platform you're already using. The whole pipeline runs as two scheduled prompts.

---

## 📊 Sample daily report

| Metric | Count |
|---|---:|
| 🏢 Companies applied to | 8 |
| 📝 Applications submitted | 11 |
| 🎤 Interviews | 2 |
| 💻 Assessments | 1 |
| 📩 Recruiters contacted | 5 |
| 💬 Recruiters responded | 3 |
| ❌ Rejections | 2 |
| 🎉 Offers | 0 |

Plus: direct links to the *exact* email thread for every item — not just "check your inbox."

## 📈 Sample weekly funnel

```
Applications Submitted ██████████████████████████████████████████████ 47
Recruiter Responses    ████████████                                   12
Interviews              ███████                                        7
Technical Assessments   █████                                          5
Final Interviews        ██                                             2
Offers                  █                                              1
```

Real numbers, traced back to real emails. Never estimated, never smoothed.

---

## 🔒 Privacy first

- **Read-only, always.** No send, reply, delete, archive, or label — v1 physically cannot touch your inbox, only read it.
- **Nothing invented.** If a fact isn't clearly in the email (a meeting link, a "no response" verdict, a stat from too small a sample), it's left blank or flagged — never guessed.
- **Your data stays yours.** Everything lives in one JSON file you control. No third-party database, no external server.

## 💰 Cost

**$0/month.** No hosting, no database, no separate LLM API bill — it rides entirely on the AI assistant platform you're already running it in.

---

## 🚀 Setup

1. Connect a read-only email tool in your AI assistant environment.
2. Drop in an empty `job-search-tracker.json` using the schema in this repo (dummy example included).
3. Create two scheduled tasks pointing at [`daily_prompt.md`](./daily_prompt.md) and [`weekly_prompt.md`](./weekly_prompt.md) — set your own cron time and timezone.
4. Approve the mailbox read tools once on first run so future runs don't stall on a permission prompt.
5. Wake up. Read your report. Never dig through your inbox again.

## 🛠️ Customize it

- **Schedule/timezone** — just edit the cron expression.
- **Classification categories** — add or remove stages to match how you actually job hunt.
- **Delivery** — swap the "publish" step for email, Slack, a dashboard, whatever you've got — keep the read-only guarantee.

> ⚠️ Heads up: this only sees what shows up in email. Applications through channels that never send a confirmation (some LinkedIn Easy Applies, for instance) won't be tracked — the report will say so rather than pretend otherwise.

---

## 📄 License

MIT — fork it, remix it, make it yours.

<div align="center">

*Built because "just check your email" is not a job-search strategy.*

</div>
