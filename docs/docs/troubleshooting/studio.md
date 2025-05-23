# Troubleshooting LangGraph Studio

## :fontawesome-brands-safari:{ .safari } Safari connection error with local dev server

Safari blocks plain‑HTTP traffic on localhost. If you start Studio with a vanilla  
`langgraph dev`, the page may report a "Failed to load assistants" error (or something similar) and the browser DevTools will show network errors.

#### Quick fix — run Studio through a secure Cloudflare tunnel

=== "Python"

    ```shell
    pip install -U langgraph-cli>=0.2.6            # Python
    langgraph dev --tunnel
    ```
=== "JS"

    ```shell
    # Requires @langchain/langgraph-cli>=0.0.26
    npx @langchain/langgraph-cli dev
    ```

The command prints a URL like:

```shell
https://smith.langchain.com/studio/?baseUrl=https://hamilton-praise-heart-costumes.trycloudflare.com
```
where
```shell
?baseUrl=https://hamilton-praise-heart-costumes.trycloudflare.com
```
indicates the endpoint where your agent server is exposed.

Open that URL in Safari and Studio should load immediately.

#### Alternative — use a Chromium‑based browser

Chrome, Edge, and Brave allow HTTP on localhost, so a plain `langgraph dev` should work without extra steps.

#### If it’s still not loading

1. Make sure the `baseUrl` query parameter in the studio URL points to the **tunnel URL** NOT to localhost.
2. Confirm your CLI version with `langgraph --version`.

No other configuration, certificates, or CORS tweaks are required.
