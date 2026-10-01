# Example: saving a reading-list item

This is a fictional teaching example, not a report about an inspected application. The source descriptions below are assumptions supplied for the example; a real explanation should replace them with verified references.

## Supplied example evidence

- `web/save-item.ts`: browser sends an authenticated POST with a URL and request ID; displays an error when the request fails.
- `api/items.ts`: handler validates input and ownership, inserts into a relational database, and uses a unique `(user_id, request_id)` key to return the existing result on a duplicate request.
- `db/items.sql`: item records persist in the database. No queue or cache is specified.
- `api/logger.ts`: logs failed writes with the request ID. No alerting or automatic retries are specified.

## System explanation

**Components and flow — Implemented in this example:** the browser collects a URL and sends it to the API. The API checks who is asking, validates the input, writes the item and returns its ID. The database preserves the record. The API owns validation and authorization; the browser owns presentation. Evidence: `web/save-item.ts`, `api/items.ts`, `db/items.sql`.

**State:** saved items live in the database. The browser's success/error message is temporary UI state. No cache or queue is established by the supplied evidence.

**Failure and recovery:** if a database write fails, the API logs the failure and the browser shows an error. A lost response creates uncertainty: the write might already have succeeded. Repeating a request with the same request ID returns the existing record instead of inserting twice. Whether the browser actually reuses that ID on retry is **Unknown** from this evidence. Automatic retry and alerting are also **Unknown**.

**Trade-off — inference:** writing synchronously keeps the flow simple and lets the API confirm persistence before returning success, but database latency or failure directly affects the request. A background queue would change that contract and is not part of this example.

**Say it aloud:** “The browser asks the API to save a link. The API checks access and writes it to the database, which is the lasting record. If the response is lost, the same request ID can prevent a duplicate—but we still need to check that the browser reuses it.”

**Practice:** Why does a unique request ID help with a lost response, and what client behavior must accompany it?

## After turning OFF

User: “System explanation off. Summarize the change.”

Expected style: “Added authenticated link saving with input validation and database deduplication. The browser displays write errors. Client retry behavior remains unverified.”

No recurring teaching section or practice question is added. If the user directly asks about deduplication afterward, answer that question normally.
