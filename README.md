# Compress PDF API

## Overview

This API allows users to compress PDF files by reducing image quality and adjusting the DPI (dots per inch). The compression process helps to decrease the file size while maintaining an acceptable level of quality.

The API is available under a **fair use policy**. For unrestricted usage, users can create an account via [https://login.cross-service-solutions.com](https://login.cross-service-solutions.com).

---

## Endpoint

### POST Request

**URL:**  
`https://api.cross-service-solutions.com/solutions/solutions/free/62`

### Headers

```http
Content-Type: multipart/form-data
```

### Request Body (Form-Data)

| Parameter      | Type   | Description                                                                                            |
|--------------|--------|--------------------------------------------------------------------------------------------------------|
| `file`        | file   | The PDF file to be uploaded and compressed.                                                            |
| `imageQuality` | string | Compression quality percentage (0-100). Lower values result in smaller file sizes but reduced quality. |
| `dpi`         | string | Dots per inch (72-300). Lower values decrease the file size but reduce resolution quality.             |

### Response

#### Success (201 Created)

Upon successful compression, the API returns the following JSON response:

```json
{
    "id": number,
    "solutionBluePrintId": number,
    "name": "string",
    "status": "string",
    "steps": [
        {
            "name": "string",
            "status": "string"
        }
    ],
    "output": null
}
```

### Cookies

The response sets the following cookies:

- **`Solution_id`**: A unique identifier for the solution.
- **`Solution_UUID`**: A unique UUID associated with the solution.

These cookies are required for retrieving the final compressed PDF.

---

## Follow-up Request

### GET Request

**URL:**  
`https://api.cross-service-solutions.com/solutions/solutions/free/62`

To retrieve the processed file, send a `GET` request to the same endpoint, including the cookies (`Solution_id` and `Solution_UUID`) from the initial response.

### Headers

```http
Cookie: Solution_id=<value>; Solution_UUID=<value>
```

### Response

The `GET` request will return the compressed PDF file once processing is complete. The result of the compression can be found under the **`output`** key.

```json
{
    "id": number,
    "solutionBluePrintId": number,
    "name": "string",
    "status": "string",
    "steps": [
        {
            "name": "string",
            "status": "string"
        }
    ],
    "output": {
        "result": "string",
        "data": null,
        "files": [
            {
                "name": "string",
                "path": "string"
            }
        ]
    }
}
```
