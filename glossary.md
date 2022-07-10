# FairX Protocol Glossary

FairX is an experimental suite of open source services that run alongside [TBD's Self-Sovereign SDK and Services](https://github.com/TBD54566975). 

FairX Decentralized Identifiers is a distributed identifier (DID) designed to provide a way for FairX Protocol Compliant Nodes to identify and verify participants on its network, as well as provide an 
identity framework for the FairX Protocol "sessions". The role of a FairX DID is to provide a service that supports authentication, personal information verification, the ability to identify FairX Protocol
WASM packages and verify their authenticity.  DIDs and the TBD infrastructure provide the backbone for the FairX Protocol.  

The FairX Protocol Glossary is a central location to understand terms users in the various FairX Protocol and Sub-Protocol specifications.  All other specifications should link back to this Glossary to help the reader navigate the terminology.

# Table of Contents
- [FairX Protocol Glossary](#fairx-protocol-glossary)
- [Table of Contents](#table-of-contents)
- [Concepts <a name="fairx-protocol-glossary-concepts"></a>](#concepts-)
  - [FairX Domain <a name="fairx-protocol-glossary-fairx-domain"></a>](#fairx-domain-)
  - [FairX Node <a name="fairx-protocol-glossary-fairx-node"></a>](#fairx-node-)
  - [FairX Participant <a name="fairx-protocol-glossary-fairx-participant"></a>](#fairx-participant-)
  - [FairX Service <a name="fairx-protocol-glossary-fairx-service"></a>](#fairx-service-)
  - [FairX Session <a name="fairx-protocol-glossary-fairx-session"></a>](#fairx-session-)
- [FairX Services <a name="fairx-protocol-glossary-fairx-services"></a>](#fairx-services-)
  - [FairX Authentication Service <a name="fairx-protocol-glossary-fairx-authentication-service"></a>](#fairx-authentication-service-)
  - [FairX Decentralized Web Node (DWN) <a name="fairx-protocol-glossary-fairx-dwn"></a>](#fairx-decentralized-web-node-dwn-)
- [Registration & Authentication <a name="fairx-protocol-glossary-regauth"></a>](#registration--authentication-)
  - [Open Registration <a name="fairx-protocol-glossary-regauth-open"></a>](#open-registration-)
  - [Closed Registration <a name="fairx-protocol-glossary-regauth-closed"></a>](#closed-registration-)

# Concepts <a name="fairx-protocol-glossary-concepts"></a>

## FairX Domain <a name="fairx-protocol-glossary-fairx-domain"></a>

A FairX Domain is a common name service configuration (such as [DNS](https://datatracker.ietf.org/doc/html/rfc1034) (default), but could be [ENS](https://eips.ethereum.org/EIPS/eip-137) or similar).

## FairX Node <a name="fairx-protocol-glossary-fairx-node"></a>

A FairX Node is an electronic service which responds to messages sent to it, or retrieved from it, according to the W3C's [Decentralized Web Node Specification](https://identity.foundation/decentralized-web-node/spec/), alongside with FairX's extensions by way of its [FairX Decentralized Web Node Messages](https://github.com/fairxio/protocol/tree/main/did/messages).

## FairX Participant <a name="fairx-protocol-glossary-fairx-participant"></a>

A FairX Participant is a [DID Subject](https://www.w3.org/TR/did-core/#did-subject) that is participating in a FairX Session with 1 or more other Participants.

## FairX Service <a name="fairx-protocol-glossary-fairx-service"></a>

A FairX Service is an endpoint on a FairX Node, or an entire Node, which serves a specific purpose for the FairX Protocol. 

## FairX Session <a name="fairx-protocol-glossary-fairx-session"></a>

A FairX Session defines a list of Participants (expressed by their DID URLs), a list of Session Executables and their IPFS URLs, metadata, and other configuration.  A Session object must be signed by each of the Participants in order to be considered a valid Active Session.

Sessions may have the following states, depending on its stage in the messaging flow:

- **Proposed** (Sessions have been posted to at least 1 participant node, but not enough signatures have been obtained)
- **Active** (Sessions have been posted to all participant nodes, and all signatures have been obtained)


# FairX Services <a name="fairx-protocol-glossary-fairx-services"></a>

## FairX Authentication Service <a name="fairx-protocol-glossary-fairx-authentication-service"></a>

The `type` must be `FairXProtocolAuthenticationService`, and the `serviceEndpoint` **must** conform to the [FairX Protocol - Authentication Specification](https://github.com/fairxio/protocol/tree/main/authentication/fairx-protocol-authentication.png).

```json
{
    "id": "#FairXAuthenticationService",
    "type": "FairXProtocolAuthenticationService",
    "serviceEndpoint": {
      "nodes": ["https://authentication.fairx.io/v1.0.0"]
    }
}
```

## FairX Decentralized Web Node (DWN) <a name="fairx-protocol-glossary-fairx-dwn"></a>

The `type` must be `DecentralizedWebNode`, and the `serviceEndpoint` **must** conform to the W3C's [Decentralized Web Node Specification](https://identity.foundation/decentralized-web-node/spec/), and must support all of the [FairX Decentralized Web Node Messages](https://github.com/fairxio/protocol/tree/main/did/messages). Be sure to follow the [DWN Service Endpoint](https://identity.foundation/decentralized-web-node/spec/#service-endpoints) section for details.

```json
{
    "id": "#DecentralizedWebNode",
    "type": "DecentralizedWebNode", 
    "serviceEndpoint": {
      "nodes": ["https://dwn.fairx.io/v1.0.0"]
    }
}
```

# Registration & Authentication <a name="fairx-protocol-glossary-regauth"></a>

## Open Registration <a name="fairx-protocol-glossary-regauth-open"></a>

A method of registration where a FairX Node may allow registration of a DID Subject openly without intervention.  Note, a DID Subject may be Blacklisted.

## Closed Registration <a name="fairx-protocol-glossary-regauth-closed"></a>

A method of registration where a FairX Node only allows authentication to previously registered DID Subjects per private means.  For example, a FairX Protocol Subnetwork can be created where participating nodes are on each other's Whitelists.
