# Expense Tracking

Expenses let you record project costs — cover design, editing, printing, marketing — that reduce the royalty pool before payments are calculated. This is particularly relevant for titles using **net receipts** royalty formulas.

## How Expenses Affect Royalties

Expenses are only deducted from royalties for projects whose formula uses **net receipts** as the price basis. If a project's formula is based on **list price**, expenses are tracked for record-keeping but do not reduce the royalty calculation.

For net-receipts projects, the system supports two deduction modes depending on whether the expense has a **quantity**:

### Per-Project (Cost Recovery)

Expenses recorded **without a quantity** are deducted in full from the project's royalty pool, similar to how advances work. The expense must be "earned out" before royalties flow to holders.

This is appropriate for one-time fixed costs like cover design, editing, and marketing.

**Example**: A project has $500 in lifetime earnings, $200 in lump-sum expenses, and one royalty holder with a 50% share:

| | Amount |
|---|---:|
| Gross Project Earnings | $500.00 |
| Project Expenses | -$200.00 |
| **Net Pool** | **$300.00** |
| Holder's Share (50%) | $150.00 |
| Less Advances | -$100.00 |
| **Balance Due** | **$50.00** |

### Per-Unit (Variable)

Expenses recorded **with a quantity** are amortized over actual units sold. Only the portion corresponding to copies that have actually sold is deducted — the remainder applies to future sales as they occur.

This is appropriate for variable costs tied to physical inventory, like printing and shipping a batch of books to a distributor.

**Example**: You ship 100 copies to Ingram at a total cost of $500 ($5.00/unit). During a statement period, 5 copies sell:

| | Amount |
|---|---:|
| Effective Expense (5 of 100 units) | $25.00 |
| *Remaining (95 units, applied to future sales)* | *$475.00* |

When the next 20 copies sell, an additional $100.00 (20 x $5.00) is deducted. The full $500 is only deducted once all 100 copies have sold. If sales exceed the expense quantity, the deduction is capped at the original expense amount.

If the expense is scoped to a specific **sales channel**, only sales through that channel count toward the unit tally.

### Both Modes Together

A project can have a mix of lump-sum and per-unit expenses. Each is calculated according to its own mode, and the totals are combined:

| Expense | Mode | Deducted |
|---|---|---:|
| Cover design ($1,500) | Cost recovery (no qty) | $1,500.00 |
| Ingram print run ($500 / 100 copies, 5 sold) | Per-unit | $25.00 |
| **Total Effective Expenses** | | **$1,525.00** |

Each royalty holder's share of the total effective expenses is proportional to their royalty share percentage.

If total expenses exceed earnings, the project has not yet "earned out" and the holder receives nothing until cumulative earnings surpass cumulative expenses and advances.

## Expense Categories

Each expense is assigned a category:

| Category | Examples |
|---|---|
| **Production** | Cover design, interior layout, typesetting, indexing |
| **Editorial** | Freelance editing, proofreading, copyediting |
| **Marketing** | Ad spend, ARCs, press releases, review copies |
| **Distribution/Fulfillment** | Shipping, printing costs, fulfillment fees |
| **Other** | Miscellaneous costs |

## Recording an Expense

Every expense is attached to a specific **project**. Required fields:

- **Project**: The title the expense applies to.
- **Description**: A short description (e.g., "Cover design by Jane Smith").
- **Category**: One of the categories above.
- **Amount**: The total invoice amount. This is always the full cost — if you paid $500 to print and ship 100 copies, enter $500 as the amount and 100 as the quantity.
- **Effective Date**: When the expense was incurred.

Optional fields:

- **Quantity**: Number of units (e.g., copies printed or shipped). When set, the expense uses per-unit amortization instead of cost recovery. The system calculates the per-unit cost automatically (`amount / quantity`).
- **Sales Channel**: For channel-specific expenses (e.g., printing costs through Ingram). When a per-unit expense is scoped to a channel, only sales through that channel count toward the units-sold tally.
- **Notes**: Any additional details or context.

Expenses can be managed via the API. See the [API Reference](api.md#expenses) for details, or use the command-line client:

```bash
# List all expenses
saggingroyals expenses list your-slug

# List expenses for a specific project
saggingroyals expenses list your-slug --project my-book

# Record a lump-sum expense (cost recovery)
saggingroyals expenses create your-slug --project my-book \
    --description "Cover design" --category production \
    --amount 1500.00 --date 2025-03-15

# Record a per-unit expense (amortized over units sold)
saggingroyals expenses create your-slug --project my-book \
    --description "Ingram print run" --category distribution_fulfillment \
    --amount 500.00 --quantity 100 --date 2025-03-01

# Delete an expense
saggingroyals expenses delete your-slug 42
```

## Expenses on Royalty Statements

When royalty statements are generated for a project with net-receipts royalties, expenses appear as itemized deductions. Each statement shows:

- An itemized list of expenses (date, category, description, amount) for the project.
- For per-unit expenses, the effective deduction based on actual units sold during the period.
- The holder's proportional share of total effective expenses.
- The net balance after earnings, expenses, and advances are accounted for.

## Auditing

Before generating royalty statements, verify that expenses are recorded correctly. Like sales data and royalty configuration, expense accuracy directly affects royalty calculations. Review the expense list for each project to confirm amounts, dates, categories, and quantities are correct.
