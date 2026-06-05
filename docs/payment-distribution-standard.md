# Payment Distribution Standard

This document defines the standard for integrating payment distribution, currency conversions, and crypto market data
into the registry.

## Overview

The payment distribution system enables:
- Multi-currency payment processing
- Real-time crypto market data integration
- Fiat currency conversions
- Distribution channels for digital assets
- Payment gateway integrations

## JSON Schema - Payment Method

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier for the payment method"
    },
    "name": {
      "type": "string",
      "description": "Human-readable name"
    },
    "type": {
      "type": "string",
      "enum": [
        "crypto",
        "bank-transfer",
        "card",
        "paypal",
        "stripe",
        "wire-transfer"
      ],
      "description": "Type of payment method"
    },
    "currencies": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "code": {
            "type": "string",
            "description": "Currency code (BTC, ETH, USD, EUR, etc.)"
          },
          "name": {
            "type": "string",
            "description": "Currency full name"
          },
          "type": {
            "type": "string",
            "enum": ["fiat", "crypto"],
            "description": "Currency type"
          },
          "decimals": {
            "type": "integer",
            "description": "Number of decimal places"
          }
        },
        "required": ["code", "name", "type"]
      }
    },
    "supported": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Array of supported regions/countries (ISO 3166-1 alpha-2 codes)"
    },
    "minimumAmount": {
      "type": "number",
      "description": "Minimum transaction amount"
    },
    "maximumAmount": {
      "type": "number",
      "description": "Maximum transaction amount (null for unlimited)"
    },
    "fees": {
      "type": "object",
      "properties": {
        "percentage": {
          "type": "number",
          "description": "Percentage fee"
        },
        "fixed": {
          "type": "number",
          "description": "Fixed fee amount"
        },
        "currency": {
          "type": "string",
          "description": "Currency of fixed fee"
        }
      }
    },
    "processingTime": {
      "type": "string",
      "description": "Expected processing time (e.g., '5-30 minutes', 'instant')"
    },
    "apiEndpoint": {
      "type": "string",
      "description": "API endpoint for integration"
    },
    "documentation": {
      "type": "string",
      "description": "Link to payment provider documentation"
    }
  },
  "required": [
    "id",
    "name",
    "type",
    "currencies"
  ]
}
```

## JSON Schema - Market Data Source

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier for the data source"
    },
    "name": {
      "type": "string",
      "description": "Name of the market data provider"
    },
    "url": {
      "type": "string",
      "description": "Provider URL"
    },
    "apiEndpoint": {
      "type": "string",
      "description": "API endpoint for market data"
    },
    "dataPoints": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Available data (price, volume, marketcap, change24h, etc.)"
    },
    "updateFrequency": {
      "type": "string",
      "description": "How often data is updated (e.g., 'real-time', '1m', '5m')"
    },
    "supportedCurrencies": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Supported currency pairs and tickers"
    },
    "rateLimit": {
      "type": "object",
      "properties": {
        "requests": {
          "type": "integer",
          "description": "Number of requests allowed"
        },
        "period": {
          "type": "string",
          "description": "Time period (e.g., '1m', '1h')"
        },
        "tier": {
          "type": "string",
          "description": "Free, paid, or premium"
        }
      }
    },
    "authentication": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": ["api-key", "oauth", "none"]
        },
        "required": { "type": "boolean" }
      }
    }
  },
  "required": [
    "id",
    "name",
    "apiEndpoint",
    "dataPoints"
  ]
}
```

## Global Market Data Links

### Cryptocurrency Price & Market Data
- **CoinGecko** - https://www.coingecko.com/
  - Free API: https://api.coingecko.com/api/v3
  - Real-time prices, charts, market data

- **CoinMarketCap** - https://coinmarketcap.com/
  - Professional API: https://pro.coinmarketcap.com/
  - Market cap, volume, dominance data

- **Kraken** - https://www.kraken.com/
  - API: https://docs.kraken.com/rest/
  - Exchange rates, OHLC data

- **Binance** - https://www.binance.com/
  - API: https://binance-docs.github.io/apidocs/
  - Real-time market data, 24h volumes

- **Gemini** - https://www.gemini.com/
  - API: https://docs.gemini.com/
  - Price ticker, order book data

### Fiat Currency Conversion
- **Open Exchange Rates** - https://openexchangerates.org/
  - Real-time and historical exchange rates

- **Fixer.io** - https://fixer.io/
  - European Central Bank rates

- **XE** - https://www.xe.com/
  - Currency conversion and data

### Global Payment Processors
- **Stripe** - https://stripe.com/
  - Multi-currency payments
  - API: https://stripe.com/docs/api

- **PayPal** - https://www.paypal.com/
  - Multi-currency support
  - API: https://developer.paypal.com/

- **2Checkout** (Verifone) - https://www.verifone.com/
  - Global payment processing

- **Wise** - https://wise.com/
  - International money transfers
  - API: https://wise.com/gb/business/api

### Crypto Payment Gateways
- **BTCPay Server** - https://btcpayserver.org/
  - Open source, self-hosted
  - BTC, Lightning Network support

- **Coinbase Commerce** - https://commerce.coinbase.com/
  - Multi-currency crypto payments
  - API: https://developers.coinbase.com/docs/commerce

- **Blockchair** - https://blockchair.com/
  - Multi-blockchain data
  - API: https://blockchair.com/api

- **TheGraph** - https://thegraph.com/
  - Blockchain indexing protocol
  - Query blockchain data via GraphQL

### Market Data Aggregators
- **Messari** - https://messari.io/
  - On-chain and market data

- **Glassnode** - https://glassnode.com/
  - On-chain analytics

- **CryptoCompare** - https://www.cryptocompare.com/
  - Comprehensive crypto data
  - API: https://min-api.cryptocompare.com/

## Implementation Guide

To implement payment distribution:

1. Create a payment method definition following the schema
2. Register supported currencies and fees
3. Integrate with market data sources for real-time pricing
4. Implement currency conversion using external APIs
5. Set up webhook handlers for payment notifications
6. Test in sandbox environments first

## Verify your definition

Use [JSON Schema Validator](https://www.jsonschemavalidator.net/) to verify compliance.
