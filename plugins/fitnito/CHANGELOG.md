# Changelog

## 1.0.1

Docs only. The MCP server and skills reflect what is live at `https://mcp.fitnito.com/`.

- Documents the OAuth scopes: `mcp` (full access) and `mcp:read` (read only). The sign-in screen offers **Full access** or **Read only**.
- Booking and dropping a class is quote, then confirm. The first call returns `status: "quoted"` and writes nothing. Confirm with `confirmed: true` and the quoted `starts_at` and `visits`. The `book-or-unbook-member` skill now follows this.
- Documents booking alerts from MCP Events: `session.booked`, `session.unbooked`, and `session.cancelled`.
- Documents the MCP Apps surfaces: `schedule.today`, `schedule.beside`, and `fitnito.mentions`.
- Notes that each tool description starts with Read, Write, or Sensitive write.

## 1.0.0 (initial release)

- Adds the `fitnito` MCP server at `https://mcp.fitnito.com/`. You sign in with your Fitnito login when it connects. There is no key or token to set up.
- Adds four skills: weekly schedule review, booking or unbooking a member, setting up a new gym, and asking before any email goes out.
