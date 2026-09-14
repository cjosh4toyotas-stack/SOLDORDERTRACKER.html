# Sold Order Tracker — McGrath Toyota

Single-page GitHub Pages site for tracking new-vehicle sold orders by model and checking that they're being filled in date order.

## Setup
1. Push this folder to a GitHub repo (e.g. `sold-order-tracker`).
2. Settings → Pages → Deploy from branch → `main` / root.
3. Open `https://<user>.github.io/<repo>/`.

## Updating orders
Export each tab of the NEW VEHICLE ORDERS 2026 sheet as CSV and drop it into `data/` with the same file name (`4RUNNER.csv`, `CAMRY.csv`, `CROWN.csv`, `GRAND_HIGHLANDER.csv`, `HIGHLANDER.csv`, `SIENNA.csv`, `TACOMA.csv`, `TUNDRA.csv`). No rebuild — the page reads the CSVs directly. To add a model, add a line to `MODELS` at the top of the script in `index.html`.

## Marking orders filled / skipped
Click a row → pick Open / Filled / Skipped, add the stock # or VIN it was filled with, date and a note. Statuses save in the browser. To carry them across devices or share with the desk, click **Export status.json** and commit the file to the repo root — the page merges it on load (newest edit wins). Orders whose notes contain "SKIP" default to Skipped until you set them.

## Inventory cross-reference
Paste or upload the Inventory Summary export in the right-hand panel. Units are matched to orders by model code, and to a specific customer when their last name appears in Res. / Presold / Comments. Each unit shows who it's assigned to, or the next open orders in line for that model code. A red warning means the assigned order is newer than open orders for the same code. Column detection is automatic; open "Column mapping" if a column was guessed wrong. Inventory stays in the browser only.

## Order check column
Within each model, orders are sequenced by order date (URGENT/PRIORITY first). A filled order is flagged **⚠ ahead of N older open** when older open orders share its model code (primary or secondary). Hover the pill to see who was passed over.
