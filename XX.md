NIP-XX
======

Escrow
-------------

`draft` `optional` `author:PatrickGeyer`

The purpose of this NIP is to allow nostr apps to coordinate to find escrow services for specific nostr applications.

## Terms

- `buyer` - NOSTR user that is making the payment
- `seller` - NOSTR user that is providing a good/service
- `escrow` - NOSTR user that is providing escrow services

## `Escrow` publishing/updating services (event)

### Event `30100`: Create or update a service.

**Event Content**:
```json
{
    "id": <String, UUID generated by the merchant. Sequential IDs (`0`, `1`, `2`...) are discouraged>,
    "maxTime": "P(n)Y(n)M(n)DT(n)H(n)M(n)S", <String, ISO 8601 duration format>
    "minTime": "P(n)Y(n)M(n)DT(n)H(n)M(n)S", <String, ISO 8601 duration format>

    // ABI only attached in case of EVM escrow contract
    "contract_address": <EVM hex address>,
    "abi": [
        {
            "0": "100", // Flat fee zero duration, sats
            "0_percent": "0.1", // Flat fee zero duration, percent
            "P(n)Y(n)M(n)DT(n)H(n)M(n)S": "0.1", // Percent per unit time
        }
    ]
}

```
**Event Tags**:
```json
  "tags": [["type", <EMV | .. further types to be added>]],
  "kinds": [10101, 10102] // Kinds of events that this escrow will arbitrate
```
 - the `d` tag is required by [NIP33](https://github.com/nostr-protocol/nips/blob/master/33.md). Its value MUST be the same as the previous listing nostr event `id`