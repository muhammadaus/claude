# Email & LinkedIn Message Replier

## Purpose
Central inbox for all recruiter messages. Claude reads messages and generates draft replies.

## Quick Commands

```bash
# Fetch LinkedIn messages (saves to inbox/linkedin/)
node fetch-linkedin.js 10

# Fetch emails from Yahoo & iCloud (saves to inbox/email/)
node fetch-emails.js 5

# Fetch both
node fetch-linkedin.js 10 && node fetch-emails.js 5
```

## Folder Structure
```
Email-replier/
├── inbox/
│   ├── linkedin/     # Auto-fetched LinkedIn messages
│   └── email/        # Auto-fetched emails
├── drafts/           # Generated draft replies
├── sent/             # Archive of sent messages
├── fetch-linkedin.js # LinkedIn scraper
├── fetch-emails.js   # Email IMAP fetcher
└── .env              # Email credentials (app passwords)
```

## Setup

### LinkedIn
Uses existing Chrome session from JobSearchAgent. Just run:
```bash
node fetch-linkedin.js 10
```

### Email (Yahoo + iCloud)
1. Create `.env` file with app passwords:
```
YAHOO_EMAIL=aushijri@yahoo.com
YAHOO_APP_PASSWORD=xxxx-xxxx-xxxx-xxxx

ICLOUD_EMAIL=aushijri@icloud.com
ICLOUD_APP_PASSWORD=xxxx-xxxx-xxxx-xxxx
```

2. Generate app passwords:
   - Yahoo: https://login.yahoo.com/account/security/app-passwords
   - iCloud: https://appleid.apple.com/account/manage > App-Specific Passwords

3. Install dependencies:
```bash
npm install imap mailparser puppeteer-extra puppeteer-extra-plugin-stealth
```

---

## My Profile (Muhammad)
- **Role**: Full Stack Developer
- **Status**: Actively looking for new opportunities
- **Japanese**: JLPT N1 (fluent)
- **Location**: Japan
- **Key Skills**: Python, JavaScript/TypeScript, React, Node.js

---

## Message File Format

### LinkedIn (`inbox/linkedin/*.txt`)
```
FROM: Recruiter Name
TITLE: Technical Recruiter at Company
PROFILE: https://linkedin.com/in/xxx
FETCHED: 2024-01-15T10:30:00Z
LAST_MESSAGE_FROM_ME: false

--- MESSAGES ---

[1] First message...
[2] Second message...
```

### Email (`inbox/email/*.txt`)
```
FROM: recruiter@company.com
TO: aushijri@yahoo.com
SUBJECT: Exciting Opportunity
DATE: 2024-01-15T10:30:00Z
ACCOUNT: Yahoo

--- BODY ---

Email content here...
```

---

## Response Rules

### SKIP - No Reply Needed
- `LAST_MESSAGE_FROM_ME: true` → Waiting for their reply
- LinkedIn promotional messages
- Spam or irrelevant emails

### Generate Reply For:

#### 1. FIRST CONTACT (Recruiter reaching out)
```
Hi [First Name],

Thank you for reaching out! I'm actively looking for new opportunities and am interested in learning more about this [Job Title] role.

Before we proceed, I'd like to clarify:
• What is the work arrangement? (Remote/Hybrid/On-site)
• Could you share the compensation range?

A bit about me: I'm a Full Stack Developer with experience in modern web technologies. I'm also fluent in Japanese (JLPT N1).

I'm available for a call at your convenience.

Best regards,
Muhammad
```

#### 2. SCHEDULING (Call/meeting request)
```
Hi [First Name],

Yes, I'm available for a call. Here are some times that work for me:
• [Day 1]: [Time range] JST
• [Day 2]: [Time range] JST

Please let me know which works best, or feel free to send a calendar invite.

Best regards,
Muhammad
```

#### 3. INTERVIEW SCHEDULING
```
Hi [First Name],

Thank you for moving forward with the interview process. I'm excited about this opportunity.

I'm available at the following times:
• [Day 1]: [Time range] JST
• [Day 2]: [Time range] JST
• [Day 3]: [Time range] JST

Please let me know which slot works best.

Best regards,
Muhammad
```

#### 4. JOB DETAILS (JD shared)
```
Hi [First Name],

Thank you for sharing the details about this role.

The position sounds interesting. I have a few questions:
• What is the work arrangement? (Remote/Hybrid/On-site)
• Could you share the compensation range?
• What does the team structure look like?

I'd be happy to discuss further on a call.

Best regards,
Muhammad
```

#### 5. SALARY DISCUSSION
```
Hi [First Name],

Thank you for sharing the compensation details.

Based on my experience and the market rate for this role, I was expecting something in the range of [EXPECTED_RANGE].

I'm open to discussing this further. Could we schedule a call to align on expectations?

Best regards,
Muhammad
```

#### 6. FOLLOW-UP
```
Hi [First Name],

Thank you for following up! Yes, I'm still very interested in this opportunity.

[Add pending questions if not yet answered]

Looking forward to the next steps.

Best regards,
Muhammad
```

#### 7. QUESTION (They asked something)
Read the question and provide a direct answer based on my profile.

---

## How to Use

1. **Fetch messages**:
   ```bash
   node fetch-linkedin.js 10
   # Or AirDrop email PDFs from iPhone → auto-moves to inbox/email/
   node watch-airdrop.js
   ```

2. **Ask Claude**:
   - "Generate replies for all new messages"
   - "What should I reply to [name]?"
   - "Check inbox and draft responses"

3. **Copy & Send**:
   ```bash
   cat drafts/reply_Name_Company_Role.txt | pbcopy
   ```
   Then paste into email/LinkedIn and send.

---

## Default Behavior (ALWAYS DO THIS)

When generating draft replies, Claude MUST:

1. **Save each draft to `drafts/` folder** with filename format:
   ```
   reply_[FirstName]_[Company]_[Role].txt
   ```
   Examples:
   - `reply_Aroua_enworld_DataAnalyst_Catalina.txt`
   - `reply_Hiroaki_Hays_ModelBasedEngineering.txt`

2. **Use Japanese** if the original message is in Japanese

3. **Show pbcopy command** after saving:
   ```bash
   cat drafts/[filename] | pbcopy
   ```

4. **Never auto-send** - all replies are drafts only

---

## Important Notes
- All replies are DRAFTS - never auto-send
- Always check `LAST_MESSAGE_FROM_ME` before generating reply
- Personalize [bracketed] parts before sending
- Update templates as preferences change
