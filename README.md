# Azure OpenAI UI

A lightweight web chat interface for talking to a GPT Nano model hosted on Azure OpenAI. The UI is plain HTML, CSS and JavaScript (no build step) and sends messages to the **AzureOpenAiApi** REST backend.

## How it works

```text
Browser (index.html)  --POST /api/v1/Chat-->  AzureOpenAiApi  -->  Azure OpenAI (GPT Nano)
```

The UI sends:

```json
{ "message": "Hello!" }
```

and expects the API to respond with:

```json
{ "reply": "Hi! How can I help you?" }
```

## Prerequisites

- The **AzureOpenAiApi** project running locally at `http://localhost:5142`
- **CORS enabled** in the API for the origin serving the UI (`http://localhost:8000`)
- **Python 3** (or any other static file server, see below)

## Getting started

1. Start the AzureOpenAiApi backend.
2. From the root of this repository, serve the files:

   ```bash
   python -m http.server 8000
   ```

3. Open the chat in your browser:

   ```text
   http://localhost:8000/index.html
   ```

### Alternative static servers

- Node.js: `npx serve -l 8000`
- VS Code: the **Live Server** extension (if it uses a different port, add that origin to the API's CORS policy)

## Configuration

The API endpoint is defined at the top of the script in `index.html`:

```js
const apiUrl = "http://localhost:5142/api/v1/Chat";
```

Change it if your API runs on a different host or port.

## Project structure

```text
.
├── index.html      # Chat page and client-side logic
├── css/
│   └── styles.css  # Chat styles
└── README.md
```

## Troubleshooting

| Problem | Likely cause |
| --- | --- |
| `Error: Failed to fetch` in the chat | The API is not running, or CORS is not allowing `http://localhost:8000` |
| Nothing happens when opening `index.html` directly | Serve it over HTTP (step 2) instead of opening it with `file://` |
