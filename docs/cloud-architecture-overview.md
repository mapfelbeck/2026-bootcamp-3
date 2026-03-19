# Cloud Architecture Overview

This monorepo contains a simple three-part application architecture:

- A React frontend that runs in the browser
- An Express API that handles task operations
- An in-memory SQLite store used by the backend process

## System Context

```mermaid
flowchart LR
    User[User in Browser]
    Frontend[React Frontend\npackages/frontend]
    Backend[Express API\npackages/backend]
    Store[In-Memory SQLite Store\nbetter-sqlite3 :memory:]

    User --> Frontend
    Frontend -->|HTTP /api/tasks| Backend
    Backend --> Store
```

## Create TODO Sequence

```mermaid
sequenceDiagram
    actor User
    participant Browser as React Frontend
    participant API as Express API
    participant DB as In-Memory SQLite Store

    User->>Browser: Enter task details and submit form
    Browser->>API: POST /api/tasks
    Note over Browser,API: Payload includes title and optional fields such as description and due_date
    API->>API: Validate request body
    API->>DB: INSERT task record
    DB-->>API: Return created task id
    API->>DB: SELECT created task
    DB-->>API: Return created task
    API-->>Browser: 201 Created + task JSON
    Browser->>API: GET /api/tasks
    API->>DB: SELECT all tasks
    DB-->>API: Return task list
    API-->>Browser: 200 OK + tasks JSON
    Browser-->>User: Show updated TODO list
```

## Notes

- The frontend is the user-facing application and sends task requests to the backend API.
- The backend exposes task endpoints and contains the application business logic.
- Data is stored only in memory, so it resets whenever the backend process restarts.
- There is no external database, cloud storage, or third-party service dependency in the current implementation.
