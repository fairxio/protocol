# Establish Session Message

# Table of Contents

# Overview

The `EstablishSession` message defines all of the properties required in a message to establish a [FairX Session](https://github.com/fairxio/protocol/tree/main/glossary.md#fairx-protocol-glossary-fairx-session).  An Active FairX Session is required in order to perform Executions or other operations between the participants.  

# Protocol Description

The `EstablishSession` message is embedded within a `CollectionsWrite` [DecentralizedWebNode Interface Message](https://identity.foundation/decentralized-web-node/spec/#write) with a specific [Session](https://github.com/fairxio/protocol/blob/main/did/messages/session-schema.json) schema.  