---
name: coplay-unity-mcp
description: Installs and operates Coplay MCP for Unity (CoplayDev/unity-mcp) — Unity package via git URL, HTTP or stdio client config, multi-instance routing with set_active_instance, resources vs tools, batch_execute for bulk edits, and post-edit validation via read_console, refresh_unity, and run_tests. Use when the user mentions Coplay, MCP for Unity, unity-mcp, unityMCP, or when driving the Unity Editor through an MCP client in Cursor.
disable-model-invocation: false
---

# Coplay MCP for Unity

## Official links

- Repository: [CoplayDev/unity-mcp](https://github.com/CoplayDev/unity-mcp)
- Setup troubleshooting: [Fix Unity MCP and Cursor, VSCode & Windsurf](https://github.com/CoplayDev/unity-mcp/wiki/1.-Fix-Unity-MCP-and-Cursor,-VSCode-&-Windsurf), [Common Setup Problems](https://github.com/CoplayDev/unity-mcp/wiki/3.-Common-Setup-Problems)

## Install (short)

1. **Unity**: 2021.3 LTS or newer.
2. **Host**: Python 3.10+, [uv](https://docs.astral.sh/uv/getting-started/installation/).
3. **Unity package**: `Window > Package Manager > + > Add package from git URL...`

```text
https://github.com/CoplayDev/unity-mcp.git?path=/MCPForUnity#main
```

For beta, use the `#beta` branch instead of `#main`.

4. **Server + client**: In Unity, `Window > MCP for Unity` → **Start Server** (default HTTP, e.g. `localhost:8080`) → pick client → **Configure** → confirm green “Connected”.

Manual MCP JSON and stdio snippets: [reference.md](reference.md).

## Agent workflow

1. **Read before write**: Use MCP **resources** for scene, selection, console, and editor state; use **tools** for mutations.
2. **Batch work**: Prefer `batch_execute` over many single-tool calls when the README’s performance note applies.
3. **Multiple editors**: Read `unity_instances`; pin the target with `set_active_instance` using `Name@hash`; reconfirm before writes.
4. **Scripts / compile**: After edits, check `read_console`; use `refresh_unity` and `validate_script` as needed; if tests exist, `run_tests` + `get_test_job`.
5. **API truth**: When `unity_reflect` / `unity_docs` are available, use them instead of guessing Unity APIs from memory.

## Tool picking

- **Scene / GameObjects**: `manage_scene`, `manage_gameobject`, `find_gameobjects`, `manage_components`
- **Assets / prefabs / materials**: `manage_asset`, `manage_prefabs`, `manage_material`, `manage_shader`, `manage_texture`
- **Scripts**: `manage_script`, `script_apply_edits`, `create_script`, `validate_script`
- **Editor**: `manage_editor`, `execute_menu_item`, `read_console`, `manage_tools`
- **Packages, build, physics, graphics, profiler**, etc.: match task to the current tool list in the upstream README (names change as versions ship).

## Security and privacy (short)

HTTP defaults are loopback-oriented; LAN or remote bind needs explicit opt-in. Telemetry: opt out with `DISABLE_TELEMETRY=true`. Details: repo `TELEMETRY.md` and README security section.

## More detail

- [reference.md](reference.md) — Cursor/VS Code MCP JSON, stdio `uvx`, Roslyn validation, custom tools pointers
