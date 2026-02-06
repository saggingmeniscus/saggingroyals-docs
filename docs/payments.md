# Payments

Sagging Royalties tracks two distinct types of payments:

1. **Incoming payments** — money your press receives from sales channels (distributor payouts).
2. **Outgoing royalty payments** — money you pay to your authors and other royalty holders.

Both types feed into royalty calculations and appear on royalty statements.

## Incoming Payments (from Channels)

Sales channels like Ingram, KDP, and Asterism periodically pay you for copies sold. These incoming payments are important because they establish the actual exchange rates and payout amounts your press received, which in turn affect net-receipts royalty calculations.

### Why Track Incoming Payments?

Many channels report sales in one currency but pay out in another. For example, Ingram may report sales in GBP or EUR but pay you in USD. The system uses payment data to calculate the effective exchange rate and convert sales figures to accurate USD amounts.

Without payment data, the system can only estimate net receipts from the sales reports themselves. With payment data, it can compute the true per-unit payout.

### Uploading Payment Reports

Some channels provide separate payment reports (distinct from their sales reports). To upload one:

1. Navigate to **Upload Reports** in the publisher portal.
2. Click **Upload Payment Report**.
3. Select the **Channel**.
4. Choose the file and click **Upload**.

The system will parse the payment data and link it to the corresponding sales records for that channel and period.

You can also upload payment reports via the CLI:

```bash
saggingroyals payments upload your-slug ingram ./ingram-payment-2025-03.csv
```

### Recording Payments Manually

If a channel pays you outside of a formal report (e.g., a direct deposit without a corresponding file), you can record the payment manually:

1. Use the API or CLI to add a payment record:

```bash
saggingroyals payments add your-slug --channel ingram --amount 1234.56 --date 2025-03-31
```

### Viewing the Payment Ledger

The payment ledger shows all incoming payments across your channels. You can filter by channel and date range.

```bash
saggingroyals payments list your-slug --channel ingram
```

### Data Freshness

The publisher dashboard tracks both sales report and payment report coverage per channel. If a channel's payment data is out of date, the dashboard will flag it so you know to upload the latest payment report.

## Outgoing Royalty Payments (to Holders)

When you pay an author or other royalty holder, record it in the system so that the balance is tracked accurately.

### Project-Linked Payments (Advances)

A payment linked to a specific project acts as an **advance** against that project's future royalties. The advance is deducted from that project's earned royalties when calculating the holder's balance.

For example, if you give an author a $500 advance on their book, record it as a payment linked to that project. The system will subtract that $500 from the project's royalty earnings before determining what's still owed.

### General Payments

A payment recorded without a project link is a **general payment**. It is subtracted from the holder's total balance across all projects. Use this for payments that aren't tied to a specific title.

### Recording a Royalty Payment

In the publisher portal:

1. Navigate to **Royalties > Record Payment**.
2. Select the **Royalty Holder**.
3. Enter the **Amount** and **Date**.
4. Optionally link the payment to a **Project** (to make it an advance).
5. Add any **Notes** (e.g., check number, payment method).
6. Click **Save**.

Or via the CLI:

```bash
# Record a project-linked advance
saggingroyals royalties payments create your-slug --holder-id 1 --amount 500.00 --date 2025-01-15

# With notes
saggingroyals royalties payments create your-slug --holder-id 1 --amount 500.00 --date 2025-01-15 --notes "Check #1234"
```

### How Payments Affect the Balance

The royalty balance calculation works as follows:

For each project the holder has a share in:

```
Project Balance = Earned Royalties - Advances - Expenses
```

Only positive project balances count (a project that hasn't earned out doesn't drag down other projects). The total balance due is:

```
Balance Due = Sum of positive project balances - General Payments
```

### Viewing Payment History

You can see all outgoing payments on the **Royalty Report** page, which shows each holder's total earned, total paid, and balance due. The **Royalty Holder Detail** page breaks this down by project.

```bash
saggingroyals royalties payments list your-slug
```

## Payments on Statements

Royalty statements include a financial summary that tracks the running balance:

```
Balance Forward:       $100.00
(+) Net Earnings:      $250.00
(-) Expenses:          ($50.00)
(-) Payments Made:     ($75.00)
(=) Closing Balance:   $225.00
```

Payments made during the statement period are itemized so the holder can see each payment's date and amount. See [Royalty Statements](statements.md) for more on generating statements.
