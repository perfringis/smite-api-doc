# SMITE API

## Ping

A quick way of validating access to the Hi-Rez API.

```
GET /ping[ResponseFormat]
```
### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/pingjson -H "Accept: application/json"
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |

### Example response

```
SmiteAPI (ver 3.24.0.18748) [PATCH - 8.12] - Ping successful. Server Date:1/8/2022 5:31:05 PM_msg": "Approved"
```