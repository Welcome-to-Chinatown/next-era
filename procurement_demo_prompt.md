# Procurement demo — the prompt (for the recorded demo)

Upload `procurement_inventory.csv`, then paste this into Claude.

---

**Role and goal.** You are my operations assistant for a small café. I am giving you my inventory as a CSV. I want two things from it: a clear reorder dashboard I can look at, and reorder emails I can send today.

**Steps.**
1. Read the CSV. Flag every item where on_hand is below par_level.
2. For each flagged item, calculate units to order to reach par (par_level minus on_hand) and the reorder cost (units to order times unit_cost).
3. Group the flagged items by supplier.
4. Build the dashboard, then write the emails.

**Output.**
- First, a single-page dashboard as an artifact. Include: total items tracked, number of items below par, total reorder cost across all suppliers, a bar chart of reorder cost by supplier, and a table of every below-par item with its supplier, on hand, par, units to order, and cost. Make it clean and easy to read.
- Then, one reorder email per supplier, addressed to that supplier's email from the file. Each email lists the items to reorder and the quantity to bring each back to par, in a warm and professional tone, and asks for delivery within that supplier's lead time.

**Eval.** Before you finish, check three things: every below-par item shows up once under the correct supplier in both the dashboard and an email; units to order equals par minus on hand for each item; and the reorder cost totals match between the table and the chart.

---

## What it should produce (so you know the demo worked)
- A dashboard artifact with ~15 below-par items, reorder cost grouped across 6 suppliers, and one bar chart.
- Six reorder emails: Dairyland USA, Counter Culture Coffee, Baldor Specialty Foods, King Arthur Baking, Restaurant Depot, Chef's Warehouse.
- Burrata (Chef's Warehouse) is at 0 on hand — a good "we are out" moment to point at on camera.
