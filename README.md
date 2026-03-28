<p align="center">
  <img src="./public/logo.png" alt="New Users Anti-Spam System Logo" width="180"/>
</p>

<h1 align="center">New Users Anti-Spam Monitoring System</h1>

<p align="center">
  A proactive, human-validated anti-spam layer for open Rocket.Chat communities.
  <br/>
  Built as a Rocket.Chat App on the Apps Engine.
</p>

---

## Overview

Open community workspaces are increasingly vulnerable to coordinated spam where new accounts join, flood multiple public channels with identical or slightly varied messages, and vanish before any moderator notices. This app shifts moderation from reactive to proactive by monitoring new users during their first 6 to 10 weeks and responding through a graduated, admin-controlled restriction system.

No permanent action ever happens without a human making the final call. Every flag has a reason, every action is reversible, and admins stay in full control throughout.

---

## Demo

### Rate Flood Detection
Catches users sending messages at suspicious velocity regardless of content. Pure speed based detection.

https://github.com/user-attachments/assets/ed709c47-089a-48b3-8e57-6d03c2f7c696

---

### Phishing Link Spam Detection
Flags users sending URL bearing messages across multiple channels within a short window, targeting link dropping and phishing campaigns.

https://github.com/user-attachments/assets/11b98cfe-88ee-4770-acf7-356ba72fc56b

---

### Exact Duplicate Detection
Catches copy paste spam sent across multiple channels within the sliding time window.

https://github.com/user-attachments/assets/5c82b404-caa1-4a41-9dc2-85e93c27c095

---

### Polymorphic Spam Detection
Catches spam even when the spammer adds emojis, strips punctuation, or changes capitalisation to bypass exact hash detection. Uses cosine similarity on token frequency maps.

https://github.com/user-attachments/assets/16f9bdd3-ab04-45d7-9c0a-ba18e160a633

---

### Admin Dashboard and Slash Commands
Live flagged user tracking with Moderation Level status, flag count, and vouch functionality. Admins can also query user status directly through slash commands from the admin channel.

https://github.com/user-attachments/assets/0b759b55-2d1a-46c6-a955-48938ef77705

---

### Bot Notifications and Timeout Enforcement
When a user triggers detection, the bot pings them directly with a warning or timeout notice based on their current Moderation Level. Messages from restricted users are silently dropped in the beforeSave hook — never written to the database, never broadcast.

https://github.com/user-attachments/assets/07a4d99f-fcec-414c-8bdb-ad08d67b485e

---

## Admin Commands

### User Flag Status
Query the current spam status of any user directly from the admin channel.

![User flag status](https://github.com/user-attachments/assets/8f5207fe-e50b-4efd-b8c1-945998fd015f)

---

### Flag History and Chat Lookup
View the full flagged message history for any user with timestamps and channels.

![Chat history](https://github.com/user-attachments/assets/7fb0b397-dc1d-42d3-a34b-40b35d2ebd91)

---

### AI Powered User Summary
Run an on demand AI analysis of any flagged user to get an intelligent summary of their behavior, pattern, and recommended action.

![AI summary](https://github.com/user-attachments/assets/c72f4673-5c1a-42f8-8f54-5f5a4038e7ff)

---

## Features

**Detection Pipeline**
- Exact duplicate detection via normalized hash matching with in-memory cache and configurable sliding window
- Polymorphic spam detection using cosine similarity on tokenized word frequency maps with adaptive thresholds
- Cross-channel flood detection tracking message spread across 3 or more channels
- Rate flood detection based on message velocity within configurable time windows
- Rapid room spread detection for spray and pray patterns across channels
- Phishing link spam detection for URL based campaigns across multiple rooms

**Moderation Level System**
- Four-tier graduated response: DM warning → 1 min cooldown → 10 min restriction → permanent block pending admin review
- Tolerance thresholds between levels so users do not escalate on a single flag
- Levels persist across cooldowns, repeat offenders escalate naturally
- Only an admin vouch resets a user back to zero

**Admin Control**
- Private admin channel created on install with all alerts and flagged user notifications
- Dashboard showing flagged users, Moderation Level, flag count, and cooldown status with vouch functionality
- Full slash command suite: status, vouch, lookup, reset-cooldown, dashboard, help
- AI powered commands: ai summary, ai analyze, ai chaos for on demand intelligent reporting
- Configurable settings: monitoring window, sliding window duration, cross-channel threshold, rate flood limits

---

## Installation

```bash
# Clone the repository
git clone https://github.com/not-meet/Apps.AntiSpammerSystem
cd Apps.AntiSpammerSystem

# Install dependencies
npm install

# Deploy to your Rocket.Chat instance
rc-apps deploy --url <your-rocketchat-url> --username <admin> --password <password>
```

---

## Configuration

Once installed, navigate to the app settings panel to configure:

| Setting | Default | Description |
|---|---|---|
| Monitoring Window | 6 weeks | Duration new users are monitored after joining |
| Sliding Window | 5 minutes | Time window for duplicate and flood detection |
| Cross-Channel Threshold | 3 channels | Minimum channels for flood detection to trigger |
| Rate Flood Limit | 5 / 30s | Message velocity threshold before flagging |

---

## Project Context

This app is being developed as part of **Google Summer of Code 2025** under the Rocket.Chat organization.

**Mentors:** Gabriel Casals, Alfredo Del Fabro Neto

---

## License

MIT
