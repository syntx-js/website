# Create a new paste

<mark style="color:green;">`GET`</mark> `https://code.erxproject.xyz/api/v1/paste/create`

Create a paste.

**Headers**

| Name          | Value    |
| ------------- | -------- |
| Authorization | `$TOKEN` |

**Body**

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| `name` | string | Name of the user |
| `age`  | number | Age of the user  |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "success": true,
  "data": {
    "code": "abcdef",
    "url": "https://code.erxproject.xyz/abcdef",
    "syntx": "JavaScript",
    "title": "Code Bin",
    "description": "
  }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
