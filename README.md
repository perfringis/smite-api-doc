# SMITE API

## Ping

A quick way of validating access to the Hi-Rez API.

```
GET /ping[ResponseFormat]
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/pingjson -H "Accept: application/json"
```

### Example response

```
SmiteAPI (ver 3.24.0.18748) [PATCH - 8.12] - Ping successful. Server Date:1/8/2022 5:31:05 PM_msg": "Approved"
```

## Create session

A required step to Authenticate the developerId/signature for further API use.

```
GET /createsession[ResponseFormat]/{developerId}/{signature}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |
| developerId | `String` | It is a credential provided by hirez studio |
| signature | `String` | md5 hash(more details in link)|
| timestamp | `String` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/createsessionjson/2117/63BBF96186ECB0485C9804727EB4FD2F/20220109090504 -H "Accept: application/json"
```

### Example response

```json
{
    ret_msg: 'Approved',
    session_id: '96AD8C1A916E461686240EE30D4E67EF',
    timestamp: '1/9/2022 09:05:04 AM'
}
```