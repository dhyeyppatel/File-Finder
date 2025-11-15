```markdown
# 📘 find.dhyey.space — Search API Documentation

This document explains how to use the public Search API of **find.dhyey.space**, including all supported query parameters, usage examples, and how the Telegram file delivery API works.

---

## 🔍 Base Search Endpoint

```

[https://find.dhyey.space/api/search](https://find.dhyey.space/api/search)

```

This endpoint returns indexed files stored in MongoDB based on search filters.

---

# 📥 How to Use the API

You pass search parameters like this:

```

[https://find.dhyey.space/api/search?q=QUERY](https://find.dhyey.space/api/search?q=QUERY)

```

### 🔹 If the search term contains spaces  
Use URL encoding:

| Search Term | Encoded URL |
|-------------|-------------|
| Golmaal     | `Golmaal` |
| 3 idiots    | `3%20idiots` OR `3+idiots` |

Example:

```

[https://find.dhyey.space/api/search?q=3%20idiots](https://find.dhyey.space/api/search?q=3%20idiots)

```

---

# ⚙️ Query Parameters Supported

Below is the complete list of parameters supported by your Search API.

---

## 1️⃣ `q` — Search Query (string)

Case-insensitive search on the configured `SEARCH_FIELD_NAME`.

**Examples:**

```

[https://find.dhyey.space/api/search?q=adobe](https://find.dhyey.space/api/search?q=adobe)

```

With space:
```

[https://find.dhyey.space/api/search?q=3%20idiots](https://find.dhyey.space/api/search?q=3%20idiots)

```

---

---

# 📦 API Response Format (JSON)

Example response:

```json
{
  "page": 1,
  "per_page": 50,
  "items": [
    {
      "id": "67a3f9d39184bb0d1c2f1234",
      "file_name": "Example File.pdf",
      "file_size": 102400,
      "caption": "Some caption",
      "year": 2023,
      "file_type": "pdf"
    }
  ]
}
````

# 🤖 File Delivery API

You can deliver any indexed file through your Telegram bot using:

```
https://find.dhyey.space/api/send_link/<file_id>
```

### Example

```
https://find.dhyey.space/api/send_link/67a3f9d39184bb0d1c2f1234
```

### Response

```json
{
  "link": "https://t.me/dhyeyautofilterbot?start=file_1123135015_67a3f9d39184bb0d1c2f1234"
}
```

Opening that link in Telegram sends the file to the user.

---

# 🗂 Internal Process Flow

Below is the process of how files flow through your system:

```
User uploads file/media
        ↓
File stored in storage
        ↓
Metadata indexed in MongoDB
        ↓
Website (find.dhyey.space) lists indexed files
        ↓
User searches → /api/search executes
        ↓
Results displayed
        ↓
User selects file
        ↓
API /api/send_link/<file_id>
        ↓
Telegram bot sends file to user
```

---
