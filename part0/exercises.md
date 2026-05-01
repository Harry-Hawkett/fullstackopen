# Part 0 Exercises

## Exercise 0.4 – New note diagram

Depicts the sequence of events when a user writes a note and clicks **Save** on:
`https://studies.cs.helsinki.fi/exampleapp/notes`

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a note into the text field and clicks Save

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note right of server: Server adds the new note to its notes array
    server-->>browser: 302 Redirect to /exampleapp/notes
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser executes the JavaScript which fetches the updated notes list

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser renders the full notes list, including the new note
```

---

## Exercise 0.5 – Single page app diagram

Depicts the sequence of events when a user opens the SPA version of the notes app at:
`https://studies.cs.helsinki.fi/exampleapp/spa`

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser executes the JavaScript which fetches the notes list

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser renders the notes list without any further page loads
```

---

## Exercise 0.6 – New note in Single page app diagram

Depicts the sequence of events when a user creates a new note using the SPA version of the app.

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a note and clicks Save

    Note right of browser: The browser handles the form submit event with JavaScript — no page reload

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note left of server: Request body is JSON: { "content": "a new note", "date": "2024-01-01" }
    server-->>browser: 201 Created — { "message": "note created" }
    deactivate server

    Note right of browser: The browser adds the new note to its local notes array and re-renders the list — no redirect, no full page reload
```
