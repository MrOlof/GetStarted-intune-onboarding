DayOne – Intune Onboarding Assistant

Windows onboarding helper for Microsoft Intune. It auto-starts at first logon, forces MFA registration, shows live app install status, and gives quick links to Microsoft 365 on the web so users can work while heavy apps finish. Goal: zero Service Desk on Day 1.

Why

New hires get stuck on MFA and first-run junk.

ESP blocking on big apps slows Autopilot.

Hand-holding users through MFA wastes time.
DayOne fixes it: let them sign in (24h CA/MFA exclusion), immediately enforce MFA, show progress, move on.

What it does

First-logon auto-launch (user context).

MFA gate: opens Security Info and won’t continue until registered.

Install status: surfaces “Installing / Installed / Failed” for Intune/Company Portal/winget apps.

Get to work: Outlook, Teams, OneDrive web links while apps finish.

Clean exit when requirements are met. (Optional: remove user from the exclusion group via Graph.)

Typical flow
HR sets start date → dynamic group adds user to 24h MFA-exclusion
Autopilot (ESP skips heavy apps) → desktop faster
DayOne starts → enforce MFA → show app installs → M365 Web links
All green → (optional) remove from exclusion → exit

Deploy (short version)

Option A – Win32 app (recommended)

Package with IntuneWinAppUtil: install.ps1 / uninstall.ps1.

Install cmd: powershell.exe -ExecutionPolicy Bypass -File .\install.ps1

Behavior: System (drops per-user launcher via Run key or logon Scheduled Task).

Detection: HKLM\Software\DayOne\Installed=1 (REG_DWORD=1).

Option B – Intune PowerShell script

Upload install.ps1, run 64-bit, as System. Same launcher logic.

Requirements: Windows 10 22H2+ or Windows 11 (x64).

Autopilot / ESP guidance

Keep ESP strict for enrollment/policies only.

Do not block on Microsoft 365 Apps or other heavy LOB packages.

Let DayOne cover the gap with status + web fallback.

Conditional Access / MFA

Use a 24h MFA-exclusion only to allow first sign-in.

DayOne forces registration immediately.

Recommended: automate exclusion removal after success (Graph/Azure Function).

Intune app metadata (copy/paste)

Name: DayOne – Intune Onboarding Assistant

Publisher: YourOrg

Category: Onboarding

Short description: Auto-starts at first logon, enforces MFA, shows live app status, and gets users productive via M365 Web while apps finish.

Logging

%ProgramData%\DayOne\Logs\DayOne-*.log

Verbose: HKLM\Software\DayOne\LogLevel=Verbose
