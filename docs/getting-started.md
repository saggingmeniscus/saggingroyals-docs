# Getting Started

Welcome to Sagging Royalties! We are currently in an invite-only phase. This guide will walk you through the process of getting your press set up on the platform.

At this time, there is no public self-service sign-up form. To create a new publisher account,  contact Sagging Royalties staff, and we'll set you up.

Email [support@saggingroyals.com](mailto:support@saggingroyals.com) with the following information:

*   **Publisher Name**: The official name of your press.
*   **Contact Email**: The primary email address for administrative notifications.
*   **Website**: Your press's website URL.
*   **Admin User**: The name and email address of the person who will be the primary administrator.

Also let us know how you calculate royalties and what your sources of sales and payment data are.
Once we receive your request, we will:

*  Create your **Publisher** entity in the system.
*  Create your **Admin User** account.
*  Send you an invitation email to set your password and log in.

Once you receive your invitation email, click the link to set your password. You can then log in at:
[https://saggingroyals.com/login](https://saggingroyals.com/login)

After logging in to the dashboard, complete these initial setup steps:

### Check Your Publisher Settings
Click the **Settings** tab (or gear icon) to review your profile.

*   **Logo**: Upload your press logo, which will appear on royalty statements and elsewhere.
*   **Contact Info**: Ensure your administrative email and website are correct.

### Import Your Catalog
The system needs to know about your books before it can parse sales reports.

1.  Navigate to the **Catalog** tab.
2.  To upload a CSV file containing your ISBNs, titles, and format details, first click on **Export CSV** to get an empty CSV file with the right columns, fill out the spreadsheet, and upload — or you can simply enter them manually. Also, we may be able to populate your catalog for you, if you point us to an appropriate data source.
4.  Once you've entered the basic information, you'll need to add royalty formulas and shares for each title. See [Catalog](catalog.md) for details.

### Set Up Your Sales Channels
Define where your sales data comes from.

1.  Navigate to **Sales Channels**.
2.  Click **Add Channel**.
3.  Select a provider (e.g., **Ingram**, **KDP**, **Asterism**).
    *   *Standard Providers*: Come with pre-built parsing logic.
    *   *Custom*: You can define your own column mappings for other distributors or direct sales.
    *   *Very Custom*: Have a report that needs special parsing? Just let us know and we'll add support for it.
4.  Set the **Update Cadence** (e.g., Monthly) to help you track missing reports. 

##  Upload Sales Reports
Navigate to the **Sales** section to upload a report. See [Uploading Sales](uploading-sales.md) for detailed instructions.

Note: as part of the onboarding process, we can help you with bulk uploads of your historical data. Our [commandline client](api.md) can also be used to upload multiple reports at a time.

## Generate Royalty Reports
Once sales are uploaded and mapped to your catalog:

1.  Navigate to the **Royalties** tab.
2.  Click **Generate Statements**.
3.  Select the **Start Date** and **End Date** for the period (e.g., Jan 1 - Jun 30).
4.  Click **Generate**.
    *   *Processing happens in the background. You will be notified when PDF statements are ready for review.*

## Invite Royalty Holders
You can invite your authors to the portal so they can view their own dashboards.

1.  Go to the **Users** tab.
2.  Click **Invite User**.
3.  Enter their email and select the **Royalty Holder** they represent.
4.  They will receive an email to set their password and access their statements.

## Maintenance

You'll want to upload sales reports as soon as they are available, so royalty holders can see recent behavior. Note also that sales can be entered manually —  direct sales from events, for instance.
