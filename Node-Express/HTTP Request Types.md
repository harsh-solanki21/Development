# HTTP Request Types

| Request Type | Description                       | Idempotent | Safe | Cacheable |
| ------------ | --------------------------------- | ---------- | ---- | --------- |
| GET          | Retrieves a resource              | Yes        | Yes  | Yes       |
| POST         | Submits data to be processed      | No         | No   | No\*      |
| PUT          | Updates an existing resource      | Yes        | No   | No        |
| PATCH        | Partially modifies a resource     | No         | No   | No        |
| DELETE       | Removes a specified resource      | Yes        | No   | No        |
| HEAD         | Retrieves headers only            | Yes        | Yes  | Yes       |
| OPTIONS      | Describes communication options   | Yes        | Yes  | No        |
| TRACE        | Performs a message loop-back test | Yes        | Yes  | No        |
| CONNECT      | Opens a two-way communication     | No         | No   | No        |

- _POST_ responses are only cacheable if they include appropriate Cache-Control or Expires header fields.

**Notes:**

- Idempotent: Multiple identical requests should have the same effect as a single request
- Safe: Should not modify server state
- Cacheable: Response can be cached for future use

<br />

## PUT vs PATCH

The main differences between `PUT` and `PATCH` are:

1. **Scope of update**

   - PUT: Replaces the entire resource with the provided data.
   - PATCH: Partially modifies the resource, updating only specified fields.

2. **Idempotency**

   - PUT: Idempotent. Multiple identical requests should have the same effect as a single request.
   - PATCH: Not necessarily idempotent. Multiple identical PATCH requests might have different effects.

3. **Complete vs. Partial data**

   - PUT: Typically requires the full updated resource to be sent.
   - PATCH: Sends only the data that needs to be modified.

4. **Behavior if resource doesn't exist**

   - PUT: Often creates the resource if it doesn't exist.
   - PATCH: Usually doesn't create new resources; it's meant for updates only.

5. **Use case**
   - PUT: Used when updating a resource in its entirety.
   - PATCH: Used for partial updates or when you only want to modify specific attributes.

### Example

```json
// Suppose we have a user resource
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com"
}

// PUT request to update
{
  "id": 1,
  "name": "John Smith",
  "email": "john@example.com"
}

// PATCH request to update
{
  "name": "John Smith"
}
```
