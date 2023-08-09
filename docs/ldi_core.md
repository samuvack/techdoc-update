---
sort: 6
---

# Linked Data Interactions Building Blocks


## Building blocks

As the LDI strives to be an easily reusable project, each of our building blocks are framework independent and is being maintained as part in our LDI Core.

Each of the LDI Core Building Blocks falls under one of four categories:
* [LDI Input](ldi_core.html#linked-data-interactions-inputs): A component that will receive data (not necessarily LD) to then feed the LDI pipeline.
* [LDI Adapter](ldi-adapters): To be used in conjunction with the LDI Input, the LDI Adapter will transform the provided content into and internal Linked Data model and sends it down the pipeline.
* [LDI Transformer](ldi-transformers): A component that takes in a Linked Data model, transforms/modifies it and then puts it back on the pipeline.
* [LDI Output](ldi-outputs): A component that will take in Linked Data and will export it to external sources.

````mermaid
stateDiagram-v2
    direction LR
    [*] --> LDI_Input
    LDI_Input --> LDI_Transformer : LD
    LDI_Transformer --> LDI_Output : LD
    LDI_Output --> [*]

    state LDI_Input {
        direction LR
        [*] --> LDI_Adapter : Non LD

        state LDI_Adapter {
            direction LR
            [*] --> adapt
            adapt --> [*]
        }

        LDI_Adapter --> [*] : LD
    }
    
    state LDI_Transformer {
        direction LR
        [*] --> transform
        transform --> [*]
    }
    state LDI_Output {
        direction LR
        [*] --> [*]
    }
````

## Linked Data Interactions Inputs

The LDI Input is a component that will receive data (not necessarily LD) to then feed the LDI pipeline.


### Archive File In


The Archive File In is used to read the models from a file archive created by the [Archive File Out component](../ldi-outputs/file-archiving.md).

This component traverses all directories in the archive in lexical order and reads the members in lexical order as well.

Example expected structure:
- archive
  - 2022
    - 01
      - 01
        - member-1.nq
        - member-2.nq
        - ...
      - 02
        - member-122.nq
        - ...

#### Config

| Property         | Description                       | Required | Default                     | Example          | Supported values                |
|:-----------------|:----------------------------------|:---------|:----------------------------|:-----------------|:--------------------------------|
| archive-root-dir | The root directory of the archive | Yes      | N/A                         | /parcels/archive | Linux (+ Mac) and Windows paths |
| source-format    | The source format of the files    | No       | Deduced from file extension | text/turtle      | Any Jena supported format       |

#### Example
A complete demo of the archiving functionality with both LDIO and NiFi can be found in the [E2E repo](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/tree/main/tests/033.archiving)

{: .note }
The traversal order is **lexical**, this means that 1, 2, 3, ..., 9 should have leading zeroes. 
03 will be read before 10 but 3 will be read after 10.

{: .note }
Not all file extensions can be deduced automatically. Extensions like `.ttl` and `.nq` work fine and don't need a source-format specified.
When using LD+JSON, you will need to specify the source-format.


### Ldes Client

The LDES Client contains the functionality to replicate and synchornise an LDES, and to persist its state for that process. More information on the functionalites can be found [here][VSDS Tech Docs].

This is achieved by configuring the processor with an initial fragment URL. When the processor is triggered, the fragment will be processed, and all relations will be added to the (non-persisted) queue.

As long as the processor runs, a queue that accepts new fragments to process is maintained. The processor also keeps track of the mutable and immutable fragments already processed.

It will be ignored when an attempt is made to queue a known immutable fragment. Fragments in the mutable fragment store will be queued when they're expired. Should a fragment be processed from a stream that does not set the max-age in the Cache-control header, a default expiration interval will be used to set an expiration date on the fragment.

Processed members of mutable fragments are also kept in state. They are ignored if presented more than once.

[VSDS Tech Docs]: https://informatievlaanderen.github.io/VSDS-Tech-Docs/docs/LDES_client.html