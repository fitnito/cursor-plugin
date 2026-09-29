# Fitnito plugin for Cursor

This repository holds the Cursor plugin for [Fitnito](https://fitnito.com): schedule, members, and bookings for independent gyms and studios, from chat.

The plugin is in [`plugins/fitnito`](plugins/fitnito/). See its [README](plugins/fitnito/README.md) for install steps, the MCP server, and the skills.

```text
.cursor-plugin/marketplace.json   marketplace manifest (one plugin)
plugins/fitnito/
  .cursor-plugin/plugin.json      plugin manifest
  mcp.json                        https://mcp.fitnito.com/ (OAuth sign-in)
  skills/                         4 skills
  assets/logo.png                 512x512 logo
```

## Test locally

Copy `plugins/fitnito` to `~/.cursor/plugins/local/fitnito`. Then run **Developer: Reload Window** and open **Customize** to check that the MCP server and the four skills show up.

## License

MIT. See [LICENSE](LICENSE).
