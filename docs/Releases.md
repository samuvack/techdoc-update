---
sort: 9
---

# Release management


## LDES Server [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=Informatievlaanderen_VSDS-LDESServer4J&metric=alert_status&?style=social)](https://sonarcloud.io/summary/new_code?id=Informatievlaanderen_VSDS-LDESServer4J)


<p align="left"><img src="https://img.shields.io/github/release-date/Informatievlaanderen/VSDS-LDESServer4J?style=social" text-align="left"></p>

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-LDESServer4J) for all the releases of the LDES server.


## LDES Client

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-core/ldes-client) for all the LDI releases of the LDES client.

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-nifi/ldi-nifi-processors/ldes-client-processor) for all the Apache NiFi releases of the LDES client.


## Linked Data Interactions [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=Informatievlaanderen_VSDS-Linked-Data-Interactions&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=Informatievlaanderen_VSDS-Linked-Data-Interactions)

<p align="left"><img src="https://img.shields.io/github/release-date/Informatievlaanderen/VSDS-Linked-Data-Interactions?style=social" text-align="left"></p>

The Linked Data Interactions Repo (LDI) is a bundle of basic SDKs used to receive, generate, transform and output Linked Data. This project is set up in the context of the VSDS Project to ease adopting LDES on data consumer and producer side.

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions) for all the releases of the Linked Data Interactions.

## LDI API
The LDI API provides a bundle of generic interfaces and classes to be used in the LDI SDKs

For further information, please refer to the JavaDoc.

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-api) for the releases of the LDI API.

## LDI Core
The LDI Core module contains the SDKs maintained by the VSDS team in order to accommodate the onboarding of LDES onboarders.

Each SDK can be wrapped in a desired implementation framework (LDI-orchestrator, NiFi, ...) to be used.

More documentation on the individual SDKs can be found [here](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/blob/main/ldi-core/README.md)

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-core) for the releases of the LDI Core.

## LDI implemented in Apache NiFi
The VSDS team currently supports and maintains two implementation frameworks in which the SDKs can be run. Apache NiFi is one of them.

Apache NiFi is a powerful data integration tool that enables organisations to manage and process their data flows in real-time.

For further details on how to use our components in NiFi, please refer to the in-NiFi documentation.

-[Apache NiFi](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-nifi)

## LDI Orchestrator
As NiFi can be quite extensive for setting up a basic Linked Data transformation, we provide an alternative lightweight Spring Boot based framework.

For further details on how to use our components in the LDI Orchestrator, please refer to the [LDI Orchestrator documentation](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/blob/main/ldi-orchestrator/README.md)

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-Linked-Data-Interactions/tree/main/ldi-orchestrator) for the releases of the LDI Orchestrator.


## LDES dockers

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-LDESDockers) for the repository with working docker environment for the GIPOD case.

## LDES End to End testing (E2Etesting)

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing) for the repository with [End-to-end tests](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/blob/main/e2e-test/README.md) and tooling needed for testing LDES components build as part of VSDS.

## LDES workbench

You can find the LDES workbench in these **archived** repositories:
-[Command Line Interface](https://github.com/Informatievlaanderen/VSDS-LDESWorkbench-Services)
-[Apache NiFi](https://github.com/Informatievlaanderen/VSDS-LDESWorkbench-NiFi)

## LDES processors

Go to [this Github repository](https://github.com/Informatievlaanderen/VSDS-LDESProcessors) for the repository with working LDES processors for Apache NiFi.This repository contains a collection of Apache Nifi processors that help working with LDES streams. These processors are considered experimental. Once they reach sufficient maturity, they will be moved to the [LDES workbench](https://github.com/Informatievlaanderen/VSDS-LDESWorkbench-NiFi).

## LDES connectors

Here you can find the [**archived** LDES connector repository](https://github.com/Informatievlaanderen/VSDS-LDESConnectors)


## Notification of new releases
```tip

To get informed when a new version of a building block is released, go to 'watch'

![](/VSDS-Tech-Docs/images/releases.png)

On the [notifications](https://github.com/notifications) page, you can see your personal notification subscribtions  
```