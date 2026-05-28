# Telegram Notification Template

Use this as a reference for customizing the message sent to Telegram in the **Review via Telegram** node.

## Default Template

```
🗞 Draft Tweet:

{{ $json.text }}

Approve to save to Google Sheets?
```

## Customization Ideas

You can enrich the notification with more context from the news item:

```
🗞 Draft Tweet:

{{ $json.text }}

📅 Date: {{ $now.toFormat('MMMM d, yyyy') }}
🔗 Source: {{ $('Fetch News').item.json.link }}

Approve to post?
```

## Button Labels

In the **Review via Telegram** node, you can change the button labels:
- Approve button: default is ✅ **Approve**
- Reject button: default is ❌ **Skip** (customizable via `disapproveLabel`)
