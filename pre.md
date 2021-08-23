# The System of Beliefs
This electronic document represents the first belief incorporated into the System of Beliefs (hereinafter referred to as the "System") on [INSERT TIMESTAMP]. 

The System of Beliefs is an abstract network of electronic documents expressing the beliefs held by entities such as people and organizations. 

## How Does a Belief Become Part of the System
Beliefs cannot be part of the System unless they are (a) [incorporated](#Incorporation) into the System, or (b) are [adopted](#Adoption) by the entities that hold that belief, [shared](Sharing) with one or more entities, and [accepted](#Acceptance) by those entities. 

There are two general types of documents that need to be submitted to the System to make a belief a part of it:
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
- the identifier that the entity will use for their next action document,
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
* Like this document (in `Version 0.29-gfm` of the GitHub Flavored Markdown Spec), for styling, the belief can be represented in any human readable format (e.g. plain-text, html, etc.). However, the need for a machine readable and reason-able System may require standards on belief document formats.

### Adoption Document
The entity needs to also create another electronic document claiming that they adopt the belief. This is an action document, similar to acceptance, attestation, etc. 
The adoption document needs to contain:
- a type specifier stating it's a adoption document,
- an identifier for the adoption document, 
- the identifier of the believer, 
- the id of the belief document, 
- the timestamp that the belief is adopted, 
- the identifier for the previous action document by the believer,
- the identifier that the entity will use for their next action document,
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


### Sharing 
That entity can then share these two electronic documents with anyone who is willing to accept it. The belief document need not always be shared - for example, if the  

### Acceptance Document

### Attestation Document

#### Chain of Beliefs
The belief document should also contain a link 

## Trust

## Provenance
