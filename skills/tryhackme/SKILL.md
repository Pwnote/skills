---
name: tryhackme
description: Use whenever the user is working through a TryHackMe (THM) room — taking structured notes per task, writing a public-facing writeup or blog post, tracking flags, or dealing with THM-specific tooling (AttackBox, OpenVPN connection issues). Trigger on "TryHackMe", "THM room", "writeup for [room name]", or "walkthrough", even without the word "skill".
---

# TryHackMe Workflow

Reference for taking notes through a THM room and producing either private working notes or a public-facing writeup/blog post.

## 1. Room Note Structure

Mirror THM's own task breakdown so notes stay easy to cross-reference against the room page. One doc per task group (maps to pwnote `docs`):

```
00_Room_Overview      — room name, difficulty, tags, learning objectives
01_Task_1_[name]
02_Task_2_[name]
...
NN_Root_Flag / NN_Wrap_Up
```

Within each task doc, log:
- The task's question(s) as headings
- Commands run + output (`command-output` blocks)
- Reasoning for why a step was taken — this is what makes notes useful for review later, not just a command transcript

## 2. Writeup Format (Public / Blog-Style)

THM writeups are commonly shared publicly (blog, LinkedIn, YouTube), so default to a teaching-oriented format rather than a bare answer key — this fits a mentorship/lecturer context well:

```
# TryHackMe: [Room Name] — Writeup

## Room Info
- Difficulty:
- Category/Tags:
- Link:

## Objective
[what the room teaches]

## Enumeration
[methodology explanation, not just command dump — explain *why* each step was taken]

## Exploitation
[same — explain the vulnerability class, not just "run this exploit"]

## Privilege Escalation
[explain the misconfiguration/technique class]

## Lessons Learned
[what this room teaches that's transferable to other boxes/real engagements]
```

- Redact actual flag values in public writeups (`THM{redacted}` or similar) — most THM rooms prohibit publishing flags verbatim in their room rules; check the specific room's policy.
- Favor explaining *why* a technique works over just listing commands — this is what separates a useful teaching writeup from a copy-paste answer key, and matters if writeups are used in a teaching/lecture context.

## 3. Flag Tracking

Use a `checklist` block per room:

```json
{
  "title": "Room Flags",
  "items": [
    { "text": "Task 1 flag", "done": false },
    { "text": "Task 2 flag", "done": false },
    { "text": "Root flag", "done": false }
  ]
}
```

## 4. THM-Specific Tooling Notes

- **AttackBox vs own VPN**: AttackBox is browser-based and simpler but has resource/time limits; own-VPN via OpenVPN config gives full control but requires split-tunnel awareness so you don't route all traffic through the THM VPN unintentionally.
- **Connection troubleshooting**: most THM connectivity issues are stale VPN config expiry (re-download the `.ovpn` file) or MTU mismatches on some networks — note this before assuming a room-specific issue.
- **Room reset**: some rooms need an explicit VM reset if state gets corrupted mid-task; note the reset button location per room type (some are on the room page, some inside the room's "Machine" tab).
