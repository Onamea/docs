# Onamea CRDT

A Conflict Free Replicated Datatype, using operations to build both Identities (by NameKeys) and regular Items (by String Ids). The Raw form of an Operation (multiline text) can be signed and wrapped in a Message.

## Operation types

- CREATE (0)
- SET (1)
- DELETE (2)
- GRANT (3)
- REVOKE (4)
- VOUCH (5)
- DENOUNCE (6)
- RELATE (7)
- UNRELATE (8)
- REVERT (9)

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
  hash: "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
  id: "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  type: "CREATE"
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
*note that OperationType is display by it's index for all Operations except CREATE
```
Vanice@EP3TH0TB0WQEEU879EEVB9YA078MDDFC7NU4XQ21N8GWB03
888c9de90960b315f36bd5b19cfb3b169751bcf47bdb0579c120c2281d935155
b14a448eceb822f374b15ab5ff77d61c4b4fae66a72679ed1a0b68d27d6343c5
1
onamea.com
```
```JSON
{
  id: "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  previousHash: "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
  hash: "6f68891beed9f167af9fd388c88885b9ddafacd728e6d6a75abb57904f170a0c",
  type: "SET",
  body: "onamea.com"
}
```

### Reduced State Object

```JSON
{
  "id": "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  "name": "Vanice",
  "fingerprintDisplay": "⚽🦋🏁💡🔥✒️⭐⏰☁️🔥🎵⚽✈️⚡️🔑🔑🏠🎁☔️☕️🎄💪⭐☔️🏁🎄🔑⭐💪🔑🎵❤️💪✈️☁️🔥👍👍⭐☕️⭐❤️☔️🌙🙏🎁🏠🎄☀️🌙☀️😀",
  "publicKeyDisplay": "e2aa1638997e2d6f3186416023332db7a7fdf7124392572c6c9913a1984a4df2",
  "body": "onamea.com",
  "tombstone": false,
  "subKeys": [],
  "referents": [],
  "relations": [],
  "operations": [
    {
      hash: "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
      id: "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
      type: "CREATE"
    },
    {
      id: "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
      previousHash: "26979df4824477a1f432f7be43016ddba51d6108aaa96c260c7ad7f742acdda3",
      hash: "6f68891beed9f167af9fd388c88885b9ddafacd728e6d6a75abb57904f170a0c",
      type: "SET",
      body: "onamea.com"
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
  raw: "Onamea@8Y9NT9WP2UTGA2SNUXVBP6PD2K4KAT0Q0H9NTD8NRFJ07G0",
  cryptoName: "Ed25519",
  publicKey: "055547291f4d749ed85bd4142cd77ee2ec6b345324d5a05c114d74d4570f900f",
  signature: "3c7f020a53e54a40fedde7f3e15925d6d277f9f0fc92c8a2da156283270e2e8689836f4186db268d64e2d1e2480629422a7d84fe44cda327b5cb23f72b079b0a",
  datetime: 1786810212817
}
```
