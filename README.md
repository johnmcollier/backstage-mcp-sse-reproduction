# backstage-mcp-sse-reproduction

To reproduce this bug:

1) `cd workspaces/mcp-repro`

2) `yarn install`

3) `export MCP_TOKEN=<some-value>`

4) `yarn dev`

## Testing SSE with Cursor

In Cursor, add [mcp.json](./mcp.json) as an MCP tool under `Cursor Settings`. Make sure to set `${MCP_TOKEN}` to the value set above.

With `backend.auth.dangerouslyDisableDefaultAuthPolicy` set to false (or not present) Cursor will never connect to the MCP server:

<img width="673" alt="Screenshot 2025-06-27 at 1 05 48 AM" src="https://github.com/user-attachments/assets/49b08009-2dbc-4c11-8b5f-0d81cabe79e5" />

If you then set `backend.auth.dangerouslyDisableDefaultAuthPolicy` to true, Cursor will then be able to connect and detect the tools in the MCP server: 

<img width="694" alt="Screenshot 2025-06-27 at 1 08 51 AM" src="https://github.com/user-attachments/assets/3a0c2636-dc75-4997-980a-b612147dd9ce" />

However, attempting to call the tool will fail:

<img width="353" alt="Screenshot 2025-06-27 at 1 10 17 AM" src="https://github.com/user-attachments/assets/5b5c1399-819c-4c70-8330-6435ab1e1cff" />

## Testing Streamable HTTP with Cursor

If you change the url in the [mcp.json](./mcp.json) to use the streamable http endpoint (`/api/mcp-actions/v1`), Cursor connects without issue, regardless of the value of `backend.auth.dangerouslyDisableDefaultAuthPolicy`. Additionally, it has no troubles calling the MCP tool:

<img width="357" alt="Screenshot 2025-06-27 at 1 11 42 AM" src="https://github.com/user-attachments/assets/9438851f-f65b-4c21-8c91-cc3a74ccac9c" />