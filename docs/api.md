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

## Sales Channels

### List Channel Types

Retrieve a list of global sales channel types supported by the system (e.g., INGRAM, KDP).

`GET /channel-types`

**Request**

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

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get("https://saggingroyals.com/api/channel-types", headers=headers)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/channel-types", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### List Channels

Retrieve a list of configured sales channels for the publisher.

`GET /publishers/{publisher_slug}/channels`

**Request**

=== "Sagging Royalties Client"
    ```bash
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

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/sagging-meniscus/channels",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/sagging-meniscus/channels", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Create Sales Channel

Configure a new sales channel.

`POST /publishers/{publisher_slug}/channels`

**Request**
JSON Body: `{"type_code": "INGRAM", "name": "Ingram", "slug": "ingram", "update_cadence": "monthly"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals channels create your-slug --name "Ingram" --slug ingram --type INGRAM
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/channels" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"type_code": "INGRAM", "name": "Ingram", "slug": "ingram"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/channels"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {
        "type_code": "INGRAM", 
        "name": "Ingram", 
        "slug": "ingram"
    }

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/channels", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        type_code: "INGRAM", 
        name: "Ingram", 
        slug: "ingram"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

## Catalog & Projects

### List Projects

List all projects for a publisher.

`GET /publishers/{publisher_slug}/projects`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals catalog list your-slug
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/projects
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/projects", 
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/projects", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Create Project

Create a new project.

`POST /publishers/{publisher_slug}/projects`

**Request**
JSON Body: `{"title": "My Book", "slug": "my-book", "author": "John Doe", "publication_date": "2025-01-01"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals catalog create your-slug "My Book" --slug my-book --author "John Doe"
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/projects" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"title": "My Book", "slug": "my-book", "author": "John Doe"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/projects"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {"title": "My Book", "slug": "my-book", "author": "John Doe"}

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/projects", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        title: "My Book", 
        slug: "my-book", 
        author: "John Doe"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Get Project Details

Retrieve metadata for a specific project.

`GET /publishers/{publisher_slug}/projects/{project_slug}`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals projects get your-slug the-great-gatsby
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/projects/the-great-gatsby", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Create Publication (ISBN)

Add a publication (ISBN) to a project.

`POST /publishers/{publisher_slug}/projects/{project_slug}/publications`

**Request**
JSON Body: `{"isbn": "978-1234567890", "format": "Paperback", "price": 19.99, "sku": "SKU123"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals projects create-publication your-slug my-book --isbn 978-1234567890 --format Paperback --price 19.99
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/projects/my-book/publications" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"isbn": "978-1234567890", "format": "Paperback", "price": 19.99}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/projects/my-book/publications"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {
        "isbn": "978-1234567890", 
        "format": "Paperback", 
        "price": 19.99
    }

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/projects/my-book/publications", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        isbn: "978-1234567890", 
        format: "Paperback", 
        price: 19.99
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Export Catalog

Download the catalog as a CSV file.

`GET /publishers/{publisher_slug}/catalog/export`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals catalog export your-slug --out catalog.csv
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         -o catalog.csv \
         https://saggingroyals.com/api/publishers/your-slug/catalog/export
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/catalog/export",
        headers=headers
    )
    with open("catalog.csv", "wb") as f:
        f.write(response.content)
    ```

=== "JavaScript"
    ```javascript
    // Node.js example (using fetch + fs)
    const fs = require('fs');
    
    fetch("https://saggingroyals.com/api/publishers/your-slug/catalog/export", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(res => res.arrayBuffer())
    .then(buffer => fs.writeFileSync("catalog.csv", Buffer.from(buffer)));
    ```

## Sales Data

### Upload Sales Report

To upload a CSV or Excel sales report for processing:

`POST /publishers/{publisher_slug}/upload-sales-report`

**Request**

=== "Sagging Royalties Client"
    ```bash
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
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    files = {"file": open("2025-10-IsdSales.csv", "rb")}
    data = {"channel": "Ingram"}

    response = requests.post(url, headers=headers, data=data, files=files)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    // Browser example (Form Data)
    const formData = new FormData();
    formData.append("channel", "Ingram");
    formData.append("file", fileInput.files[0]);

    fetch("https://saggingroyals.com/api/publishers/your-slug/upload-sales-report", {
      method: "POST",
      headers: { "X-API-Key": "<YOUR_API_KEY>" },
      body: formData
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Get Sales Ledger

Retrieve raw sales records.

`GET /publishers/{publisher_slug}/sales/ledger`

#### Parameters
*   `start_date` (query, date)
*   `end_date` (query, date)
*   `channel` (query, string): Channel slug or code

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals sales ledger your-slug --start 2025-01-01
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         "https://saggingroyals.com/api/publishers/your-slug/sales/ledger?start_date=2025-01-01"
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    params = {"start_date": "2025-01-01"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/sales/ledger",
        headers=headers,
        params=params
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    const params = new URLSearchParams({ start_date: "2025-01-01" });
    fetch(`https://saggingroyals.com/api/publishers/your-slug/sales/ledger?${params}`, {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

## Royalties

### List Royalty Holders

`GET /publishers/{publisher_slug}/royalty-holders`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties holders list your-slug
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/royalty-holders
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/royalty-holders",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/royalty-holders", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Create Royalty Holder

`POST /publishers/{publisher_slug}/royalty-holders`

**Request**
JSON Body: `{"name": "Jane Author", "email": "jane@example.com"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties holders create your-slug --name "Jane Author" --email "jane@example.com"
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/royalty-holders" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"name": "Jane Author", "email": "jane@example.com"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/royalty-holders"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {"name": "Jane Author", "email": "jane@example.com"}

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/royalty-holders", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        name: "Jane Author", 
        email: "jane@example.com"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### List Royalty Payments

`GET /publishers/{publisher_slug}/royalty-payments`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties payments list your-slug
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/royalty-payments
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/royalty-payments",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/royalty-payments", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Record Royalty Payment

Record an outgoing payment to a royalty holder.

`POST /publishers/{publisher_slug}/royalty-payments`

**Request**
JSON Body: `{"holder_id": 1, "amount": 500.00, "date": "2025-01-15", "notes": "Check #123"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties payments create your-slug --holder-id 1 --amount 500.00 --date 2025-01-15
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/royalty-payments" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"holder_id": 1, "amount": 500.00, "date": "2025-01-15"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/royalty-payments"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {"holder_id": 1, "amount": 500.00, "date": "2025-01-15"}

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/royalty-payments", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        holder_id: 1, 
        amount: 500.00, 
        date: "2025-01-15"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### List Royalty Statements

Retrieve a list of generated royalty statements.

`GET /publishers/{publisher_slug}/statements`

**Request**

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

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/statements",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/statements", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Generate Statements

Trigger the generation of royalty statements for a period.

`POST /publishers/{publisher_slug}/statements/generate`

**Request**
JSON Body: `{"period_start": "2024-07-01", "period_end": "2024-12-31"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals royalties statements generate your-slug --start 2024-07-01 --end 2024-12-31
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/statements/generate" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"period_start": "2024-07-01", "period_end": "2024-12-31"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/statements/generate"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {"period_start": "2024-07-01", "period_end": "2024-12-31"}

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/statements/generate", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        period_start: "2024-07-01", 
        period_end: "2024-12-31"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Download Statement PDF

Download the PDF file for a specific statement.

`GET /publishers/{publisher_slug}/statements/{statement_id}/download`

**Request**

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

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/statements/123/download",
        headers=headers
    )
    with open("statement.pdf", "wb") as f:
        f.write(response.content)
    ```

=== "JavaScript"
    ```javascript
    // Node.js example
    const fs = require('fs');
    fetch("https://saggingroyals.com/api/publishers/your-slug/statements/123/download", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(res => res.arrayBuffer())
    .then(buffer => fs.writeFileSync("statement.pdf", Buffer.from(buffer)));
    ```

## Users

### List Publisher Users

List users with access to the publisher account.

`GET /publishers/{publisher_slug}/users`

**Request**

=== "Sagging Royalties Client"
    ```bash
    saggingroyals users list your-slug
    ```

=== "cURL"
    ```bash
    curl -H "X-API-Key: <YOUR_API_KEY>" \
         https://saggingroyals.com/api/publishers/your-slug/users
    ```

=== "Python"
    ```python
    import requests

    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    response = requests.get(
        "https://saggingroyals.com/api/publishers/your-slug/users",
        headers=headers
    )
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/users", {
      headers: { "X-API-Key": "<YOUR_API_KEY>" }
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```

### Invite User

Invite a new user to the publisher account.

`POST /publishers/{publisher_slug}/invitations`

**Request**
JSON Body: `{"email": "editor@example.com", "role": "editor"}`

=== "Sagging Royalties Client"
    ```bash
    saggingroyals users invite your-slug editor@example.com --role editor
    ```

=== "cURL"
    ```bash
    curl -X POST "https://saggingroyals.com/api/publishers/your-slug/invitations" \
         -H "X-API-Key: <YOUR_API_KEY>" \
         -H "Content-Type: application/json" \
         -d '{"email": "editor@example.com", "role": "editor"}'
    ```

=== "Python"
    ```python
    import requests

    url = "https://saggingroyals.com/api/publishers/your-slug/invitations"
    headers = {"X-API-Key": "<YOUR_API_KEY>"}
    data = {"email": "editor@example.com", "role": "editor"}

    response = requests.post(url, headers=headers, json=data)
    print(response.json())
    ```

=== "JavaScript"
    ```javascript
    fetch("https://saggingroyals.com/api/publishers/your-slug/invitations", {
      method: "POST",
      headers: { 
        "X-API-Key": "<YOUR_API_KEY>",
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        email: "editor@example.com", 
        role: "editor"
      })
    })
    .then(response => response.json())
    .then(data => console.log(data));
    ```
