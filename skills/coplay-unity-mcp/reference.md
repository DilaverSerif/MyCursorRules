# Coplay MCP for Unity — reference

## Manual MCP client configuration

If Unity’s auto-setup fails, mirror the JSON in the [CoplayDev/unity-mcp README](https://github.com/CoplayDev/unity-mcp/blob/main/README.md).

### HTTP (default)

Cursor / Claude Desktop tarzı:

```json
{
  "mcpServers": {
    "unityMCP": {
      "url": "http://localhost:8080/mcp"
    }
  }
}
```

VS Code:

```json
{
  "servers": {
    "unityMCP": {
      "type": "http",
      "url": "http://localhost:8080/mcp"
    }
  }
}
```

### Stdio (`uvx`)

**macOS / Linux:**

```json
{
  "mcpServers": {
    "unityMCP": {
      "command": "uvx",
      "args": ["--from", "mcpforunityserver", "mcp-for-unity", "--transport", "stdio"]
    }
  }
}
```

**Windows:** You may need the full path to `uvx.exe`; see the WinGet path template in the README.

## Strict script validation (Roslyn)

- Recommended: Unity `Window > MCP for Unity` → Scripts/Validation → **Install Roslyn DLLs** (or the equivalent menu action).
- Alternative: NuGetForUnity + `Microsoft.CodeAnalysis` + companion packages from the README + `USE_ROSLYN` scripting define.

## Custom tools and development

- Custom tools: [CUSTOM_TOOLS.md](https://github.com/CoplayDev/unity-mcp/blob/main/docs/reference/CUSTOM_TOOLS.md)
- Dev setup: [README-DEV.md](https://github.com/CoplayDev/unity-mcp/blob/main/docs/development/README-DEV.md)

## Other install channels

- Unity Asset Store package and OpenUPM (`openupm add com.coplaydev.unity-mcp`) — follow README steps.
