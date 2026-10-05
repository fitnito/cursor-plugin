# Fitnito

Schedule, members, and bookings for independent gyms and studios, from chat.

Fitnito is gym software for independent gyms and studios. Connect it to Cursor to see the week's schedule, look up members, book people into classes or take them off, add classes, and get answers from Fitnito help. Owners, coaches, and members sign in with their own Fitnito login, and the assistant can only see and do what that login already can. It asks before it emails anyone.

## Install

1. In Cursor, find **Fitnito** in the plugin marketplace.
2. Install it.
3. The Fitnito sign-in page opens. Sign in with your Fitnito email and password, or click Continue with Google.
4. Pick the gym or gyms this connection can use. Under **What this app can do**, choose **Full access** or **Read only**, then click **Allow access**.

That's it. There's nothing else to set up.

## MCP server

```json
{
  "mcpServers": {
    "fitnito": {
      "type": "http",
      "url": "https://mcp.fitnito.com/"
    }
  }
}
```

## Sign-in and access

- MCP URL: `https://mcp.fitnito.com/`
- OAuth with dynamic client registration and PKCE (S256). Authorization server: `https://app.fitnito.com`. There is no key, token, or client secret to set up.
- Scopes: `mcp` (full access) and `mcp:read` (read only). On the sign-in screen you can narrow full access to read only. A read-only connection can call Read tools only. Write tools are left off its tool list and return an error, without running, if called.
- Access tokens last 2 hours. An expired or revoked token gets a 401 with `error="invalid_token"`, so Cursor can refresh or ask you to sign in again.

## Tools

Each tool description starts with **Read**, **Write**, or **Sensitive write**, and Read tools set `readOnlyHint`.

| Label | Meaning |
| --- | --- |
| Read | Does not change anything. |
| Write | Creates or changes gym data, like adding a class. |
| Sensitive write | Books or drops a class, sends an email, changes a membership or money, signs a document, or deletes. |

A tool that can both read and write counts as a write. The live list and schemas are `tools/list` on the server.

## Booking: quote, then confirm

Booking or dropping a class (`book_client`, `unbook_client`, `member_book`, `member_cancel_booking`) takes two calls.

1. The first call returns `status: "quoted"`: the class, `starts_at`, the visit cost, the terms, and the cancellation policy. **A quote is not a booking.** Nothing is written.
2. To book or drop, call again with `confirmed: true`, the same `starts_at`, and `visits` from the quote's cost (or `new_pass_visits` when `book_client` would create a pass; that pass is 10 visits).
3. If the class time or visit count no longer matches, you get a new quote with `changed: true` and nothing is written.

A confirmed booking returns `status: "confirmed"` and a `confirmation_id`. Booking again returns the same id. A refused booking returns `status: "failed"` (full, no visits left, waiver missing, class cancelled). A drop returns `status: "cancelled"`. No card is charged for a class: the cost is visits, or included on an unlimited pass.

## Booking alerts (MCP Events)

Ask the assistant to tell you when someone books, drops, or a class is cancelled. Fitnito sends `session.booked`, `session.unbooked`, and `session.cancelled`. A booking or drop has the class id and one `client_id`. A cancellation has `client_ids`. The note has the time and how full the class is, not names or emails. Owners and coaches can watch the whole gym. A member connection only hears about that member and their kids. Say stop, or disconnect the app, to turn it off.

## App surfaces

In hosts that support MCP Apps, the same server also offers:

- **Today's classes** (`schedule.today`): today's classes, who is booked, and how many spots are open.
- **Schedule** (`schedule.beside`): the same board in a panel beside the chat.
- **@Fitnito** (`fitnito.mentions`): pick a class or member from the composer. Booking still goes through the quote-then-confirm tools above.

## Skills

| Skill | What it does |
| --- | --- |
| `weekly-schedule-review` | Sums up a week of classes, bookings, and anything that needs a look. It doesn't change anything. |
| `book-or-unbook-member` | Books a member into one class or takes them off it. It checks the person and the class, shows the quote (visit cost and terms), and confirms only after you say yes. |
| `set-up-new-gym` | Walks a new owner through setup in order: location, programs, pass types, plans and packs, then the weekly schedule. |
| `ask-before-emailing` | Says who would get an email and asks first. This covers welcome emails, password resets, and family link requests. |

## Try it

- What's on the schedule this week?
- Who's booked into next Tuesday's 7pm Yoga?
- Look up Riley Chen.
- Book Priya Sharma (priya.sharma@example.com) into the next Thursday 6pm Training.
- Take Priya Sharma off the next Thursday 6pm Training.
- Add a one-off Training class next Wednesday from 6 to 7pm, capacity 12.
- What passes does the gym offer?
- How do members book a class?

## What your login can do

What you can do matches your role in Fitnito. Owners and admins can run the gym: schedule, members, passes, and plans. Coaches can see the schedule and members, and book people into the classes they coach. Members can book classes and manage their own account, the same as on the booking site. A read-only connection can look but cannot book, email, or change anything. To disconnect, go to **Settings → AI Agent Access** in Fitnito and remove this connection. Each connection is one login in one app.

## Support

- Help: https://help.fitnito.com/owners/advanced/connect-ai-agents
- Developers: https://fitnito.com/developers
- Support: https://fitnito.com/support · info@fitnito.com
- Privacy: https://fitnito.com/privacy-policy
- Terms: https://fitnito.com/terms

## License

MIT. This license covers the plugin files in this repository. Using Fitnito itself is covered by the Fitnito terms.
