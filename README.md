# Country Generator MCP Server

Look up any country's capital, population and borders, or play geography quizzes with your AI.

This repository holds the documentation and registration metadata for the hosted server. The server itself runs at countrygenerator.com.

- **Endpoint:** `https://countrygenerator.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** None
- **Documentation:** [countrygenerator.com/mcp](https://countrygenerator.com/mcp)

## Tools

| Tool | What it does |
| --- | --- |
| `get_country` | Facts about one country: capital, region, population, area, languages, currencies, driving side and neighbours. |
| `search_countries` | Lists countries by part of a name or capital, by continent, or landlocked only. |
| `random_country` | Picks a random country, optionally from one continent. |
| `compare_population` | Ranks 2 to 4 countries by population. |
| `get_borders` | Lists the countries that share a land border with a country. |
| `create_quiz` | Creates questions on flags, capitals, country outlines, population or neighbours. |
| `check_answer` | Checks one quiz answer and returns the right answer, some facts and the new score. |

Every tool is read-only. Names and answers work in English, German, Spanish, French, Portuguese, Japanese and Italian. Country lookups accept a name in any of those languages or an ISO code.

Each quiz question carries an encrypted ticket that holds the answer, so the assistant cannot give it away early. A run ends after three wrong answers. Quizzes have easy, medium and hard levels and can be limited to one continent.

The server also has a `quiz_me` prompt for clients that show prompts.

## Connect

### Claude

1. Open **Customize**, then **Connectors**.
2. Select **+ Add**, then **Add custom connector**.
3. Enter **Country Generator** as the name and `https://countrygenerator.com/mcp` as the URL, then select **Continue**.
4. Under **Authentication**, choose **No sign in**, then select **Add**.

### Claude Code

```bash
claude mcp add --transport http country-generator https://countrygenerator.com/mcp
```

### Cursor

Add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "country-generator": {
      "url": "https://countrygenerator.com/mcp"
    }
  }
}
```

### VS Code

Add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "country-generator": {
      "type": "http",
      "url": "https://countrygenerator.com/mcp"
    }
  }
}
```

### Gemini CLI

```bash
gemini extensions install https://github.com/countrygenerator/mcp-server
```

### ChatGPT

1. Open [ChatGPT Plugins](https://chatgpt.com/plugins) in your browser.
2. Select the plus button, then **Add custom MCP server**.
3. Enter **Country Generator** as the name and `https://countrygenerator.com/mcp` as the server URL.
4. Review the permissions and warning, then select **Create as a plugin**.
5. Install the resulting plugin, start a new conversation and select it using `@`.

### Grok

1. Open [Grok Connectors](https://grok.com/connectors).
2. Select **New Connector**, then **Custom**.
3. Enter `https://countrygenerator.com/mcp` as the MCP server URL. This server requires no authentication.
4. Complete the setup to make the tools available in conversations.

### Other MCP clients

Where custom remote MCP connections are available, use `https://countrygenerator.com/mcp` with Streamable HTTP.

## Example prompts

- What is the capital of Kazakhstan, and which countries border it?
- Which has more people: Nigeria, Brazil or Japan?
- Quiz me on African flags, hard mode.
- Give me 10 capital questions about Asia, in German.

## Limits

To maintain service stability, security, and fair usage, the API enforces server-side rate limiting and request validation.

- **Rate Limiting:** Requests are subject to usage restrictions to prevent excessive traffic and automated abuse.
- **Limit Exceeded:** Requests exceeding permitted thresholds receive an HTTP `429 Too Many Requests` response with a `Retry-After` header.
- **Quiz Generation:** The `create_quiz` endpoint enforces request and question-generation limits.
- **Ticket Validity:** Quiz tickets are temporary and automatically expire after a predefined period.
- **Abuse Prevention:** Additional restrictions may be applied to suspicious or excessive activity.

## Support

For bug reports and questions, [open an issue](https://github.com/countrygenerator/mcp-server/issues).

- [Documentation](https://countrygenerator.com/mcp)
- [Privacy Policy](https://countrygenerator.com/privacy)
- [Terms](https://countrygenerator.com/terms)
