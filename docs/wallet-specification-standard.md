# Wallet Specification Standard

In order to have your wallet properly integrated into our registry, we require you to stick to the following standard
to make sure that clients will be able to properly handle your wallet definition.

## JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier for the wallet (e.g., metamask, ledger, trust-wallet)"
    },
    "name": {
      "type": "string",
      "description": "Human-readable name of the wallet"
    },
    "description": {
      "type": "string",
      "description": "Brief description of the wallet"
    },
    "website": {
      "type": "string",
      "description": "Official website URL"
    },
    "logo": {
      "type": "string",
      "description": "URL to wallet logo/icon"
    },
    "type": {
      "type": "string",
      "enum": [
        "browser-extension",
        "mobile",
        "desktop",
        "hardware",
        "web",
        "cli"
      ],
      "description": "Type of wallet"
    },
    "supportedChains": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Array of supported chain network IDs"
    },
    "supportedInterfaces": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": ["evm", "cosmos"]
      },
      "description": "Supported blockchain interfaces"
    },
    "features": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Wallet features (e.g., staking, swap, nft-support, multi-sig)"
    },
    "security": {
      "type": "object",
      "properties": {
        "hasAudit": {
          "type": "boolean"
        },
        "auditLink": {
          "type": "string"
        },
        "openSource": {
          "type": "boolean"
        },
        "githubRepository": {
          "type": "string"
        }
      }
    },
    "platforms": {
      "type": "object",
      "properties": {
        "ios": {
          "type": "object",
          "properties": {
            "available": { "type": "boolean" },
            "appStore": { "type": "string" }
          }
        },
        "android": {
          "type": "object",
          "properties": {
            "available": { "type": "boolean" },
            "playStore": { "type": "string" }
          }
        },
        "chrome": {
          "type": "object",
          "properties": {
            "available": { "type": "boolean" },
            "storeLink": { "type": "string" }
          }
        },
        "firefox": {
          "type": "object",
          "properties": {
            "available": { "type": "boolean" },
            "storeLink": { "type": "string" }
          }
        }
      }
    },
    "contact": {
      "type": "object",
      "properties": {
        "twitter": { "type": "string" },
        "discord": { "type": "string" },
        "email": { "type": "string" }
      }
    }
  },
  "required": [
    "id",
    "name",
    "type",
    "supportedChains",
    "supportedInterfaces"
  ]
}
```

## Verify your definition

In order to verify that your wallet definition adheres to the above standard, you can use tools such as
[JSON Schema Validator](https://www.jsonschemavalidator.net/).
