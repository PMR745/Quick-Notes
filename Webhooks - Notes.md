
## 🔍 What is a Webhook?
- Webhook is an **event-driven** mechanism.
- It allows one system to notify another via an **HTTP POST** request when a specific event occurs.
- Unlike traditional API calls, webhooks don't require continuous polling.

## 🔁 Webhook vs API Call

- **Communication**
  - **API Call**: Client sends a request and waits for a response.
  - **Webhook**: Server sends a request to a client-defined endpoint when an event occurs.

- **Trigger**
  - **API Call**: Triggered manually or programmatically by the client.
  - **Webhook**: Triggered automatically when a specific event occurs on the server.

- **Direction**
  - **API Call**: Client → Server
  - **Webhook**: Server → Client (to a registered URL)



## ✅ Real-world Use Case
- Messaging apps: When a message is sent, notify the recipient via a webhook instead of maintaining open connections.

## 🔐 Webhook Security
- Use **signatures** or **tokens** (e.g., HMAC) in headers.
- Validate signature on the server using a **shared secret**.
- GitHub uses `X-Hub-Signature-256`.

## 📬 HTTP Method
- Most webhooks use **POST** to send payloads.
- Headers include authentication info or event type.

## 🧪 Testing Webhooks Locally
- Tools:
  - [ngrok](https://ngrok.com/): Expose local server to public.
  - [Webhook.site](https://webhook.site/): Inspect payloads.
- Steps:
  1. Run your server locally.
  2. Start `ngrok http <port>`.
  3. Use the public URL as the webhook endpoint.

## 🛠️ .NET Minimal API Webhook Endpoint Example
```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapPost("/webhook", async (HttpRequest request) =>
{
    // Read the raw body
    using var reader = new StreamReader(request.Body);
    var body = await reader.ReadToEndAsync();

    // Optional: Read headers
    var signature = request.Headers["X-Hub-Signature-256"].ToString();

    // Optional: Verify signature
    if (!VerifySignature(body, signature))
    {
        return Results.Unauthorized();
    }

    // Parse JSON payload
    var payload = JsonSerializer.Deserialize<Dictionary<string, object>>(body);

    // Perform your logic here
    Console.WriteLine("Webhook received!");

    return Results.Ok(new { status = "received" });
});

bool VerifySignature(string payload, string signature)
{
    var secret = "your-secret-token";
    using var hmac = new HMACSHA256(Encoding.UTF8.GetBytes(secret));
    var hash = hmac.ComputeHash(Encoding.UTF8.GetBytes(payload));
    var hashString = "sha256=" + BitConverter.ToString(hash).Replace("-", "").ToLower();

    return hashString == signature;
}

app.Run();
```

## ⚠️ Common Challenges & Solutions
- **Server down**: Use sender-side **retry logic**.
- **Duplicate events**: Store and check **event_id**.
- **Slow processing**: Return `200 OK`, handle tasks in **background**.
- **Spoofing**: Validate **signatures**.

## 🛑 Preventing Duplicate Processing
- Track and ignore previously seen **event IDs**.
- Make handlers **idempotent**.
- Use **timestamps** cautiously for deduplication.

## 🔁 Response to Sender
- Return `200 OK` quickly.
- Optionally return JSON: `{"status": "received"}`.
- Use `202 Accepted` for **async** processing.

## 🧬 GitHub Webhooks
- **Events**: `push`, `pull_request`, `issues`, etc.
- GitHub sends a **JSON payload** + headers:
  - `X-GitHub-Event`
  - `X-GitHub-Delivery` (unique ID)
  - `X-Hub-Signature-256`

