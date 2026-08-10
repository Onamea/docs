# Onamea CRDT

A Conflict Free Replicated Datatype, using operations to build both Identities (by NameKeys) and regular Items (by String Ids). An Operation can be signed into Message.

## Operation types

- CREATE
- SET
- DELETE
- GRANT
- REVOKE
- VOUCH
- DENOUNCE
- RELATE
- UNRELATE
- REVERT

### Create Operation

```Typescript
type CreateOperation = {
  hash: Hash
  id: Id
  type: "CREATE"
}
```
```
Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02
```
```JSON
{
  "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "hash": "888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155",
  "type": "CREATE"
}
```

### Set Operation

```Typescript
type SetOperation = {
  id: Id
  previousHash: Hash
  type: "SET"
  hash: Hash
}
```
```
Vanice@EP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155
b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5
1
any text 
https://vanice.cloud/
line 3
```
```JSON
{
  "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "hash": "ffcd419f10025945fd167eb6e80649c156f0b2716706a17fdb75bf3eb500a412",
  "previousHash": "888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155",
  "type": "SET",
  "body": "any text \nhttps://vanice.cloud/\nline 3\n"
}
```

### Delete Operation
```Typescript
type DeleteOperation = {
  id: Id
  previousHash: Hash
  type: "DELETE"
  hash: Hash
}
```
```
Vanice@EP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
ffcd419f10025945fd167eb6e80649c156f0b2716706a17fdb75bf3eb500a412
DELETE
```
```JSON
{
  "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "hash": "a2046dc73b750a5353b1e0093dd643442e769677b96b667e76e150d1c8c692b6",
  "previousHash": "ffcd419f10025945fd167eb6e80649c156f0b2716706a17fdb75bf3eb500a412",
  "type": "DELETE"
}
```

### Reduced State Object

```JSON
{
  "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "body": "any text \nhttps://vanice.cloud/\nline 3\n",
  "tombstone": true,
  "operations": [
    {
      "hash": "888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155",
      "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
      "type": "CREATE"
    },
    {
      "hash": "ffcd419f10025945fd167eb6e80649c156f0b2716706a17fdb75bf3eb500a412",
      "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
      "previousHash": "888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155",
      "type": "SET",
      "body": "any text \nhttps://vanice.cloud/\nline 3\n"
    },
    {
      "hash": "a2046dc73b750a5353b1e0093dd643442e769677b96b667e76e150d1c8c692b6",
      "id": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
      "previousHash": "ffcd419f10025945fd167eb6e80649c156f0b2716706a17fdb75bf3eb500a412",
      "type": "DELETE"
    }
  ],
  "relations": [],
  "primaryKey": "VAN1CE4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "name": "Vanice",
  "fingerprintDisplay": "⚽🦋🏁💡🔥✒️⭐⏰☁️🔥🎵⚽✈️⚡️🔑🔑🏠🎁☔️☕️🎄💪⭐☔️🏁🎄🔑⭐💪🔑🎵❤️💪✈️☁️🔥👍👍⭐☕️⭐❤️☔️🌙🙏🎁🏠🎄☀️🌙☀️😀",
  "publicKeyDisplay": "e2aa1638997e2d6f3186416023332db7a7fdf7124392572c6c9913a1984a4df2",
  "subKeys": [],
  "referents": []
}
```

### Message

```Typescript
type Message = {
  raw: RawOperation
  cryptoName: CryptoName
  publicKey: PublicKeyDisplay
  signature: SignatureDisplay
  datetime?: Datetime
}
```
```JSON
{
  "raw": "Vanice@4SFRPPXCC685G26CSDPXKYUWRJ8E95EB3CK49T362A9QS02",
  "cryptoName": "Schnorr",
  "publicKey": "e2aa1638997e2d6f3186416023332db7a7fdf7124392572c6c9913a1984a4df2",
  "signature": "4a7b4e2831aa3c35405ce90ba486a44eaca50f01174f847a23df195613fd77c6f35f027ac2335c9ac90cd8e814fdfa3e61178dc8ab3ec02a645a8d6b79920202",
  "datetime": 1768236684322
}
```
