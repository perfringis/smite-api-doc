# SMITE API

# Connectivity, Development, & System Status

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
curl https://api.smitegame.com/smiteapi.svc/pingjson
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
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/createsessionjson/2117/63BBF96186ECB0485C9804727EB4FD2F/20220111190948
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
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/testsessionjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504
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
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getdatausedjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504
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
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/gethirezserverstatusjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504
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
  ...
]
```

## Get patch info

Function returns information about current deployed patch. Currently, this information only includes patch version.

```
GET /getpatchinfo[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getpatchinfojson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504
```

### Example response

```json
{
  "ret_msg": null, 
  "version_string": "8.12" 
}
```

# Gods/Champions & Items

## Get gods

Returns all Gods and their various attributes.

```
GET /getgods[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}/{languageCode}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |
| languageCode | `integer` | Language code(more details in link)  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getgodsjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504/1
```

### Example response

```json
[
  {
    "Ability1": "Shield of Achilles",
    "Ability2": "Radiant Glory",
    "Ability3": "Combat Dodge",
    "Ability4": "Fatal Strike",
    "Ability5": "Gift of the Gods",
    "AbilityId1": 15676,
    "AbilityId2": 15677,
    "AbilityId3": 15679,
    "AbilityId4": 15680,
    "AbilityId5": 15678,
    "Ability_1": {
      "Description": {
        "itemDescription": {
          "cooldown": "14s",
          "cost": "60/65/70/75/80",
          "description": "Achilles punches forward with the edge of his Shield, inflicting massive damage and stunning enemy targets hit by the impact. The force of his punch continues to radiate past his initial target area, dealing 85% damage to targets farther away.",
          "menuitems": [{
            "description": "Ability:",
            "value": "Cone"
          }, {
            "description": "Affects:",
            "value": "Enemies"
          }, {
            "description": "Damage:",
            "value": "Physical"
          }, {
            "description": "Range:",
            "value": "50"
          }],
          "rankitems": [{
            "description": "Damage:",
            "value": "100/155/210/265/320 (90% of your Physical Power)"
          }, {
            "description": "Stun Duration:",
            "value": "1s"
          }]
        }
      },
      "Id": 15676,
      "Summary": "Shield of Achilles",
      "URL": "https://webcdn.hirezstudios.com/smite/god-abilities/shield-of-achilles.jpg"
    },
    "Ability_2": {
      "Description": {
        "itemDescription": {
          "cooldown": "10s",
          "cost": "40/45/50/55/60",
          "description": "Achilles is blessed by the gods, giving him bonus Physical Power, Protections, and Crowd Control Reduction for 6 seconds. While this blessing is active, Achilles will heal himself upon successfully damaging enemies with abilities.",
          "menuitems": [{
            "description": "Ability:",
            "value": "Buff"
          }, {
            "description": "Affects:",
            "value": "Self"
          }],
          "rankitems": [{
            "description": "Heal:",
            "value": "20/23/26/29/32 (10% of your Physical Power)"
          }, {
            "description": "Max Heals per Ability:",
            "value": "2/2/3/3/4"
          }, {
            "description": "Physical Power:",
            "value": "+6/7/8/9/10%"
          }, {
            "description": "Protections:",
            "value": "+10/12.5/15/17.5/20%"
          }, {
            "description": "Crowd Control Reduction:",
            "value": "20%"
          }]
        }
      },
      "Id": 15677,
      "Summary": "Radiant Glory",
      "URL": "https://webcdn.hirezstudios.com/smite/god-abilities/radiant-glory.jpg"
    },
    "Ability_3": {
      "Description": {
        "itemDescription": {
          "cooldown": "14/13/12/11/10s",
          "cost": "24/28/32/36/40",
          "description": "Achilles dodges his enemies' attacks before striking them in swift response. If Achilles successfully hits an enemy god with this strike, Achilles can use this ability once more before it goes on Cooldown.",
          "menuitems": [{
            "description": "Ability:",
            "value": "Dash"
          }, {
            "description": "Affects:",
            "value": "Enemies"
          }, {
            "description": "Damage:",
            "value": "Physical"
          }, {
            "description": "Range:",
            "value": "35"
          }],
          "rankitems": [{
            "description": "Damage:",
            "value": "60/95/130/165/200 (+45% of your Physical Power)"
          }]
        }
      },
      "Id": 15679,
      "Summary": "Combat Dodge",
      "URL": "https://webcdn.hirezstudios.com/smite/god-abilities/combat-dodge.jpg"
    },
    "Ability_4": {
      "Description": {
        "itemDescription": {
          "cooldown": "90s",
          "cost": "80/85/90/95/100",
          "description": "Achilles dashes forward and attacks. While dashing, Achilles will pass through minions, stop and hit the first enemy god he encounters, dealing damage to all he hits and executing gods below 30% Health. If Achilles kills a god with this ability, he can use it again, up to 5 times. As Achilles successfully Executes his enemies, he becomes more reckless in combat and leaves his heel exposed. Achilles will become more susceptible to damage, stacking up to 5 times.",
          "menuitems": [{
            "description": "Ability:",
            "value": "Dash"
          }, {
            "description": "Affects:",
            "value": "Enemies"
          }, {
            "description": "Damage:",
            "value": "Physical"
          }, {
            "description": "Range:",
            "value": "35"
          }],
          "rankitems": [{
            "description": "Damage:",
            "value": "180/270/360/450/540 (100% of your Physical Power)"
          }, {
            "description": "Execute Threshold:",
            "value": "30%"
          }, {
            "description": "Damage Taken Increase:",
            "value": "5%"
          }]
        }
      },
      "Id": 15680,
      "Summary": "Fatal Strike",
      "URL": "https://webcdn.hirezstudios.com/smite/god-abilities/fatal-strike.jpg"
    },
    "Ability_5": {
      "Description": {
        "itemDescription": {
          "cooldown": "",
          "cost": "",
          "description": "Achilles adapts to the tide of Battle. While in the Fountain, Achilles can choose to wear armor, granting him bonus Health and Protections, or forgo it, granting him bonus Movement Speed and Physical Power. To swap, use Achilles' Basic Attack while the Passive targeter is active. ",
          "menuitems": [{
            "description": "Ability:",
            "value": "Passive"
          }],
          "rankitems": [{
            "description": "Health Bonus:",
            "value": "25 +15 per Level"
          }, {
            "description": "Protections Bonus:",
            "value": "5 +2 per Level"
          }, {
            "description": "Movement Speed Bonus:",
            "value": "1% +.25% per Level"
          }, {
            "description": "Physical Power Bonus:",
            "value": "3 +2 per Level"
          }]
        }
      },
      "Id": 15678,
      "Summary": "Gift of the Gods",
      "URL": "https://webcdn.hirezstudios.com/smite/god-abilities/gift-of-the-gods.jpg"
    },
    "AttackSpeed": 0.95,
    "AttackSpeedPerLevel": 0.012,
    "AutoBanned": "n",
    "Cons": "",
    "HP5PerLevel": 0.75,
    "Health": 475,
    "HealthPerFive": 9,
    "HealthPerLevel": 85,
    "Lore": "King Agamemnon brought his fury to bear against gilded Troy, for Prince Paris had stolen his Helen, his wife, whose beauty rivaled that of Athena and Aphrodite. To famed Achilles, invincible warrior, the king gave command of a thousand ships.\\n\\nAcross stormy seas and salted beach, soldiers sieged the city. Arrow and stone, blade and barb bounced from Achilles’ skin. Bathed as a babe in the River Styx by his Nereid mother, his hide was hardened, imperviously made. Through every charge, every death-defying battle, Achilles was at the fore. Troy hung poised to crumble.\\n\\nUntil Agamemnon gave slight to the mighty myrmidon. In grave offense, Achilles pulled his forces from the field. Hector, boldest, bravest, eldest of the Trojan princes seized the chance to push the Greeks to the sea. Water’s reflection mirrored scorching sails as Hector fired their ships. All seemed lost until Achilles rose to meet him. Fierce and fast the two titans fought, but Hector’s spear felled Achilles fair. Though Patroclus, it was, in the armor of Achilles, not Achilles who lay dead.\\n\\nWrathful at the loss of his faithful lover, Achilles donned armor newly-made and challenged Hector alone. Spear and blade and amor rang, but Achilles could not be harmed. Hector, prince of Troy, died in battle that day.\\n\\nParis, brother lost, tearful-eyed, let arrow loose, guided by divine envy. For there were Gods that could not suffer Achilles to survive. Straight and true the arrow flew and harpooned Achilles’ heel, where his mother held him when submerged. The wound was deep, his weakness found, Achilles met his end.\\n\\nA decade thence, from Hades’ depths, Achilles has been drawn. Armored now, upon the heel, revenge his only aim. For envious Gods stole from him his glory and his life. Now they tremble at the wrath of the man who cannot be harmed.",
    "MP5PerLevel": 0.39,
    "MagicProtection": 30,
    "MagicProtectionPerLevel": 0.9,
    "MagicalPower": 0,
    "MagicalPowerPerLevel": 0,
    "Mana": 205,
    "ManaPerFive": 4.7,
    "ManaPerLevel": 35,
    "Name": "Achilles",
    "OnFreeRotation": "",
    "Pantheon": "Greek",
    "PhysicalPower": 38,
    "PhysicalPowerPerLevel": 2,
    "PhysicalProtection": 17,
    "PhysicalProtectionPerLevel": 3,
    "Pros": "High Single Target Damage, High Mobility",
    "Roles": "Warrior",
    "Speed": 370,
    "Title": "Hero of the Trojan War",
    "Type": "Melee, Physical",
    "abilityDescription1": {
      "itemDescription": {
        "cooldown": "14s",
        "cost": "60/65/70/75/80",
        "description": "Achilles punches forward with the edge of his Shield, inflicting massive damage and stunning enemy targets hit by the impact. The force of his punch continues to radiate past his initial target area, dealing 85% damage to targets farther away.",
        "menuitems": [{
          "description": "Ability:",
          "value": "Cone"
        }, {
          "description": "Affects:",
          "value": "Enemies"
        }, {
          "description": "Damage:",
          "value": "Physical"
        }, {
          "description": "Range:",
          "value": "50"
        }],
        "rankitems": [{
          "description": "Damage:",
          "value": "100/155/210/265/320 (90% of your Physical Power)"
        }, {
          "description": "Stun Duration:",
          "value": "1s"
        }]
      }
    },
    "abilityDescription2": {
      "itemDescription": {
        "cooldown": "10s",
        "cost": "40/45/50/55/60",
        "description": "Achilles is blessed by the gods, giving him bonus Physical Power, Protections, and Crowd Control Reduction for 6 seconds. While this blessing is active, Achilles will heal himself upon successfully damaging enemies with abilities.",
        "menuitems": [{
          "description": "Ability:",
          "value": "Buff"
        }, {
          "description": "Affects:",
          "value": "Self"
        }],
        "rankitems": [{
          "description": "Heal:",
          "value": "20/23/26/29/32 (10% of your Physical Power)"
        }, {
          "description": "Max Heals per Ability:",
          "value": "2/2/3/3/4"
        }, {
          "description": "Physical Power:",
          "value": "+6/7/8/9/10%"
        }, {
          "description": "Protections:",
          "value": "+10/12.5/15/17.5/20%"
        }, {
          "description": "Crowd Control Reduction:",
          "value": "20%"
        }]
      }
    },
    "abilityDescription3": {
      "itemDescription": {
        "cooldown": "14/13/12/11/10s",
        "cost": "24/28/32/36/40",
        "description": "Achilles dodges his enemies' attacks before striking them in swift response. If Achilles successfully hits an enemy god with this strike, Achilles can use this ability once more before it goes on Cooldown.",
        "menuitems": [{
          "description": "Ability:",
          "value": "Dash"
        }, {
          "description": "Affects:",
          "value": "Enemies"
        }, {
          "description": "Damage:",
          "value": "Physical"
        }, {
          "description": "Range:",
          "value": "35"
        }],
        "rankitems": [{
          "description": "Damage:",
          "value": "60/95/130/165/200 (+45% of your Physical Power)"
        }]
      }
    },
    "abilityDescription4": {
      "itemDescription": {
        "cooldown": "90s",
        "cost": "80/85/90/95/100",
        "description": "Achilles dashes forward and attacks. While dashing, Achilles will pass through minions, stop and hit the first enemy god he encounters, dealing damage to all he hits and executing gods below 30% Health. If Achilles kills a god with this ability, he can use it again, up to 5 times. As Achilles successfully Executes his enemies, he becomes more reckless in combat and leaves his heel exposed. Achilles will become more susceptible to damage, stacking up to 5 times.",
        "menuitems": [{
          "description": "Ability:",
          "value": "Dash"
        }, {
          "description": "Affects:",
          "value": "Enemies"
        }, {
          "description": "Damage:",
          "value": "Physical"
        }, {
          "description": "Range:",
          "value": "35"
        }],
        "rankitems": [{
          "description": "Damage:",
          "value": "180/270/360/450/540 (100% of your Physical Power)"
        }, {
          "description": "Execute Threshold:",
          "value": "30%"
        }, {
          "description": "Damage Taken Increase:",
          "value": "5%"
        }]
      }
    },
    "abilityDescription5": {
      "itemDescription": {
        "cooldown": "",
        "cost": "",
        "description": "Achilles adapts to the tide of Battle. While in the Fountain, Achilles can choose to wear armor, granting him bonus Health and Protections, or forgo it, granting him bonus Movement Speed and Physical Power. To swap, use Achilles' Basic Attack while the Passive targeter is active. ",
        "menuitems": [{
          "description": "Ability:",
          "value": "Passive"
        }],
        "rankitems": [{
          "description": "Health Bonus:",
          "value": "25 +15 per Level"
        }, {
          "description": "Protections Bonus:",
          "value": "5 +2 per Level"
        }, {
          "description": "Movement Speed Bonus:",
          "value": "1% +.25% per Level"
        }, {
          "description": "Physical Power Bonus:",
          "value": "3 +2 per Level"
        }]
      }
    },
    "basicAttack": {
      "itemDescription": {
        "cooldown": "",
        "cost": "",
        "description": "",
        "menuitems": [{
          "description": "Damage:",
          "value": "38 + 2/Lvl (+100% of Physical Power)"
        }, {
          "description": "Progression:",
          "value": "None"
        }],
        "rankitems": []
      }
    },
    "godAbility1_URL": "https://webcdn.hirezstudios.com/smite/god-abilities/shield-of-achilles.jpg",
    "godAbility2_URL": "https://webcdn.hirezstudios.com/smite/god-abilities/radiant-glory.jpg",
    "godAbility3_URL": "https://webcdn.hirezstudios.com/smite/god-abilities/combat-dodge.jpg",
    "godAbility4_URL": "https://webcdn.hirezstudios.com/smite/god-abilities/fatal-strike.jpg",
    "godAbility5_URL": "https://webcdn.hirezstudios.com/smite/god-abilities/gift-of-the-gods.jpg",
    "godCard_URL": "https://webcdn.hirezstudios.com/smite/god-cards/achilles.jpg",
    "godIcon_URL": "https://webcdn.hirezstudios.com/smite/god-icons/achilles.jpg",
    "id": 3492,
    "latestGod": "n",
    "ret_msg": null
  },
  ...
]
```

## Get god leaderboard

Returns the current season’s leaderboard for a god/queue combination.

```
GET /getgodleaderboard[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}/{godId}/{queue}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |
| godId | `integer` | God id  |
| queue | `integer` | Queue code(more details in link)  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getgodleaderboardjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504/3492/440
```

### Example response

```json
[
  {
    "god_id": "3492",
    "losses": "0",
    "player_id": "12345678",
    "player_name": "player_name",
    "player_ranking": "85.860641",
    "rank": "1",
    "ret_msg": null,
    "wins": "12"
  },
  ...
]
```

## Get god alt abilities

Returns alt abilities for all gods.

```
GET /getgodaltabilities[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getgodaltabilitiesjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504
```

```json
[
  {
    "alt_name": "Loki V2A A02 Sub Device",
    "alt_position": "2",
    "god": "Loki",
    "god_id": 1797,
    "item_id": 18614,
    "ret_msg": null
  },
  ...
]
```

## Get god skins

Returns all available skins for a particular God.

```
GET /getgodskins[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}/{godId}/{languageCode}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |
| godId | `integer` | God id  |
| languageCode | `integer` | Language code(more details in link)  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getgodskinsjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504/3492/1
```

```json
[
  {
    "godIcon_URL": "https://webcdn.hirezstudios.com/smite/god-icons/ratatoskr.jpg",
    "godSkin_URL": "https://webcdn.hirezstudios.com/smite/god-skins/ratatoskr_standard-ratatoskr.jpg",
    "god_id": 2063,
    "god_name": "Ratatoskr",
    "obtainability": "Normal",
    "price_favor": 0,
    "price_gems": 0,
    "ret_msg": null,
    "skin_id1": 13143,
    "skin_id2": 11450,
    "skin_name": "Standard Ratatoskr"
  },
  ...
]
```

## Get god recommended items

Returns the Recommended Items for a particular God.

```
GET /getgodrecommendeditems[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}/{godid}/{languageCode}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |
| godId | `integer` | God id  |
| languageCode | `integer` | Language code(more details in link)  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getgodrecommendeditemsjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504/3492/1
```

```json
[
  {
    "Category": "Consumable",
    "Item": "Ward",
    "Role": "Standard",
    "category_value_id": 10779,
    "god_id": 2063,
    "god_name": "Ratatoskr",
    "icon_id": 1992,
    "item_id": 7668,
    "ret_msg": null,
    "role_value_id": 10770
  },
  ...
]
```

## Get items

Returns all Items and their various attributes.

```
GET /getitems[ResponseFormat]/{developerId}/{signature}/{session}/{timestamp}/{languageCode}
```

### Query parameters

| Name     | Type       | Description                           |
|----------|------------|---------------------------------------|
| ResponseFormat | `string` | "json" or "xml" value |
| developerId | `integer` | It is a credential provided by hirez studio |
| signature | `string` | md5 hash(more details in link) |
| session | `string` | Session id created by createsession endpoint |
| timestamp | `integer` | Current time(formatted 'yyyyMMddHHmmss')  |
| languageCode | `integer` | Language code(more details in link)  |

### Example request

```bash
curl https://api.smitegame.com/smiteapi.svc/getitemsjson/2117/63BBF96186ECB0485C9804727EB4FD2F/96AD8C1A916E461686240EE30D4E67EF/20220109090504/1
```

```json
[
  {
    "ActiveFlag": "y",
    "ChildItemId": 0,
    "DeviceName": "Iron Mail",
    "IconId": 2866,
    "ItemDescription": {
      "Description": "Physical Protection and Health.",
      "Menuitems": [{
        "Description": "Health",
        "Value": "+75"
      }, {
        "Description": "Physical Protection",
        "Value": "+10"
      }],
      "SecondaryDescription": null
    },
    "ItemId": 7526,
    "ItemTier": 1,
    "Price": 650,
    "RestrictedRoles": "no restrictions",
    "RootItemId": 7526,
    "ShortDesc": "Physical Protection and Health.",
    "StartingItem": false,
    "Type": "Item",
    "itemIcon_URL": "https://webcdn.hirezstudios.com/smite/item-icons/iron-mail.jpg",
    "ret_msg": null
  },
  ...
]
```