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
