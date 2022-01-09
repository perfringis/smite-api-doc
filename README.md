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
| signature | `String` | md5 hash(more details in link) |
| timestamp | `String` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/createsessionjson/2117/63BBF96186ECB0485C9804727EB4FD2F/20220109090504 -H "Accept: application/json"
```

### Example response

```json
{
  "ret_msg": "Approved",
  "session_id": "96AD8C1A916E461686240EE30D4E67EF",
  "timestamp": "1/9/2022 09:05:04 AM"
}
```

## Test session

A means of validating that a session is established.

```
GET /testsession[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |
| developerId | `String` | It is a credential provided by hirez studio |
| signature | `String` | md5 hash(more details in link) |
| session | `String` | Session id created by createsession endpoint |
| timestamp | `String` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/testsessionjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504 -H "Accept: application/json"
```

### Example response

```
This was a successful test with the following parameters added: developer: 4164 time: 1/9/2022 10:43:23 AM signature: 63BBF96186ECB0485C9804727EB4FD2F session: 96AD8C1A916E461686240EE30D4E67EF
```

## Get data used

Returns API Developer daily usage limits and the current status against those limits.

```
GET /getdataused[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |
| developerId | `String` | It is a credential provided by hirez studio |
| signature | `String` | md5 hash(more details in link) |
| session | `String` | Session id created by createsession endpoint |
| timestamp | `String` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getdatausedjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504 -H "Accept: application/json"
```

### Example response

```json
[
  {
    "Active_Sessions": 1,
    "Concurrent_Sessions": 50,
    "Request_Limit_Daily": 7500,
    "Session_Cap": 500,
    "Session_Time_Limit": 15,
    "Total_Requests_Today": 8,
    "Total_Sessions_Today": 6,
    "ret_msg": null
  }
]
```

## Get HIREZ server status

Function returns UP/DOWN status for the primary game/platform environments.  Data is cached once a minute.

```
GET /gethirezserverstatus[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `String` | "json" or "xml" value |
| developerId | `String` | It is a credential provided by hirez studio |
| signature | `String` | md5 hash(more details in link) |
| session | `String` | Session id created by createsession endpoint |
| timestamp | `String` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/gethirezserverstatusjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504 -H "Accept: application/json"
```

### Example response

```json
[
  {
    "entry_datetime": "2022-01-09 10:55:10.134",
    "environment": "live",
    "limited_access": false,
    "platform": "pc",
    "ret_msg": null,
    "status": "UP",
    "version": "8.12.6904.8"
  },
  {
    "entry_datetime": "2022-01-09 10:55:10.134",
    "environment": "live",
    "limited_access": false,
    "platform": "switch",
    "ret_msg": null,
    "status": "UP",
    "version": "8.12.6904.8"
  },
  {
    "entry_datetime": "2022-01-09 10:55:10.134",
    "environment": "live",
    "limited_access": false,
    "platform": "xbox",
    "ret_msg": null,
    "status": "UP",
    "version": "8.12.6904.8"
  },
  {
    "entry_datetime": "2022-01-09 10:55:10.134",
    "environment": "live",
    "limited_access": false,
    "platform": "ps4",
    "ret_msg": null,
    "status": "UP",
    "version": "8.12.6904.8"
  },
  {
    "entry_datetime": "2022-01-09 10:54:43.555",
    "environment": "pts",
    "limited_access": false,
    "platform": "pc",
    "ret_msg": null,
    "status": "UP",
    "version": "9.1.6945.1"
  }
]
```