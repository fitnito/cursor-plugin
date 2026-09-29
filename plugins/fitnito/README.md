# Fitnito

Schedule, members, and bookings for independent gyms and studios, from chat.

Fitnito is gym software for independent gyms and studios. Connect it to Cursor to see the week's schedule, look up members, book people into classes or take them off, add classes, and get answers from Fitnito help. Owners, coaches, and members sign in with their own Fitnito login, and the assistant can only see and do what that login already can. It asks before it emails anyone.

## Install

1. In Cursor, find **Fitnito** in the plugin marketplace.
2. Install it.
3. The Fitnito sign-in page opens. Sign in with your Fitnito email and password, or click Continue with Google.
4. Pick the gym or gyms this connection can use, then click **Allow access**.

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

## Skills

| Skill | What it does |
| --- | --- |
| `weekly-schedule-review` | Sums up a week of classes, bookings, and anything that needs a look. It doesn't change anything. |
| `book-or-unbook-member` | Books a member into one class or takes them off it. It checks the person and the class, and asks before it makes the change. |
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

What you can do matches your role in Fitnito. Owners and admins can run the gym: schedule, members, passes, and plans. Coaches can see the schedule and members, and book people into the classes they coach. Members can book classes and manage their own account, the same as on the booking site. To disconnect, go to **Settings → AI Agent Access** in Fitnito and remove this connection. Each connection is one login in one app.

## Support

- Help: https://help.fitnito.com/owners/advanced/connect-ai-agents
- Developers: https://fitnito.com/developers
- Support: https://fitnito.com/support · info@fitnito.com
- Privacy: https://fitnito.com/privacy-policy
- Terms: https://fitnito.com/terms

## License

MIT. This license covers the plugin files in this repository. Using Fitnito itself is covered by the Fitnito terms.
