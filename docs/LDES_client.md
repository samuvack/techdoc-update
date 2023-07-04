---
sort: 5
---

# LDES CLIENT

<p align="center"><img src="/VSDS-Tech-Docs/images/LDES%20client.png" width="60%" text-align="center"></p>

The [LDES CLIENT](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions) is designed for replication and synchronisation, meaning the client can retrieve members of an LDES but also checks regularly if new members are added and fetch them, allowing data consumers to stay up to date with the dataset.

To understand the functioning of an LDES client, it is important to understand how LDESes are published on the Web. The [Linked Data Fragments](https://linkeddatafragments.org/specification/linked-data-fragments/) principle is utilised for publishing an LDES, meaning that the data is published in one or more fragments and meaningful semantic links are created between these fragments. This approach facilitates clients to follow these links and discover additional data. However, the critical aspect for the LDES client is the notion of mutable and immutable fragments. When publishing an LDES stream, a common configuration is to have a maximum number of members per fragment. Once a fragment surpasses this limit, it is regarded as immutable, and a **'Cache-control: immutable'** cache header is added to the fragment to signify this. This information is crucial for the LDES client since it only needs to retrieve an immutable fragment once, while mutable fragments must be regularly polled to identify new members.

## Replication

To initiate the replication of an LDES, data consumers must configure the LDES client with an LDES endpoint. If multiple views are available for the LDES, the LDES client will begin the replication process utilising the first view it receives. However, suppose a data consumer has a specific preference for a particular view to initiate the replication. In that case, it is also possible to configure the view URI in the LDES client accordingly.

<p align="center"><img src="/VSDS-Tech-Docs/images/replication.png" width="60%" text-align="center"></p>

When the client visits a fragment, it parses the content to RDF and discovers LDES members by looking for triples with the **tree:member**. Moreover, the client searches for triples with a **tree:relation** predicate, signifying links to other fragments, and adds them to its queue of fragments to be fetched if they still need to be retrieved. The client inspects the response headers for each fragment and looks for a potential *'Cache-control: immutable'* attribute, indicating that the fragment is *immutable* and does not need to be polled again.

## Synchronisation

In addition to replication, the LDES client keeps track of all *mutable* fragments and periodically polls them to check if new LDES members were added. To further optimise the synchronisation process, the LDES client reads the *'Cache-control: max-age'* value from the response headers, which specifies the time period for which the LDES fragment remains valid. This allows the LDES client to schedule periodic polling more efficiently.

<p align="center"><img src="/VSDS-Tech-Docs/images/synchronisation.png" width="60%" text-align="center"></p>

By utilising the response headers provided by the LDES server, the LDES client can effectively manage the synchronisation of the LDES stream, while minimising the amount of processing required. This makes the LDES client an efficient and reliable tool for processing and managing Linked Data Event Streams.

## Resuming

An essential functionality of the LDES client is *resuming*, enabling the client to halt and resume from where it last stopped. To achieve this functionality, the client utilises an SQLite database to persist the immutable and mutable fragment IDs, guaranteeing that an immutable fragment is only retrieved once. The member IDs are also saved in the database for mutable fragments, ensuring that an LDES member is processed only once.

<p align="center"><img src="/VSDS-Tech-Docs/images/State.png" width="60%" text-align="center"></p>

## Linked Data Interactions

The LDES client component is written in Java and available as an [SDK](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-core/ldes-client) in the Linked Data Interactions repository. More information about Linked Data Interactions can be found [here](/docs/LINKED_DATA_INTERACTIONS.md).
