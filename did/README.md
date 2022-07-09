FairX DID Method Specification
=================
3th July 2022

# Table of Contents
1. [DID Method Name](#name)
2. [Method Specific Identifier](#identifier)
    1. [Example](#example1)
3. [DID Document](#document)
    1. [Example](#example2)
4. [JSON-LD Context Definition](#ld)
5. [CRUD Operation Definitions](#crud)
    1. [Create (Register)](#create)
    2. [Read (Resolve)](#read)
    3. [Update](#update)
    4. [Delete](#delete)
6. [Security](#security)
7. [Privacy](#privacy)
8. [References](#references)

FairX is an experimental suite of open source services that run alongside [TBD's Self-Sovereign SDK and Services](https://github.com/TBD54566975). 

FairX Decentralized Identifiers is a distributed identifier (DID) designed to provide a way for FairX Protocol Compliant Nodes to identify and verify participants on its network, as well as provide an 
identity framework for the FairX Protocol "sessions". The role of a FairX DID is to provide a service that supports authentication, personal information verification, the ability to identify FairX Protocol
WASM packages and verify their authenticity.  DIDs and the TBD infrastructure provide the backbone for the FairX Protocol.  

The FairX DID method specification conforms to the requirements specified in
the DID specification [**[1]**](https://www.w3.org/TR/did-core/), currently published by the
W3C Credentials Community Group. For more information about DIDs and DID method specifications,
please see the DID Primer [**[2]**](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md)

# DID Method Name <a name="name"></a>

The namestring that shall identify this DID method is: `fairx`

A DID that uses this method MUST begin with the following prefix: `did:fairx`. Per the DID specification, this string MUST be in lowercase. The remainder of the DID, after the prefix, is specified below.

# Method Specific Identifier <a name="identifier"></a>

The method specific identifier is composed of a required FairX address with an optional `:` separator, followed by a base58btc-encoded string of additional data that may be sub-protocol specific.
```
fairx-did = "did:fairx:" + fairx-specific-idstring
fairx-specific-idstring = fairx-address + ":" + additional-data
fairx-address = multibase(identifier + "@" + fairx_domain)
additional-data = multibase(data)
```

## Example <a name="example1"></a>

Example `fairx` DIDs:

### Simple FairX Address:  example@fairx.io
```
did:fairx:zDXjqxEXcqSNsRfc7PdHDw4
```

### FairX Address with optional data elements attached:  example@fairx.io:/some/path/about/something#forfun
```
did:fairx:zDXjqxEXcqSNsRfc7PdHDw4:zF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh
```
# DID Document <a name="document"></a>

## Example <a name="example2"></a>
```
{
	"@context": "https://w3id.org/did/v1",
	"id": "did:fairx:zDXjqxEXcqSNsRfc7PdHDw4",
	"created": "2022-07-01T12:00:00Z",
	"updated": "2022-07-03T12:00:00Z",
	"publicKey": [{
		"id": "#FairXSigningKey1",
		"type": "Secp256k1VerificationKey2018",
		"publicKeyHash": "3934e3eb037ab1630a195eec0d0eda2570cf6388fea385361598e12b904588f3"
	    },
	    {
		"id": "#VerififcationKey1",
		"type": "Secp256k1VerificationKey2018",
		"publicKeyHash": "3934e3eb037ab1630a195eec0d0eda2570cf6388fea385361598e12b904588f3"
	    }
	],
	"authentication": [{
		"id": "#Service1Key1",
		"type": "Secp256k1VerificationKey2018",
		"publicKeyHex": "034f355bdcb7cc0af728ef3cc...59ab0f0b704075871aa"
	    }
	],
	"service": [{
		"id": "#FairXAuthenticationService",
		"type": "FairX Protocol Authentication Service",
		"serviceEndpoint": "https://authentication.fairx.io/v1.0.0"
	    },
		{
		"id": "#FairXSessionService",
		"type": "FairX Protocol Session Service",
		"serviceEndpoint": "https://session.fairx.io/v1.0.0"
	    }
	]
}
```
FairX uses the ISO 8601 [**[3]**](https://www.iso.org/iso-8601-date-and-time-format.html) basic and extended notations for timestamp.
To make a public key hash from the public key, all we need to do is to apply Multibase algorithm to the key and then take the last 20 bytes of the result.

# JSON-LD Context Definition <a name="ld"></a>

The `fairx` method defines additional JSON-LD terms for the supported FairX key types `SIGNING`, and `SESSION`.

The definition of the `fairx` JSON-LD context is:
```
{
	"@context":
	{
		"FairXSigningKey": "{TBA}",
		"FairXSessionKey": "{TBA}"
	}
}
```
Note: Other type of keys, such as `executor`, `resolver`, and `dataprovider` of a DID Document may be supported in future versions of this specification.

# CRUD Operation Definitions <a name="crud"></a>

## Create (Register) <a name="create"></a>

In order to create a `fairx` DID, FairX-protocol compliant node ([including a Self Soverign Service infrastructure](https://github.com/TBD54566975/ssi-service)) must be provisioned and 
deployed to a domain owned by the node operator.

`fairx` DID creation is done by submitting a DID document to a FairX-compliant DID service:
```
POST https://fairx.io/v1/did/did%3Afairx%3AzDXjqxEXcqSNsRfc7PdHDw4%3AzF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh 
...
```
This will the FairX DID Document must conform to the FairX Protocol DID Specification.  The document must also specify verification parameters before it can be accepted.

## Read (Resolve) <a name="read"></a>

To construct a valid DID document from a `fairx` DID, the following steps are performed (example: `did:fairx:zDXjqxEXcqSNsRfc7PdHDw4`):

1. Split the DID method specific identifier by colon `:` into an array `["zDXjqxEXcqSNsRfc7PdHDw4"]`
2. Multibase Decode each element of the array `["example@fairx.io"]`
3. For the first item in the array:
    1. Further split by `@`, into a FairX Identifier and a FairX Domain. `FairX Identifier: example / FairX Domain: fairx.io`
    1. Start a URL for resolution, and concatenate the FairX Domain:  `https://fairx.io/v1/did`
4. Concatenate the URL-encoded DID Identifier to the URL `https://fairx.io/v1/did/did%3Afairx%3AzDXjqxEXcqSNsRfc7PdHDw4%3AzF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh`
5. Call a HTTP(s) GET request to the URL `GET /v1/did/did%3Afairx%3AzDXjqxEXcqSNsRfc7PdHDw4%3AzF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh HTTP/...`

Note: Multiple additional FairX service endpoints and other elements of a DID Document may be supported in future versions of this specification.

## Update <a name="update"></a>

The DID Document may be updated by invoking the FairX Domain Endpoint, using Authentication Credentials specified in your FairX DID Document:
```
PUT /v1/did/did%3Afairx%3AzDXjqxEXcqSNsRfc7PdHDw4%3AzF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh HTTP/...`
```
## Delete (Revoke) <a name="delete"></a>

The DID Document may be deleting by invoking the FairX Domain Endpoint, using Authentication Credentials specified in your FairX DID Document:
```
DELETE /v1/did/did%3Afairx%3AzDXjqxEXcqSNsRfc7PdHDw4%3AzF6ZVrPmpyDt8s4paK2tJaQhivnLTjsr9fS7KGiN8hC8Eh HTTP/...`
```

# Security Considerations <a name="security"></a>

When an entity creates and registers its own `fairx` DID in the FairX domain node:
- The FairX DID Document **must** include at least 1 FairX-compatible [**[4]**](https://www.w3.org/TR/did-core/#verification-methods) Verification Method and associated [**[5]**](https://www.w3.org/TR/did-core/#authentication) Authentication Verification Relationship to prove ownership of the document in order to make any modifications.  [**[6]**](https://www.w3.org/TR/did-core/#capability-delegation) Delegated authorities are acceptable. 
- Anyone can operate a FairX Protocol Node.  The operator of that node is responsible for data management, and the user of that node accepts the node's capabilities and SLAs, if any.  The FairX Protocol makes no warranties for the use of a distributed ledger for "permanent" recording of data, though nothing stop a developer from doing so.

# Privacy Considerations <a name="privacy"></a>

- Its up to document creators to be mindful of the data they put into a DID, as the FairX specification does not require DID document privacy for READ (Resolve) operations.

# References <a name="references"></a>
----------

**[1]** https://www.w3.org/TR/did-core/

**[2]** https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md

**[3]** https://www.iso.org/iso-8601-date-and-time-format.html

**[4]** https://www.w3.org/TR/did-core/#verification-methods

**[5]** https://www.w3.org/TR/did-core/#authentication

**[6]** https://www.w3.org/TR/did-core/#capability-delegation
 