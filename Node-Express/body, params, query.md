# HTTP Request Data Sending Methods

## `req.body`

- Generally used in POST/PUT requests.
- Use it when you want to send sensitive data (e.g., form data) or large JSON data to the server.
- Use this middleware functions to parse incoming requests with JSON payloads.
  `app.use(express.json())`

<br />

#### How to send data in request body

- **Using Curl:**

```bash
curl -d '{"key1":"value1", "key2":"value2"}' -H "ContentType: application/json" -X POST http://localhost:3000/giraffe
```

<br />

- **using axios:**

```node
axios
  .post("/giraffe", {
    key1: "value1",
    key2: "value2",
  })
  .then((response) => {
    // Handle response
  })
  .catch((error) => {
    // Handle error
  });
```

<br />

## `req.params`

- These are properties attached to the URL, i.e., named route parameters. You prefix the parameter name with a colon (:) when writing your routes.

```node
app.get("/giraffe/:number", (req, res) => {
  console.log(req.params.number);
});
```

<br />

## `req.query`

- It is mostly used for searching, sorting, filtering, pagination, etc. For instance, if you want to query an API but only want to get data from page 10, this is what you'd generally use.
- It is written as `key=value` in the URL.
  `GET  http://localhost:3000/animals?page=10`

```node
app.get("/animals?page=10)", () => {
  console.log(req.query.page); // 10
});
```
