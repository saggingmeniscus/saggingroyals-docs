# Managing Your Catalog

Your **Catalog** is the definitive list of all your titles with their specific publications in particular formats, with their identifying ISBNs.

## Adding Books

Currently, books can be added to the catalog in the publisher portal, either one at a time or en masse by importing a CSV document. 

## Managing Contributors and Royalty Holders

Royalty holders are the individuals or entities that receive payments. They can be added individually or imported in bulk.

1.  **Contributors**: People listed on the book cover (author, editor, illustrator). They are metadata.
2.  **Royalty Holders**: People who get paid. Often the same as contributors, but not always (e.g., an estate, or agent).

---

## Royalty Formulas & Shares

The system uses a two-step process to calculate royalties:
1.  **Formula**: Determines the total royalties owed for a sale, based on rules.
2.  **Shares**: Splits that total among beneficiaries.

### 1. Formula Builder

Click **Manage Formula** on a Project page to configure how royalties are generated. The system uses a visual builder that lets you define rules for different formats (Paperback, Ebook, etc.).

For each format you want to configure:

1.  **Select the Format**: Check the box next to the format name (e.g., "Paperback") to expand its settings. (Note that if you want to apply the same formula to both paperback and hardcover, you can select "All Print Formats" rather than duplicating the formula.)
2.  **Set Price Basis**: Choose what the royalty is calculated on:
    *   **US List Price**: Based on the domestic list price.
    *   **Regional List Price**: Based on the list price in the currency of the sale.
    *   **Net Receipts**: Based on the amount actually received from the retailer.
3.  **Tiers (Optional)**: If royalties increase after a certain number of copies sold:
    *   Click `+ Add Tier`.
    *   Enter the quantity (e.g., 2500) and the percentage for that bracket. The tier will apply  until that quantity has been reached; then the next tier, if any, or the final rate will apply.
4.  **Final Rate**: Enter the standard royalty percentage that applies after any tiers are exhausted (or for all sales if no tiers are used).

#### Discount Rules
You can add exceptions for deeply discounted sales (common in distribution contracts).
*   Click `+ Add Discount Rule`.
*   Set the threshold (e.g., "If Discount > 55%").
*   Configure a different Price Basis and Percentage for these sales.

*Note: The system processes these rules for every sale line item. If a sale matches a Discount Rule, that rule takes precedence over the standard royalties.*

### 2. Assigning Shares

Click **Manage Shares** to determine who receives the calculated royalty.
-   You can add multiple Royalty Holders.
-   Total Percentage must equal 100%.
-   If you only have one payee (e.g. the Author), assign them `100%`.
-   If an Agent takes 15% and Author takes 85%, add both entries accordingly.

