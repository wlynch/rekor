


# Rekor
Rekor is a cryptographically secure, immutable transparency log for signed software releases.
  

## Informations

### Version

0.0.1

## Content negotiation

### URI Schemes
  * http

### Consumes
  * application/json

### Produces
  * application/x-pem-file
  * application/json

## All endpoints

###  entries

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| POST | /api/v1/log/entries | [create log entry](#create-log-entry) | Creates an entry in the transparency log |
| GET | /api/v1/log/entries | [get log entry by index](#get-log-entry-by-index) | Retrieves an entry and inclusion proof from the transparency log (if it exists) by index |
| GET | /api/v1/log/entries/{entryUUID} | [get log entry by UUID](#get-log-entry-by-uuid) | Get log entry and information required to generate an inclusion proof for the entry in the transparency log |
| POST | /api/v1/log/entries/retrieve | [search log query](#search-log-query) | Searches transparency log for one or more log entries |
  


###  index

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| POST | /api/v1/index/retrieve | [search index](#search-index) | Searches index by entry metadata |
  


###  pubkey

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/v1/log/publicKey | [get public key](#get-public-key) | Retrieve the public key that can be used to validate the signed tree head |
  


###  tlog

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/v1/log | [get log info](#get-log-info) | Get information about the current state of the transparency log |
| GET | /api/v1/log/proof | [get log proof](#get-log-proof) | Get information required to generate a consistency proof for the transparency log |
  


## Paths

### <span id="create-log-entry"></span> Creates an entry in the transparency log (*createLogEntry*)

```
POST /api/v1/log/entries
```

Creates an entry in the transparency log for a detached signature, public key, and content. Items can be included in the request or fetched by the server when URLs are specified.


#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| proposedEntry | `body` | [CreateLogEntryBody](#create-log-entry-body) | `CreateLogEntryBody` | | ✓ | |  |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [201](#create-log-entry-201) | Created | Returns the entry created in the transparency log | ✓ | [schema](#create-log-entry-201-schema) |
| [400](#create-log-entry-400) | Bad Request | The content supplied to the server was invalid |  | [schema](#create-log-entry-400-schema) |
| [409](#create-log-entry-409) | Conflict | The request conflicts with the current state of the transparency log | ✓ | [schema](#create-log-entry-409-schema) |
| [default](#create-log-entry-default) | | There was an internal error in the server while processing the request |  | [schema](#create-log-entry-default-schema) |

#### Responses


##### <span id="create-log-entry-201"></span> 201 - Returns the entry created in the transparency log
Status: Created

###### <span id="create-log-entry-201-schema"></span> Schema
   
  

map of [CreateLogEntryCreatedBodyAnon](#create-log-entry-created-body-anon)

###### Response headers

| Name | Type | Go type | Separator | Default | Description |
|------|------|---------|-----------|---------|-------------|
| ETag | string | `string` |  |  | UUID of log entry |
| Location | uri (formatted string) | `strfmt.URI` |  |  | URI location of log entry |

##### <span id="create-log-entry-400"></span> 400 - The content supplied to the server was invalid
Status: Bad Request

###### <span id="create-log-entry-400-schema"></span> Schema
   
  

[CreateLogEntryBadRequestBody](#create-log-entry-bad-request-body)

##### <span id="create-log-entry-409"></span> 409 - The request conflicts with the current state of the transparency log
Status: Conflict

###### <span id="create-log-entry-409-schema"></span> Schema
   
  

[CreateLogEntryConflictBody](#create-log-entry-conflict-body)

###### Response headers

| Name | Type | Go type | Separator | Default | Description |
|------|------|---------|-----------|---------|-------------|
| Location | uri (formatted string) | `strfmt.URI` |  |  |  |

##### <span id="create-log-entry-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="create-log-entry-default-schema"></span> Schema

  

[CreateLogEntryDefaultBody](#create-log-entry-default-body)

###### Inlined models

**<span id="create-log-entry-bad-request-body"></span> CreateLogEntryBadRequestBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="create-log-entry-body"></span> CreateLogEntryBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |



**<span id="create-log-entry-conflict-body"></span> CreateLogEntryConflictBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="create-log-entry-created-body-anon"></span> CreateLogEntryCreatedBodyAnon**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| attestation | [CreateLogEntryCreatedBodyAnonAttestation](#create-log-entry-created-body-anon-attestation)| `CreateLogEntryCreatedBodyAnonAttestation` |  | |  |  |
| body | [interface{}](#interface)| `interface{}` | ✓ | |  |  |
| integratedTime | integer| `int64` | ✓ | |  |  |
| logID | string| `string` | ✓ | | This is the SHA256 hash of the DER-encoded public key for the log at the time the entry was included in the log |  |
| logIndex | integer| `int64` | ✓ | |  |  |
| verification | [CreateLogEntryCreatedBodyAnonVerification](#create-log-entry-created-body-anon-verification)| `CreateLogEntryCreatedBodyAnonVerification` |  | |  |  |



**<span id="create-log-entry-created-body-anon-attestation"></span> CreateLogEntryCreatedBodyAnonAttestation**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| data | byte (base64 string)| `strfmt.Base64` |  | |  |  |



**<span id="create-log-entry-created-body-anon-verification"></span> CreateLogEntryCreatedBodyAnonVerification**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inclusionProof | [CreateLogEntryCreatedBodyAnonVerificationInclusionProof](#create-log-entry-created-body-anon-verification-inclusion-proof)| `CreateLogEntryCreatedBodyAnonVerificationInclusionProof` |  | |  |  |
| signedEntryTimestamp | byte (base64 string)| `strfmt.Base64` |  | | Signature over the logID, logIndex, body and integratedTime. |  |



**<span id="create-log-entry-created-body-anon-verification-inclusion-proof"></span> CreateLogEntryCreatedBodyAnonVerificationInclusionProof**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



**<span id="create-log-entry-default-body"></span> CreateLogEntryDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



### <span id="get-log-entry-by-index"></span> Retrieves an entry and inclusion proof from the transparency log (if it exists) by index (*getLogEntryByIndex*)

```
GET /api/v1/log/entries
```

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| logIndex | `query` | integer | `int64` |  | ✓ |  | specifies the index of the entry in the transparency log to be retrieved |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-log-entry-by-index-200) | OK | the entry in the transparency log requested along with an inclusion proof |  | [schema](#get-log-entry-by-index-200-schema) |
| [404](#get-log-entry-by-index-404) | Not Found | The content requested could not be found |  | [schema](#get-log-entry-by-index-404-schema) |
| [default](#get-log-entry-by-index-default) | | There was an internal error in the server while processing the request |  | [schema](#get-log-entry-by-index-default-schema) |

#### Responses


##### <span id="get-log-entry-by-index-200"></span> 200 - the entry in the transparency log requested along with an inclusion proof
Status: OK

###### <span id="get-log-entry-by-index-200-schema"></span> Schema
   
  

map of [GetLogEntryByIndexOKBodyAnon](#get-log-entry-by-index-o-k-body-anon)

##### <span id="get-log-entry-by-index-404"></span> 404 - The content requested could not be found
Status: Not Found

###### <span id="get-log-entry-by-index-404-schema"></span> Schema

##### <span id="get-log-entry-by-index-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="get-log-entry-by-index-default-schema"></span> Schema

  

[GetLogEntryByIndexDefaultBody](#get-log-entry-by-index-default-body)

###### Inlined models

**<span id="get-log-entry-by-index-default-body"></span> GetLogEntryByIndexDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="get-log-entry-by-index-o-k-body-anon"></span> GetLogEntryByIndexOKBodyAnon**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| attestation | [GetLogEntryByIndexOKBodyAnonAttestation](#get-log-entry-by-index-o-k-body-anon-attestation)| `GetLogEntryByIndexOKBodyAnonAttestation` |  | |  |  |
| body | [interface{}](#interface)| `interface{}` | ✓ | |  |  |
| integratedTime | integer| `int64` | ✓ | |  |  |
| logID | string| `string` | ✓ | | This is the SHA256 hash of the DER-encoded public key for the log at the time the entry was included in the log |  |
| logIndex | integer| `int64` | ✓ | |  |  |
| verification | [GetLogEntryByIndexOKBodyAnonVerification](#get-log-entry-by-index-o-k-body-anon-verification)| `GetLogEntryByIndexOKBodyAnonVerification` |  | |  |  |



**<span id="get-log-entry-by-index-o-k-body-anon-attestation"></span> GetLogEntryByIndexOKBodyAnonAttestation**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| data | byte (base64 string)| `strfmt.Base64` |  | |  |  |



**<span id="get-log-entry-by-index-o-k-body-anon-verification"></span> GetLogEntryByIndexOKBodyAnonVerification**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inclusionProof | [GetLogEntryByIndexOKBodyAnonVerificationInclusionProof](#get-log-entry-by-index-o-k-body-anon-verification-inclusion-proof)| `GetLogEntryByIndexOKBodyAnonVerificationInclusionProof` |  | |  |  |
| signedEntryTimestamp | byte (base64 string)| `strfmt.Base64` |  | | Signature over the logID, logIndex, body and integratedTime. |  |



**<span id="get-log-entry-by-index-o-k-body-anon-verification-inclusion-proof"></span> GetLogEntryByIndexOKBodyAnonVerificationInclusionProof**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



### <span id="get-log-entry-by-uuid"></span> Get log entry and information required to generate an inclusion proof for the entry in the transparency log (*getLogEntryByUUID*)

```
GET /api/v1/log/entries/{entryUUID}
```

Returns the entry, root hash, tree size, and a list of hashes that can be used to calculate proof of an entry being included in the transparency log

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| entryUUID | `path` | string | `string` |  | ✓ |  | the UUID of the entry for which the inclusion proof information should be returned |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-log-entry-by-uuid-200) | OK | Information needed for a client to compute the inclusion proof |  | [schema](#get-log-entry-by-uuid-200-schema) |
| [404](#get-log-entry-by-uuid-404) | Not Found | The content requested could not be found |  | [schema](#get-log-entry-by-uuid-404-schema) |
| [default](#get-log-entry-by-uuid-default) | | There was an internal error in the server while processing the request |  | [schema](#get-log-entry-by-uuid-default-schema) |

#### Responses


##### <span id="get-log-entry-by-uuid-200"></span> 200 - Information needed for a client to compute the inclusion proof
Status: OK

###### <span id="get-log-entry-by-uuid-200-schema"></span> Schema
   
  

map of [GetLogEntryByUUIDOKBodyAnon](#get-log-entry-by-uuid-o-k-body-anon)

##### <span id="get-log-entry-by-uuid-404"></span> 404 - The content requested could not be found
Status: Not Found

###### <span id="get-log-entry-by-uuid-404-schema"></span> Schema

##### <span id="get-log-entry-by-uuid-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="get-log-entry-by-uuid-default-schema"></span> Schema

  

[GetLogEntryByUUIDDefaultBody](#get-log-entry-by-uuid-default-body)

###### Inlined models

**<span id="get-log-entry-by-uuid-default-body"></span> GetLogEntryByUUIDDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="get-log-entry-by-uuid-o-k-body-anon"></span> GetLogEntryByUUIDOKBodyAnon**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| attestation | [GetLogEntryByUUIDOKBodyAnonAttestation](#get-log-entry-by-uuid-o-k-body-anon-attestation)| `GetLogEntryByUUIDOKBodyAnonAttestation` |  | |  |  |
| body | [interface{}](#interface)| `interface{}` | ✓ | |  |  |
| integratedTime | integer| `int64` | ✓ | |  |  |
| logID | string| `string` | ✓ | | This is the SHA256 hash of the DER-encoded public key for the log at the time the entry was included in the log |  |
| logIndex | integer| `int64` | ✓ | |  |  |
| verification | [GetLogEntryByUUIDOKBodyAnonVerification](#get-log-entry-by-uuid-o-k-body-anon-verification)| `GetLogEntryByUUIDOKBodyAnonVerification` |  | |  |  |



**<span id="get-log-entry-by-uuid-o-k-body-anon-attestation"></span> GetLogEntryByUUIDOKBodyAnonAttestation**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| data | byte (base64 string)| `strfmt.Base64` |  | |  |  |



**<span id="get-log-entry-by-uuid-o-k-body-anon-verification"></span> GetLogEntryByUUIDOKBodyAnonVerification**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inclusionProof | [GetLogEntryByUUIDOKBodyAnonVerificationInclusionProof](#get-log-entry-by-uuid-o-k-body-anon-verification-inclusion-proof)| `GetLogEntryByUUIDOKBodyAnonVerificationInclusionProof` |  | |  |  |
| signedEntryTimestamp | byte (base64 string)| `strfmt.Base64` |  | | Signature over the logID, logIndex, body and integratedTime. |  |



**<span id="get-log-entry-by-uuid-o-k-body-anon-verification-inclusion-proof"></span> GetLogEntryByUUIDOKBodyAnonVerificationInclusionProof**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



### <span id="get-log-info"></span> Get information about the current state of the transparency log (*getLogInfo*)

```
GET /api/v1/log
```

Returns the current root hash and size of the merkle tree used to store the log entries.

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-log-info-200) | OK | A JSON object with the root hash and tree size as properties |  | [schema](#get-log-info-200-schema) |
| [default](#get-log-info-default) | | There was an internal error in the server while processing the request |  | [schema](#get-log-info-default-schema) |

#### Responses


##### <span id="get-log-info-200"></span> 200 - A JSON object with the root hash and tree size as properties
Status: OK

###### <span id="get-log-info-200-schema"></span> Schema
   
  

[GetLogInfoOKBody](#get-log-info-o-k-body)

##### <span id="get-log-info-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="get-log-info-default-schema"></span> Schema

  

[GetLogInfoDefaultBody](#get-log-info-default-body)

###### Inlined models

**<span id="get-log-info-default-body"></span> GetLogInfoDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="get-log-info-o-k-body"></span> GetLogInfoOKBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inactiveShards | [][GetLogInfoOKBodyInactiveShardsItems0](#get-log-info-o-k-body-inactive-shards-items0)| `[]*GetLogInfoOKBodyInactiveShardsItems0` |  | |  |  |
| rootHash | string| `string` | ✓ | | The current hash value stored at the root of the merkle tree |  |
| signedTreeHead | signedCheckpoint (formatted string)| `string` | ✓ | | The current signed tree head |  |
| treeID | string| `string` | ✓ | | The current treeID |  |
| treeSize | integer| `int64` | ✓ | | The current number of nodes in the merkle tree |  |



**<span id="get-log-info-o-k-body-inactive-shards-items0"></span> GetLogInfoOKBodyInactiveShardsItems0**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| rootHash | string| `string` | ✓ | | The current hash value stored at the root of the merkle tree |  |
| signedTreeHead | signedCheckpoint (formatted string)| `string` | ✓ | | The current signed tree head |  |
| treeID | string| `string` | ✓ | | The current treeID |  |
| treeSize | integer| `int64` | ✓ | | The current number of nodes in the merkle tree |  |



### <span id="get-log-proof"></span> Get information required to generate a consistency proof for the transparency log (*getLogProof*)

```
GET /api/v1/log/proof
```

Returns a list of hashes for specified tree sizes that can be used to confirm the consistency of the transparency log

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| firstSize | `query` | integer | `int64` |  |  | `1` | The size of the tree that you wish to prove consistency from (1 means the beginning of the log) Defaults to 1 if not specified |
| lastSize | `query` | integer | `int64` |  | ✓ |  | The size of the tree that you wish to prove consistency to |
| treeID | `query` | string | `string` |  |  |  | The tree ID of the tree that you wish to prove consistency for |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-log-proof-200) | OK | All hashes required to compute the consistency proof |  | [schema](#get-log-proof-200-schema) |
| [400](#get-log-proof-400) | Bad Request | The content supplied to the server was invalid |  | [schema](#get-log-proof-400-schema) |
| [default](#get-log-proof-default) | | There was an internal error in the server while processing the request |  | [schema](#get-log-proof-default-schema) |

#### Responses


##### <span id="get-log-proof-200"></span> 200 - All hashes required to compute the consistency proof
Status: OK

###### <span id="get-log-proof-200-schema"></span> Schema
   
  

[GetLogProofOKBody](#get-log-proof-o-k-body)

##### <span id="get-log-proof-400"></span> 400 - The content supplied to the server was invalid
Status: Bad Request

###### <span id="get-log-proof-400-schema"></span> Schema
   
  

[GetLogProofBadRequestBody](#get-log-proof-bad-request-body)

##### <span id="get-log-proof-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="get-log-proof-default-schema"></span> Schema

  

[GetLogProofDefaultBody](#get-log-proof-default-body)

###### Inlined models

**<span id="get-log-proof-bad-request-body"></span> GetLogProofBadRequestBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="get-log-proof-default-body"></span> GetLogProofDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="get-log-proof-o-k-body"></span> GetLogProofOKBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| hashes | []string| `[]string` | ✓ | |  |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |



### <span id="get-public-key"></span> Retrieve the public key that can be used to validate the signed tree head (*getPublicKey*)

```
GET /api/v1/log/publicKey
```

Returns the public key that can be used to validate the signed tree head

#### Produces
  * application/x-pem-file

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| treeID | `query` | string | `string` |  |  |  | The tree ID of the tree you wish to get a public key for |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-public-key-200) | OK | The public key |  | [schema](#get-public-key-200-schema) |
| [default](#get-public-key-default) | | There was an internal error in the server while processing the request |  | [schema](#get-public-key-default-schema) |

#### Responses


##### <span id="get-public-key-200"></span> 200 - The public key
Status: OK

###### <span id="get-public-key-200-schema"></span> Schema
   
  



##### <span id="get-public-key-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="get-public-key-default-schema"></span> Schema

  

[GetPublicKeyDefaultBody](#get-public-key-default-body)

###### Inlined models

**<span id="get-public-key-default-body"></span> GetPublicKeyDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



### <span id="search-index"></span> Searches index by entry metadata (*searchIndex*)

```
POST /api/v1/index/retrieve
```

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| query | `body` | [SearchIndexBody](#search-index-body) | `SearchIndexBody` | | ✓ | |  |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#search-index-200) | OK | Returns zero or more entry UUIDs from the transparency log based on search query |  | [schema](#search-index-200-schema) |
| [400](#search-index-400) | Bad Request | The content supplied to the server was invalid |  | [schema](#search-index-400-schema) |
| [default](#search-index-default) | | There was an internal error in the server while processing the request |  | [schema](#search-index-default-schema) |

#### Responses


##### <span id="search-index-200"></span> 200 - Returns zero or more entry UUIDs from the transparency log based on search query
Status: OK

###### <span id="search-index-200-schema"></span> Schema
   
  

[]string

##### <span id="search-index-400"></span> 400 - The content supplied to the server was invalid
Status: Bad Request

###### <span id="search-index-400-schema"></span> Schema
   
  

[SearchIndexBadRequestBody](#search-index-bad-request-body)

##### <span id="search-index-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="search-index-default-schema"></span> Schema

  

[SearchIndexDefaultBody](#search-index-default-body)

###### Inlined models

**<span id="search-index-bad-request-body"></span> SearchIndexBadRequestBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="search-index-body"></span> SearchIndexBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| email | email (formatted string)| `strfmt.Email` |  | |  |  |
| hash | string| `string` |  | |  |  |
| operator | string| `string` |  | |  |  |
| publicKey | [SearchIndexParamsBodyPublicKey](#search-index-params-body-public-key)| `SearchIndexParamsBodyPublicKey` |  | |  |  |



**<span id="search-index-default-body"></span> SearchIndexDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="search-index-params-body-public-key"></span> SearchIndexParamsBodyPublicKey**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| content | byte (base64 string)| `strfmt.Base64` |  | |  |  |
| format | string| `string` | ✓ | |  |  |
| url | uri (formatted string)| `strfmt.URI` |  | |  |  |



### <span id="search-log-query"></span> Searches transparency log for one or more log entries (*searchLogQuery*)

```
POST /api/v1/log/entries/retrieve
```

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| entry | `body` | [SearchLogQueryBody](#search-log-query-body) | `SearchLogQueryBody` | | ✓ | |  |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#search-log-query-200) | OK | Returns zero or more entries from the transparency log, according to how many were included in request query |  | [schema](#search-log-query-200-schema) |
| [400](#search-log-query-400) | Bad Request | The content supplied to the server was invalid |  | [schema](#search-log-query-400-schema) |
| [default](#search-log-query-default) | | There was an internal error in the server while processing the request |  | [schema](#search-log-query-default-schema) |

#### Responses


##### <span id="search-log-query-200"></span> 200 - Returns zero or more entries from the transparency log, according to how many were included in request query
Status: OK

###### <span id="search-log-query-200-schema"></span> Schema
   
  

[][map[string]SearchLogQueryOKBodyAnon](#map-string-search-log-query-o-k-body-anon)

##### <span id="search-log-query-400"></span> 400 - The content supplied to the server was invalid
Status: Bad Request

###### <span id="search-log-query-400-schema"></span> Schema
   
  

[SearchLogQueryBadRequestBody](#search-log-query-bad-request-body)

##### <span id="search-log-query-default"></span> Default Response
There was an internal error in the server while processing the request

###### <span id="search-log-query-default-schema"></span> Schema

  

[SearchLogQueryDefaultBody](#search-log-query-default-body)

###### Inlined models

**<span id="search-log-query-bad-request-body"></span> SearchLogQueryBadRequestBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="search-log-query-body"></span> SearchLogQueryBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| entries | [][SearchLogQueryParamsBodyEntriesItems0](#search-log-query-params-body-entries-items0)| `[]SearchLogQueryParamsBodyEntriesItems0` |  | |  |  |
| entryUUIDs | []string| `[]string` |  | |  |  |
| logIndexes | []integer| `[]*int64` |  | |  |  |



**<span id="search-log-query-default-body"></span> SearchLogQueryDefaultBody**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



**<span id="search-log-query-o-k-body-anon"></span> SearchLogQueryOKBodyAnon**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| attestation | [SearchLogQueryOKBodyAnonAttestation](#search-log-query-o-k-body-anon-attestation)| `SearchLogQueryOKBodyAnonAttestation` |  | |  |  |
| body | [interface{}](#interface)| `interface{}` | ✓ | |  |  |
| integratedTime | integer| `int64` | ✓ | |  |  |
| logID | string| `string` | ✓ | | This is the SHA256 hash of the DER-encoded public key for the log at the time the entry was included in the log |  |
| logIndex | integer| `int64` | ✓ | |  |  |
| verification | [SearchLogQueryOKBodyAnonVerification](#search-log-query-o-k-body-anon-verification)| `SearchLogQueryOKBodyAnonVerification` |  | |  |  |



**<span id="search-log-query-o-k-body-anon-attestation"></span> SearchLogQueryOKBodyAnonAttestation**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| data | byte (base64 string)| `strfmt.Base64` |  | |  |  |



**<span id="search-log-query-o-k-body-anon-verification"></span> SearchLogQueryOKBodyAnonVerification**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inclusionProof | [SearchLogQueryOKBodyAnonVerificationInclusionProof](#search-log-query-o-k-body-anon-verification-inclusion-proof)| `SearchLogQueryOKBodyAnonVerificationInclusionProof` |  | |  |  |
| signedEntryTimestamp | byte (base64 string)| `strfmt.Base64` |  | | Signature over the logID, logIndex, body and integratedTime. |  |



**<span id="search-log-query-o-k-body-anon-verification-inclusion-proof"></span> SearchLogQueryOKBodyAnonVerificationInclusionProof**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



**<span id="search-log-query-params-body-entries-items0"></span> SearchLogQueryParamsBodyEntriesItems0**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |



## Models

### <span id="consistency-proof"></span> ConsistencyProof


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| hashes | []string| `[]string` | ✓ | |  |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |



### <span id="error"></span> Error


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  |  |
| message | string| `string` |  | |  |  |



### <span id="inactive-shard-log-info"></span> InactiveShardLogInfo


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| rootHash | string| `string` | ✓ | | The current hash value stored at the root of the merkle tree |  |
| signedTreeHead | signedCheckpoint (formatted string)| `string` | ✓ | | The current signed tree head |  |
| treeID | string| `string` | ✓ | | The current treeID |  |
| treeSize | integer| `int64` | ✓ | | The current number of nodes in the merkle tree |  |



### <span id="inclusion-proof"></span> InclusionProof


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



### <span id="log-entry"></span> LogEntry


  

[LogEntry](#log-entry)

#### Inlined models

**<span id="log-entry-anon"></span> LogEntryAnon**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| attestation | [LogEntryAnonAttestation](#log-entry-anon-attestation)| `LogEntryAnonAttestation` |  | |  |  |
| body | [interface{}](#interface)| `interface{}` | ✓ | |  |  |
| integratedTime | integer| `int64` | ✓ | |  |  |
| logID | string| `string` | ✓ | | This is the SHA256 hash of the DER-encoded public key for the log at the time the entry was included in the log |  |
| logIndex | integer| `int64` | ✓ | |  |  |
| verification | [LogEntryAnonVerification](#log-entry-anon-verification)| `LogEntryAnonVerification` |  | |  |  |



**<span id="log-entry-anon-attestation"></span> LogEntryAnonAttestation**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| data | byte (base64 string)| `strfmt.Base64` |  | |  |  |



**<span id="log-entry-anon-verification"></span> LogEntryAnonVerification**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inclusionProof | [LogEntryAnonVerificationInclusionProof](#log-entry-anon-verification-inclusion-proof)| `LogEntryAnonVerificationInclusionProof` |  | |  |  |
| signedEntryTimestamp | byte (base64 string)| `strfmt.Base64` |  | | Signature over the logID, logIndex, body and integratedTime. |  |



**<span id="log-entry-anon-verification-inclusion-proof"></span> LogEntryAnonVerificationInclusionProof**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| checkpoint | signedCheckpoint (formatted string)| `string` | ✓ | | The checkpoint (signed tree head) that the inclusion proof is based on |  |
| hashes | []string| `[]string` | ✓ | | A list of hashes required to compute the inclusion proof, sorted in order from leaf to root |  |
| logIndex | integer| `int64` | ✓ | | The index of the entry in the transparency log |  |
| rootHash | string| `string` | ✓ | | The hash value stored at the root of the merkle tree at the time the proof was generated |  |
| treeSize | integer| `int64` | ✓ | | The size of the merkle tree at the time the inclusion proof was generated |  |



### <span id="log-info"></span> LogInfo


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| inactiveShards | [][LogInfoInactiveShardsItems0](#log-info-inactive-shards-items0)| `[]*LogInfoInactiveShardsItems0` |  | |  |  |
| rootHash | string| `string` | ✓ | | The current hash value stored at the root of the merkle tree |  |
| signedTreeHead | signedCheckpoint (formatted string)| `string` | ✓ | | The current signed tree head |  |
| treeID | string| `string` | ✓ | | The current treeID |  |
| treeSize | integer| `int64` | ✓ | | The current number of nodes in the merkle tree |  |



#### Inlined models

**<span id="log-info-inactive-shards-items0"></span> LogInfoInactiveShardsItems0**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| rootHash | string| `string` | ✓ | | The current hash value stored at the root of the merkle tree |  |
| signedTreeHead | signedCheckpoint (formatted string)| `string` | ✓ | | The current signed tree head |  |
| treeID | string| `string` | ✓ | | The current treeID |  |
| treeSize | integer| `int64` | ✓ | | The current number of nodes in the merkle tree |  |



### <span id="proposed-entry"></span> ProposedEntry


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |



### <span id="rekor-version"></span> RekorVersion


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| builddate | string| `string` | ✓ | |  |  |
| commit | string| `string` | ✓ | |  |  |
| treestate | string| `string` | ✓ | |  |  |
| version | string| `string` | ✓ | |  |  |



### <span id="search-index"></span> SearchIndex


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| email | email (formatted string)| `strfmt.Email` |  | |  |  |
| hash | string| `string` |  | |  |  |
| operator | string| `string` |  | |  |  |
| publicKey | [SearchIndexPublicKey](#search-index-public-key)| `SearchIndexPublicKey` |  | |  |  |



#### Inlined models

**<span id="search-index-public-key"></span> SearchIndexPublicKey**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| content | byte (base64 string)| `strfmt.Base64` |  | |  |  |
| format | string| `string` | ✓ | |  |  |
| url | uri (formatted string)| `strfmt.URI` |  | |  |  |



### <span id="search-log-query"></span> SearchLogQuery


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| entries | [][SearchLogQueryEntriesItems0](#search-log-query-entries-items0)| `[]SearchLogQueryEntriesItems0` |  | |  |  |
| entryUUIDs | []string| `[]string` |  | |  |  |
| logIndexes | []integer| `[]*int64` |  | |  |  |



#### Inlined models

**<span id="search-log-query-entries-items0"></span> SearchLogQueryEntriesItems0**


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |



### <span id="alpine"></span> alpine


> Alpine package
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for Alpine package objects |  |



### <span id="cose"></span> cose


> COSE object
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | COSE for Rekord objects |  |



### <span id="hashedrekord"></span> hashedrekord


> Hashed Rekord object
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for Rekord objects |  |



### <span id="helm"></span> helm


> Helm chart
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for Helm objects |  |



### <span id="intoto"></span> intoto


> Intoto object
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Intoto for Rekord objects |  |



### <span id="jar"></span> jar


> Java Archive (JAR)
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for JAR objects |  |



### <span id="rekord"></span> rekord


> Rekord object
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for Rekord objects |  |



### <span id="rfc3161"></span> rfc3161


> RFC3161 Timestamp
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for RFC 3161 timestamp objects |  |



### <span id="rpm"></span> rpm


> RPM package
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for RPM objects |  |



### <span id="tuf"></span> tuf


> TUF metadata
  




* inlined member (*AO0*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| kind | string| `string` | ✓ | |  |  |


* inlined member (*AO1*)



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| apiVersion | string| `string` | ✓ | |  |  |
| spec | [interface{}](#interface)| `interface{}` | ✓ | | Schema for TUF metadata objects |  |


