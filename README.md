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
