# The System of Beliefs
The System of Beliefs is a distributed organization of electronic documents expressing beliefs held by entities such as people and organizations.

This electronic document represents the first belief incorporated into the System of Beliefs (hereinafter referred to as the "System") on [INSERT TIMESTAMP]. 

## How Does a Belief Become Part of the System?
Before submitting a belief, an entity should first [introduce](#Introduction_Document) themselves. Beliefs cannot be part of the System unless they are (a) [incorporated](#Incorporation_Document) into the System, or (b) are [adopted](#Adoption_Document) by the entities that hold that belief, [shared](Sharing) with one or more entities, and [accepted](#Acceptance_Document) by those entities. Acceptance here refers to checks that the receiver might do to confirm that the belief is not unreasonable. It does not mean that the receiver also subscribes to those beliefs. To make beliefs usable between entities, verification of the statements in the belief might be needed. The receiver may [attest](#Attestation_Document) this belief to be true if it can independently verify the truth of the belief. 

We can categorize the documents that need to be submitted to the System to make a belief a part of it into two general categories:
  1. **Belief Documents** - An electronic document stating the belief: 
      * a [belief document](#Belief_Document), 
      * this [Incorporation Document](#Incorporation_Document).
  2. **Action Documents** - An electronic document ddescribing the following actions that entities can take on these beliefs.
      * [Introduction Document](#Introduction_Document)
      * [Adoption Document](#Adoption_Document)
      * [Acceptance Document](#Acceptance_Document)
      * [Attestation Document](#Attestation_Document)

### Incorporation Document
This first belief is the only belief that can be incorporated into the System and by doing so is a part of it. It doesn't need to be adopted, shared with or accepted by any entity to become a part of it. 

### Introduction Document
People and organizations are the only entities allowed to submit a belief to the System. Any electronic software provisioned by an entity may also submit beliefs to the System on behalf of the entity. Organizations are run by people. And so, for organizations to submit beliefs to a System, they must have delegate person(s) who submit beliefs. 

Both people and organizations can generate a public-private key to manage their identity and submit beliefs to the System. Public keys shall be part of an asymmetric key generated using ECDSA, where the private key is known to the entity. This public key also serves as the unique identifier for the entity, while the private key is used to sign the documents when needed. 

Any entity must create and share an introduction document, that introduces themselves in the System before creating any other type of document (belief or action). 

The introduction document needs to contain:
- a type specifier stating it's a introduction document,
- the entity type stating it's a person/organization,
- an identifier for the introduction document, 
- the public key of the entity, 
- the timestamp that the belief is adopted, 
- the identifier that the entity will use for their next action document, which should not be an id that they have previously used,
- a hash of the above information, 
- and a signature with their private key on that hash 

#### Specifications
* The introduction electronic document needs to be `UTF-8` encoded. 
* This is a machine readable document containing key-value pairs on each line, separated by a colon. The keys usable for the fields needed in the introduction document are:
  * `type: introduction` - Stating that this is a adoption document.
  * `entity: person` OR `entity: organization` - Stating if it's a person/organization,
  * `id: <unique_id>` - A UUID v4 unique identifier for this action document.
  * `public_key: <the public key of the entity>` - The public key of the entity that is also their unique id.
  * `created_at: <the timestamp of introduction>` - The timestamp of the date and time of adoption ISO-8601 UTC format with Zero offset.
  * `next: <unique_id>` - A UUID v4 unique identifier for the next action document by this entity.

### Belief Document
Any entity that has a belief they'd like to assert and convey to others can create an electronic document detailing the belief. Each belief document can be uniquely identified by exactly one identifier - its hash generated using a hash function. 

#### Specifications
* The belief electronic document needs to be `UTF-8` encoded. 
* The belief identifier is the 256-bit `SHA3` hash of the document represented as a hexdigest with lowercase alphabets.
* Like this document (in `Version 0.29-gfm` of the GitHub Flavored Markdown Spec), for styling, the belief can be represented in any human readable format (e.g. plain-text, html, etc.) or use any other text format. However, the need for a machine readable and reason-able System may require standards on belief document formats.

### Adoption Document
The entity needs to also create another electronic document claiming that they adopt the belief. This is an action document, similar to acceptance, attestation, etc. Once created, this document can then be [shared](#Sharing) with other entities in the System.

The adoption document needs to contain:
- a type specifier stating it's a adoption document,
- an identifier for the adoption document, 
- the identifier of the believer, 
- the id of the belief document, 
- the timestamp that the belief is adopted, 
- the identifier for the previous action document by the believer,
- the identifier that the entity will use for their next action document, which should not be an id that they have previously used,
- a hash of the above information, 
- and a signature with their private key on that hash 

#### Specifications
* The adoption electronic document needs to be `UTF-8` encoded. 
* This is a machine readable document containing key-value pairs on each line, separated by a colon. The keys usable for the fields needed in the adoption document are:
  * `type: adoption` - Stating that this is a adoption document.
  * `id: <unique_id>` - A UUID v4 unique identifier for this action document.
  * `believer: <the public key of the believer>` - The public key of the believer.
  * `belief: <the id of the belief document>` - As explained earlier, this is the hash of the belief document.
  * `created_at: <the timestamp of adoption>` - The timestamp of the date and time of adoption ISO-8601 UTC format with Zero offset.
  * `previous: <unique_id>` - A UUID v4 unique identifier for the previous action document by this entity.
  * `next: <unique_id>` - A UUID v4 unique identifier for the next action document by this entity.

### Acceptance Document
The receiver of the belief document and the adoption document shared by an entity, may choose to accept or reject it. They may perform checks to validate the content of the belief document or the action document. For example, they can validate the hashes, signatures, the links, etc. 

To accept a belief adopted, the receiver must also establish soundness of this belief combined with all the beliefs adopted by that person previously. For example, one cannot adopt the belief that the earth is flat, and also adopt the belief that the earth is round (without abandoning the belief). 

It does not mean that the receiver also subscribes to those beliefs. The receiver may accept that it reasonable to the sender to have this new belef without having to believe in it themselves, as long is it is consistent with other beliefs held by the person. 

To establish the soundness of the belief, the receiver may ask the sender all their other beliefs and action documents leading to this belief. The sender must provide these if the receiver is to accept. The receiver may have to use considerable computing or human resources to validate and verify this belief, and so may ask for some compensation. 

Once the receiver determines that this adoption document can be accepted, they can create an acceptance document and share it with the sender. The sender must store this and furnish it in case a future belief adoption needs to be accepted or attested.

The acceptance document needs to contain:
- a type specifier stating it's a acceptance document,
- an identifier for the acceptance document, 
- the identifier of the accepter, 
- the id of the adoption document that is accepted, 
- the timestamp that the adoption document is accepted, 
- the identifier for the previous action document by the accepter,
- the identifier that the entity will use for their next action document, which should not be an id that they have previously used,
- a hash of the above information, 
- and a signature with their private key on that hash 

#### Specifications
* The acceptance electronic document needs to be `UTF-8` encoded. 
* This is a machine readable document containing key-value pairs on each line, separated by a colon. The keys usable for the fields needed in the acceptance document are:
  * `type: acceptance` - Stating that this is a acceptance document.
  * `id: <unique_id>` - A UUID v4 unique identifier for this action document.
  * `accepter: <the public key of the accepter>` - The public key of the accepter.
  * `adoption: <the id of the adoption document>` - As explained earlier, this is the hash of the adoption document.
  * `created_at: <the timestamp of adoption>` - The timestamp of the date and time of acceptance ISO-8601 UTC format with Zero offset.
  * `previous: <unique_id>` - A UUID v4 unique identifier for the previous action document by this entity.
  * `next: <unique_id>` - A UUID v4 unique identifier for the next action document by this entity.

### Attestation
Entities may also provide attestation of certain belief or action documents. A requestor who wants another entity to attest the content of their belief of action document may request them to do so if they are willing to provide the service. Attestation would mean that the belief and actions are valid and sound, as in acceptance documents, and also verified independently by the attestor to be true.

In this case, the attestation would mean that the receiver also believes those documents to be true. And so, an attestation involves creation of a belief document that lists out the requestor's documents believes to be true, and an attestation document attesting to that belief. The attester must share their attestation document with the requestor. The requestor must store this and furnish it in case a future belief adoption needs to refer to it.

The attestation document needs to contain:
- a type specifier stating it's a attestation document,
- an identifier for the attestation document, 
- the ids of the belief and action documents attested, 
- the timestamp of the attestation, 
- the identifier for the previous action document by the attester,
- the identifier that the entity will use for their next action document, which should not be an id that they have previously used,
- a hash of the above information, 
- and a signature with their private key on that hash 

#### Specifications
* The attestation electronic document needs to be `UTF-8` encoded. 
* This is a machine readable document containing key-value pairs on each line, separated by a colon. The keys usable for the fields needed in the attestation document are:
  * `type: attestation` - Stating that this is a attestation document.
  * `id: <unique_id>` - A UUID v4 unique identifier for this action document.
  * `belief: <the id of a belief document part of the attestation>` - One or more belief documents that are attested, each on their own newline with the key.
  * `introduction: <the id of an introduction document part of the attestation>` - One or more introduction documents that are attested, each on their own newline.
  * `adoption: <the id of an adoption document part of the attestation>` - One or more adoption documents that are attested, each on their own newline.
  * `acceptance: <the id of an acceptance document part of the attestation>` - One or more acceptance documents that are attested, each on their own newline.
  * `attestation: <the id of an attestation document part of the attestation>` - One or more attestation documents that are attested, each on their own newline.
  * `created_at: <the timestamp of adoption>` - The timestamp of the date and time of adoption ISO-8601 UTC format with Zero offset.
  * `previous: <unique_id>` - A UUID v4 unique identifier for the previous action document by this entity.
  * `next: <unique_id>` - A UUID v4 unique identifier for the next action document by this entity.

## Sharing 
That entity can then share these two electronic documents with anyone who is willing to accept it. The belief document need not always be shared - for example, if the  


## Chain of Actions and Network of Beliefs
A chain of documents is formed for each user starting from their introduction document to the most recent action that they perform. Tracing the previous action id helps us follow all the evolved beliefs of the entity as they adopt it or track the beliefs they have accepted or attested. Constraining the next identifier allows us to prevent a user from having multiple simultaneous actions - preventing a Directed Acyclic Graph for that user. 

When we consider documents from across different entities, we see a Directed Acyclic Graph of beliefs and actions emerging which allows for interoperability.

## Trust

## Bad Actors

## Provenance

## Encryption

