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

### Polymorphic Spam Detection
Catches spam even when the spammer adds emojis, strips punctuation, or changes capitalisation to bypass exact hash detection. Uses cosine similarity on token frequency maps.

https://github.com/user-attachments/assets/6fdd30f7-a273-4f01-827d-c2e76520e85c

---

### Admin Dashboard and Slash Commands
Live flagged user tracking with Moderation Level status, flag count, and vouch functionality. Admins can also query user status directly through slash commands from the admin channel.

https://github.com/user-attachments/assets/0b759b55-2d1a-46c6-a955-48938ef77705

---

### Bot Notifications and Timeout Enforcement
When a user triggers detection, the bot pings them directly with a warning or timeout notice based on their current Moderation Level. Messages from restricted users are silently dropped in the beforeSave hook — never written to the database, never broadcast.

https://github.com/user-attachments/assets/07a4d99f-fcec-414c-8bdb-ad08d67b485e

---

## Features

**Detection Pipeline**
- Exact duplicate detection via hash matching with an in-memory LRU cache and configurable sliding window
- Polymorphic spam detection using cosine similarity on tokenized word frequency maps
- Cross-channel flood detection tracking message spread across 3 or more channels within the sliding window

**Moderation Level System**
- Four-tier graduated response: DM warning → 1 min cooldown → 10 min restriction → permanent block pending admin review
- Levels persist across cooldowns, repeat offenders escalate naturally
- Only an admin vouch resets a user back to zero

**Admin Control**
- Private admin channel created on install with all alerts and flagged user notifications
- Dashboard showing flagged users, Moderation Level, flag count, and cooldown status
- Slash commands for querying user status directly from the admin channel
- Configurable settings: monitoring window, sliding window duration, cross-channel threshold

---

## Installation

```bash
# Clone the repository
git clone <repository-url>
cd new-users-anti-spam

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

---

## Project Context

This app is being developed as part of **Google Summer of Code 2025** under the Rocket.Chat organization.

**Mentors:** Gabriel Casals, Alfredo Del Fabro Neto

---

## License

MIT
