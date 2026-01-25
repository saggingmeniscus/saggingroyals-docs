# API Documentation

Use the Sagging Royalties API to programmatically interact with your data. This is useful for automating the upload of sales reports from your own scripts or systems.

## Overview

*   **Base URL**: `https://saggingroyals.com/api`
*   **Authentication**: All requests must include your API Key in the `X-API-Key` header.
*   **Full Reference**: [Interactive API Documentation (Swagger/ReDoc)](https://saggingroyals.com/api/docs)

## Authentication

Obtain your API Key from your user profile page (https://saggingroyals.com/profile/).

**Header:**
`X-API-Key: <YOUR_API_KEY>`

## Endpoints

### Upload Sales Report

Upload a CSV or Excel sales report for processing.

`POST /publishers/{publisher_slug}/upload-sales-report`

#### Parameters

*   `publisher_slug` (path, string): Your unique publisher identifier (e.g., `sagging-meniscus`).
*   `channel` (form, string): The source of the report. Must be one of:
    *   `Asterism`
    *   `Ingram`
    *   `KDP`
    *   `Draft2Digital`
    *   `Snipcart`
    *   `Brookside`
    *   `Gazelle`
    *   `EBSCO`
    *   `Direct`
    *   `SPD`
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
    files = {"file": open("./2025-10-IsdSales.csv", "rb")}

    response = requests.post(url, headers=headers, data=data, files=files)
    print(response.json())
    ```

=== "JavaScript"

    ```javascript
    const formData = new FormData();
    formData.append("channel", "Ingram");
    formData.append("file", fileInput.files[0]);

    fetch("https://saggingroyals.com/api/publishers/your-slug/upload-sales-report", {
      method: "POST",
      headers: {
        "X-API-Key": "your-api-key"
      },
      body: formData
    })
    .then(response => response.json())
    .then(data => console.log(data));
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
