# Onamea CRDT

A Conflict Free Replicated Datatype, using operations to build both Identities (by NameKeys) and regular Items (by String Ids). The Raw form of an Operation (multiline text) can be signed and wrapped in a Message.

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
  id: Id
  hash: Hash
  type: "CREATE"
}
```
**raw**

*note that a RawOperation for a CREATE is just a string of the Identity / Id*
```
Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0
```
```JSON
{
  "hash": "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
  "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  "type": "CREATE"
}
```

### Set Operation

```Typescript
type SetOperation = {
  id: Id
  previousHash: Hash
  hash: Hash
  type: "SET"
  body: string
}
```
**raw**

```
Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0
26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3
SET
onamea.com
```
```JSON
{
  "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  "previousHash": "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
  "hash": "5363b6a504513c0a39d1d10ea871cc00427dbae39684f1715c1b640bfc3682ac",
  "type": "SET",
  "body": "onamea.com"
}
```

### Reduced State Object

```JSON
{
  "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  "name": "Vanice",
  "fingerprintDisplay": "💪🎄⚽☀️☔️🦋💪🍴☃️🏠☔️🎄❤️🦋✒️🔑☁️☁️⏰💪👍😀⚽🌙☔️⚡️🔑🏠🎄🚀☃️☃️💡✈️🎵🎉🚀🏁🎁🚗🔥⚽⚽⏰⚡️🎁💡🚗☔️🎉🏠🎁",
  "publicKeyDisplay": "e2aa1638997e2d6f3186416023332db7a7fdf7124392572c6c9913a1984a4df2",
  "body": "onamea.com",
  "tombstone": false,
  "subKeys": [],
  "referents": [],
  "relations": [],
  "operations": [
    {
      "hash": "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
      "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
      "type": "CREATE"
    },
    {
      "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
      "previousHash": "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
      "hash": "5363b6a504513c0a39d1d10ea871cc00427dbae39684f1715c1b640bfc3682ac",
      "type": "SET",
      "body": "onamea.com"
    }
  ]
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
  "raw": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  "cryptoName": "Ed25519",
  "publicKey": "055547291f4d749ed85bd4142cd77ee2ec6b345324d5a05c114d74d4570f900f",
  "signature": "3c7f020a53e54a40fedde7f3e15925d6d277f9f0fc92c8a2da156283270e2e8689836f4186db268d64e2d1e2480629422a7d84fe44cda327b5cb23f72b079b0a",
  "datetime": 1786810212817
}
```
