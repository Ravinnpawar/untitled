# PG Manager

An all-in-one dashboard for **PG (paying-guest) / hostel managers and owners** to run
daily operations from a single screen — rooms, tenants, rent, expenses, inventory and
maintenance complaints.

No login, no server, no build step. It's a single self-contained HTML file that runs
entirely in the browser and stores data locally on the device.

## How to use

- **Open it:** double-click `index.html`, or open it in any modern browser.
  (To use it on a phone/tablet on the same network, serve the folder with any static
  server, e.g. `python3 -m http.server` and open the shown address.)
- The app loads with **sample data** so you can explore. Use **Reset Data** in the
  sidebar to clear it and start fresh, or just edit/delete the samples.

## What it does

| Section | What you can do |
|---|---|
| **Dashboard** | Occupancy %, rent collected vs. pending this month, expenses, net balance, and a "Needs attention" list (rent due, low stock, open complaints). Mark rent paid in one click. |
| **Rooms** | Add rooms with floor, type, bed capacity and rent; see live occupancy (vacant / partial / full) and who's in each room. |
| **Tenants** | Add tenants, assign to rooms (rent auto-fills), track phone, deposit, join date, ID proof and status (active / notice / moved out). Searchable. |
| **Rent & Payments** | Per-month rent tracking for every active tenant, record payments (cash/UPI/bank/cheque/card), see collected vs. pending totals. |
| **Expenses** | Log groceries, utilities, salaries, maintenance etc. with a per-category breakdown and monthly filter. |
| **Inventory** | Track stock items with quantity, unit and minimum level; quick +/- adjust and automatic **low-stock alerts**. |
| **Complaints** | Log maintenance issues per room with priority and status (open / in-progress / resolved). |

## Data & backup

- All data is saved in the browser's **localStorage** — it stays on the device and is
  never sent anywhere. Clearing browser data will erase it.
- Use **⬇ Backup** in the sidebar to download a JSON file, and **⬆ Restore** to load it
  back (also handy for moving data between devices).

## Notes

- Currency defaults to `₹` and dates use Indian formatting; both are easy to adjust in
  `index.html` (`settings.currency` and the `en-IN` locale strings).
- Because there is no login yet, treat the device it runs on as trusted. Authentication
  and multi-device sync can be layered on later without changing the data model.

## Tech

Plain HTML, CSS and vanilla JavaScript — zero dependencies. Light/dark theme included.

---

# FOCUS – Reels Control & Study Reminder (`focus/index.html`)

Prototype app for the project **"Impact of Reels and Short Video Addiction on Academic
Concentration Among College Students"** (महाविद्यालयीन विद्यार्थ्यांच्या अभ्यासावरील एकाग्रतेवर
रील्सच्या व्यसनाचा होणारा परिणाम). Same approach as above: one HTML file, no server, data
stays in the browser. Open `focus/index.html` on a phone or laptop.

| Section | Purpose (project objective) |
|---|---|
| **Today · आज** | Study minutes vs. daily goal, reels minutes vs. daily limit, a 0–100 focus score, study streak and a 7‑day study‑vs‑reels chart. Warns when the reels limit is near or crossed. |
| **Focus Timer · अभ्यास** | Pomodoro timer (15/25/45/60 min + break) per subject. Switching away from the tab during a focus block is counted as a distraction. Completed blocks are logged automatically. |
| **Reels Log · रील्स** | Log minutes per app (Instagram Reels, YouTube Shorts, …) with one tap. A browser cannot read phone screen time, so entries are manual (copy from Digital Wellbeing / Screen Time). |
| **Survey · प्रश्नावली** | The research questionnaire (13 bilingual questions: reels time, platform, timing, concentration, sleep, incomplete study, study hours…). Collect responses on one device, see live results incl. a *concentration difficulty vs. daily reels time* table, and export CSV for Excel/Sheets. |
| **Tips · उपाय** | Practical ways to cut screen time and improve study habits. |
| **Settings** | Study goal, reels limit, timer lengths, study‑reminder times and a "phone away" bedtime alert (browser notifications while the tab is open), backup/restore. |

The survey results screen reminds you that conclusions should be drawn only after enough
real responses are collected (प्रत्यक्ष संशोधनानंतरच निष्कर्ष) and that self‑reported data
shows correlation, not cause. No sample/fake responses are included.
