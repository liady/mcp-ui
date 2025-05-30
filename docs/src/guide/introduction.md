# Introduction

Welcome to the MCP-UI documentation!

This SDK provides tools for building Model Context Protocol (MCP) enabled applications with interactive UI components. It aims to standardize how models and tools can request the display of rich HTML interfaces within a client application.

## What is MCP UI?

MCP UI is a TypeScript SDK containing:

- **`@mcp-ui/client`**: UI components (like `<HtmlResource />`) for easy rendering of interactive HTML resources.
- **`@mcp-ui/server`**: Helper functions (like `createHtmlResource`) for server-side logic to easily construct `HtmlResource` objects.

## Core Concept: The Interactive HTML Resource Protocol

The central piece of this SDK is the `HtmlResource`. This object defines a contract for how interactive HTML content should be structured and delivered from a server/tool to a client.

### `HtmlResource` Structure

```typescript
// Defined in @mcp-ui/shared, but shown here for clarity
export interface HtmlResource {
  type: 'resource'; // Fixed type identifier
  resource: {
    uri: string; // Unique identifier. Governs rendering behavior.
    mimeType: 'text/html' | 'text/uri-list'; // text/html for HTML content, text/uri-list for URL content
    text?: string; // Raw HTML string or an iframe URL string.
    blob?: string; // Base64 encoded HTML string or iframe URL string.
  };
}
```

### Key Field Details:

- **`uri` (Uniform Resource Identifier)**:
  - All UI resources use the `ui://` scheme (e.g., `ui://my-custom-form/instance-01`)
  - The rendering method is determined by the `mimeType`:
    - `mimeType: 'text/html'` → HTML content rendered via `<iframe srcdoc>`
    - `mimeType: 'text/uri-list'` → URL content rendered via `<iframe src>`
- **`mimeType`**: `'text/html'` for HTML content, `'text/uri-list'` for URL content
- **`text` or `blob` Content Delivery**:
  - `text`: The HTML string or URL is provided directly.
  - `blob`: The HTML string or URL is Base64 encoded. Useful for complex HTML, ensuring integrity, or avoiding issues with JSON encoding of special characters.

This protocol allows for flexible delivery and rendering of HTML content, from simple static blocks to fully interactive applications embedded within the client.

Dive into the "Getting Started" guide or explore specific SDK packages for more details.

## Philosophy

Returning chunks of UI as responses from MCP servers is a powerful way to create interactive experiences. However, it can be difficult to get right.
This is an ongoing discussion in the MCP community and [steering committee](https://github.com/orgs/modelcontextprotocol/discussions/287#discussioncomment-13175290).

This project is an experimental playground for MCP UI ideas, as we're exploring ways to make it easier.