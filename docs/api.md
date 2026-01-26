# API Documentation

Use the Sagging Royalties API to programmatically interact with your data. This is useful for automating the upload of sales reports from your own scripts or systems.

## Overview

*   **Base URL**: `https://saggingroyals.com/api`
*   **Authentication**: All requests must include your API Key in the `X-API-Key` header.
*   **Full Reference**: [Interactive API Documentation](https://saggingroyals.com/api/docs)

## Authentication

Obtain your API Key from your user profile page (https://saggingroyals.com/profile/). Copy it immediately into your password manager or other secure location, as it will only be shown once!

**Header:**
`X-API-Key: <YOUR_API_KEY>`

## Endpoints

### List Channel Types

Retrieve a list of global sales channel types supported by the system (e.g., INGRAM, KDP).

`GET /channel-types`

#### Request

=== "Sagging Royalties Client"
    ```bash
    saggingroyals channels types
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/channel-types
    ```

=== "Python"
    ```python
    import requests
    url = "https://saggingroyals.com/api/channel-types"
    response = requests.get(url, headers={"X-API-Key": "YOUR_API_KEY"})
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    const response = await fetch("https://saggingroyals.com/api/channel-types", {
        headers: { "X-API-Key": "YOUR_API_KEY" }
    });
    console.log(await response.json());
    ```

### List Channels

Retrieve a list of configured sales channels for the publisher. This is useful for validating channel names before uploading reports.

`GET /publishers/{publisher_slug}/channels`

#### Parameters
*   `publisher_slug` (path, string): Your unique publisher identifier.

#### Request

=== "Sagging Royalties Client"
    ```bash
    # List channels for 'sagging-meniscus'
    saggingroyals channels list sagging-meniscus
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/sagging-meniscus/channels
    ```

=== "Python"
    ```python
    import requests

    api_key = "YOUR_API_KEY"
    publisher = "sagging-meniscus"
    url = f"https://saggingroyals.com/api/publishers/{publisher}/channels"

    response = requests.get(url, headers={"X-API-Key": api_key})
    response.raise_for_status()
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    const apiKey = "YOUR_API_KEY";
    const publisher = "sagging-meniscus";
    const url = `https://saggingroyals.com/api/publishers/${publisher}/channels`;

    const response = await fetch(url, {
        headers: { "X-API-Key": apiKey }
    });
    const data = await response.json();
    console.log(data);
    ```

#### Response
```json
[
  {
    "id": 1,
    "name": "Ingram",
    "slug": "ingram",
    "type": {
      "code": "INGRAM",
      "name": "Ingram CoreSource"
    },
    "update_cadence": "monthly"
  },
  {
    "id": 2,
    "name": "Direct Sales",
    "slug": "direct-sales",
    "type": {
      "code": "CUSTOM",
      "name": "Custom Channel"
    },
    "update_cadence": "weekly"
  }
]
```

### Upload Sales Report

To upload a CSV or Excel sales report for processing:

`POST /publishers/{publisher_slug}/upload-sales-report`


#### Parameters

*   `publisher_slug` (path, string): Your unique publisher identifier (e.g., `sagging-meniscus`).
*   `channel` (form, string): The source of the report. Must be the name of one of your defined channels.
*   `file` (file): The report file itself.
*   `period_start` (form, date, optional): `YYYY-MM-DD`.
*   `period_end` (form, date, optional): `YYYY-MM-DD`.

#### Examples

=== "Sagging Royalties Client"

    The easiest way to upload files is using our official CLI tool.
    
    ```bash
    # Set your API Key
    export SAGGINGROYALS_API_KEY="your-api-key"

    # Upload a file
    saggingroyals upload-sales your-slug Ingram ./2025-10-IsdSales.csv
    ```

=== "cURL"

    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/upload-sales-report" \
      -H "X-API-Key: your-api-key" \
      -F "channel=Ingram" \
      -F "file=@./2025-10-IsdSales.csv"
    ```

=== "Python"

    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/upload-sales-report"
    headers = {"X-API-Key": "your-api-key"}
    data = {"channel": "Ingram"}
    files = {"file": open("2025-10-IsdSales.csv", "rb")}

    response = requests.post(url, headers=headers, data=data, files=files)
    print(response.json())
    ```

=== "JavaScript"

    ```javascript
    const apiKey = "your-api-key";
    const publisher = "your-slug";
    const url = `https://saggingroyals.com/api/publishers/${publisher}/upload-sales-report`;

    const formData = new FormData();
    formData.append("channel", "Ingram");
    formData.append("file", fileInput.files[0]);

    const response = await fetch(url, {
        method: "POST",
        headers: { "X-API-Key": apiKey },
        body: formData
    });
    
    const result = await response.json();
    console.log(result);
    ```

#### Response

```json
{
  "status": "success",
  "message": "Report processed successfully",
  "data": {
    "rows_processed": 150,
    "net_revenue": 1250.50
  }
}
```

### Get Project Details

Retrieve metadata for a specific project.

`GET /publishers/{publisher_slug}/projects/{project_slug}`

#### Parameters
*   `publisher_slug` (path, string): Your unique publisher identifier.
*   `project_slug` (path, string): The project's identifier (e.g., `the-great-gatsby`).

#### Request

=== "Sagging Royalties Client"
    ```bash
    # See client documentation for project subcommands
    # saggingroyals catalog --help
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby
    ```

=== "Python"
    ```python
    import requests

    api_key = "YOUR_API_KEY"
    url = "https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby"

    response = requests.get(url, headers={"X-API-Key": api_key})
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    const response = await fetch("https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby", {
        headers: { "X-API-Key": "YOUR_API_KEY" }
    });
    const data = await response.json();
    console.log(data);
    ```

### List Royalty Statements

Retrieve a list of generated royalty statements.

`GET /publishers/{publisher_slug}/statements`

#### Parameters
*   `publisher_slug` (path, string): Your unique publisher identifier.

#### Request

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties statements list your-slug
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/statements
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/statements"
    response = requests.get(url, headers={"X-API-Key": "YOUR_API_KEY"})
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    const response = await fetch("https://saggingroyals.com/api/publishers/your-slug/statements", {
        headers: { "X-API-Key": "YOUR_API_KEY" }
    });
    const data = await response.json();
    console.log(data);
    ```

### Download Statement PDF

Download the PDF file for a specific statement.

`GET /publishers/{publisher_slug}/statements/{statement_id}/download`

#### Parameters
*   `publisher_slug` (path, string): Your unique publisher identifier.
*   `statement_id` (path, integer): The ID of the statement to download.

#### Request

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties statements download your-slug 123 --out statement.pdf
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         -O -J \
         https://saggingroyals.com/api/publishers/your-slug/statements/123/download
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/statements/123/download"
    response = requests.get(url, headers={"X-API-Key": "YOUR_API_KEY"})
    
    with open("statement.pdf", "wb") as f:
        f.write(response.content)
    ```

=== "JavaScript"
    ```javascript
    const response = await fetch("https://saggingroyals.com/api/publishers/your-slug/statements/123/download", {
        headers: { "X-API-Key": "YOUR_API_KEY" }
    });
    const blob = await response.blob();
    // Use URL.createObjectURL(blob) to display or download in browser
    ```
