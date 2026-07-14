`curl` sends an **HTTP** request and prints the response.

Send a GET request and print the response body.
```shell
curl https://example.com
```

Send a POST request with JSON data and print the response data.
```shell
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice"}'
```

