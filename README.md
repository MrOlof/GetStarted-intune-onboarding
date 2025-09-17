# DayOne – Intune Onboarding Assistant

*Auto-starts at first logon, enforces user MFA registration, shows live app install status, and links to Microsoft 365 on the web so users can work while heavy apps finish. Goal: zero Service Desk on Day 1.*

---

Example (old version)

![Animation](https://github.com/user-attachments/assets/98769eb9-0b5c-44e2-87e7-63e1d7bbcb7e)


## Why

- New hires get stuck on MFA and first-run junk.  
- ESP blocking on big apps slows Autopilot.  
- DayOne fixes it: let them sign in and get a nice Get Started guide for setting up the basics. Removing servicedesk to help user with common tasks. More tasks can be added easily.

---

## What it does

- **First-logon auto-launch** (user context).
- **MFA gate**: opens Security Info and won’t continue until registered.
- **Install status**: surfaces *Installing / Installed / Failed* for Intune / Company Portal / winget apps.
- **Get to work**: Outlook, Teams, OneDrive **web** links while apps finish.
- **Clean exit** when requirements are met. *(Optional: remove user from the exclusion group via Graph.)*

---

Typical flow:

Conditional Access / MFA
Use a dynamic 24h MFA-exclusion only to allow first sign-in.
Allows user to sign in without MFA first day
Get Started will guide the user to setup MFA amongst other company related tasks or information

