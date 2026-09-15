# Sold Order Tracker — McGrath Toyota

Single-page GitHub Pages site for tracking new-vehicle sold orders by model and checking that they're being filled in date order.

## Setup
1. Push this folder to a GitHub repo (e.g. `sold-order-tracker`).
2. Settings → Pages → Deploy from branch → `main` / root.
3. Open `https://<user>.github.io/<repo>/`.

## Updating orders
Export each tab of the NEW VEHICLE ORDERS 2026 sheet as CSV and drop it into `data/` (or next to `index.html` at the repo root) with the same file name (`4RUNNER.csv`, `CAMRY.csv`, `CROWN.csv`, `GRAND_HIGHLANDER.csv`, `HIGHLANDER.csv`, `SIENNA.csv`, `TACOMA.csv`, `TUNDRA.csv`). No rebuild — the page reads the CSVs directly. To add a model, add a line to `MODELS` at the top of the script in `index.html`.

## Marking orders filled / skipped
Click a row → pick Open / Filled / Skipped, add the stock # or VIN it was filled with, date and a note. Statuses save in the browser. To carry them across devices or share with the desk, click **Export status.json** and commit the file to the repo root — the page merges it on load (newest edit wins). Orders whose notes contain "SKIP" default to Skipped until you set them.

## Inventory cross-reference

The page loads `inventory.csv` from the repo root automatically — commit each fresh Inventory Summary export under that name. Comments in the form `XX#LASTNAME` (sales initials + customer) are how units get matched to orders; a unit whose code is in the same model family (e.g. a 6722 for a 6724 order) still matches, with an "(ordered …)" note. Reserved units whose name isn't on the order sheet are called out.
Paste or upload the Inventory Summary export in the right-hand panel. Units are matched to orders by model code, and to a specific customer when their last name appears in Res. / Presold / Comments. Each unit shows who it's assigned to, or the next open orders in line for that model code. A red warning means the assigned order is newer than open orders for the same code. Column detection is automatic; open "Column mapping" if a column was guessed wrong. Inventory stays in the browser only.

## Order check column
Within each model, orders are sequenced by order date (URGENT/PRIORITY first). A filled order is flagged **⚠ ahead of N older open** when older open orders share its model code (primary or secondary). Hover the pill to see who was passed over.

## Wait times (`waits.html`)
Linked from the tracker header. Reads the order sheets plus `sales.csv` (the Sales Summary export, RDR rows) and matches each sold order to its RDR by customer name within the model family. Shows typical wait (median) and the middle-half range per trim, the last-90-day trend, a month-by-month chart, and who is still waiting versus the typical wait. `inventory.csv` adds the "filled, not delivered" stage (unit reserved, on lot / in transit / allocated). Refresh by committing a new `sales.csv`.

The tracker also reads `sales.csv`: any order matched to an RDR shows as DELIVERED automatically, and the order check treats it as filled.
