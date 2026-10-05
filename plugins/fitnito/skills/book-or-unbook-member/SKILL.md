---
name: book-or-unbook-member
description: Book a Fitnito member into a class or take them off one, safely. Use when someone asks to book, add, drop, remove, or move a person in a class.
---

# Book or unbook a member

## When to use

- "Book Priya into Thursday's 6pm Training."
- "Take Priya off Thursday's class."
- "Move Sam from the 6pm to the 7pm."

## Steps

1. Find the member. If more than one person matches the name, list them with their email and ask which one. Never guess a person.
2. Find the exact class: the program, the date, and the start time. "Next Thursday 6pm" means one class, not the whole weekly series. If it's unclear, ask.
3. Call the booking tool without `confirmed` to get a quote. A quote (`status: "quoted"`) is not a booking. Nothing has changed yet.
4. Say the quote back in one line, with the visit cost and the cancellation terms, and wait for a yes. For example: "Book Priya Sharma (priya.sharma@example.com) into Training, Thu Oct 8, 6 to 7pm? It uses 1 visit."
5. After the yes, call again with `confirmed: true`, the same `starts_at`, and `visits` from the quote (or `new_pass_visits` if a new pass would be created). If the reply is a new quote with `changed: true`, the class or visit count changed. Show the new quote and ask again.
6. On `status: "confirmed"`, confirm what happened: the member, the class, the day, the time, and the confirmation id. On `status: "failed"`, say why and change nothing else.
7. To move someone, take them off the first class and book them into the second, each with its own quote and confirm. Confirm both parts.

## Keep in mind

- If the class is full, say so and ask what they want to do. If a coach's login can't book because the member has no pass or visits left, say so. Don't work around it.
- Taking someone off a class gives back the visit they used. The class itself stays on the schedule.
- No card is charged for a class. The cost is visits, or included on an unlimited pass.
- A read-only (`mcp:read`) connection can't book or drop. Say so and suggest reconnecting with full access.
- Don't create a new member or a new class to make a booking work unless they ask for that.
- Ask first before assigning a paid plan, selling a pack, refunding, or cancelling a membership. These can charge or refund real money.
