# File → Index → Search → Telegram Delivery (Flow Diagram)

This diagram explains the full process:

1. A file/media is uploaded.
2. The file is stored and indexed in MongoDB.
3. The indexed file appears on the public website **find.dhyey.space**.
4. When a user searches, `/api/search` fetches results.
5. When a file is selected, `/api/send_link/<file_id>` is called.
6. The Telegram bot sends the file to the user.

---

```mermaid
flowchart LR
    A[User uploads file/media] --> B[Store file in storage]
    B --> C[Index metadata in MongoDB]

    C --> D[Website: find.dhyey.space shows indexed files]
    C --> E[API: /api/search fetches results]
    E --> F[Search results shown to user]
    F --> G[User selects a file]

    G --> H[API: /api/send_link/<file_id> builds Telegram link]
    H --> I[Telegram bot receives link and sends file]

    D --> G
