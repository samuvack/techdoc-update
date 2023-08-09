---
sort: 10
---

# Use case LDES server

```tip
Having trouble implementing these examples? Please post your issue on the [VSDS Tech docs repo](https://github.com/Informatievlaanderen/VSDS-Tech-Docs/issues).

```

<p align="center"><img src="/VSDS-Tech-Docs/images/onboarding.png"  width="50%" text-align="center"></p>

Apache Kafka, Fiware-Orien Context Broker, and MQTT can be used as a Publisher to the VSDS LDES Ecosystem. The following examples will explain the use cases.   

##  Kafka to LDES server



Apache Kafka can be used as a data provider for ingesting data topics into the LDES ecosystem. The diagram below illustrates how the VSDS NIFI solution subscribes to a Kafka stream, updates the dataset's attributes, converts it into an LDES-formatted stream, and uses HTTP protocols to publish it to the LDES Server. This process enables fragmentation or pagination of the data.


<p align="center"><img src="/VSDS-Tech-Docs/images/Kafka_onboarding.png"  width="60%" text-align="center"></p>

This [GitHub repository](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/tree/d45ecbeee157255ff577728c2f198fa768a24d5a/e2e-test/use-cases/grar/1.addresses-substring-fragmentation) demonstrates the configuration of transferring subscribed GRAR (Building units, addresses & parcels) Kafka data stream to the published substring fragmented LDES Stream using LDES Server. As we have no control over the GRAR system, the demo uses a [JSON Data Generator](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/blob/d45ecbeee157255ff577728c2f198fa768a24d5a/json-data-generator/README.md) which produces a continuous stream of addresses as an alternative to the GRAR system. Also, the Apache NIFI has standard Kafka Reader processors for subscribing to Kafka stream, please modify the [nifi-workflow.json](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/blob/d45ecbeee157255ff577728c2f198fa768a24d5a/e2e-test/use-cases/grar/1.addresses-substring-fragmentation/nifi-workflow.json) accordingly based on your environment. An example setup with Kafka can be as follow ([GRAR.json](https://github.com/Informatievlaanderen/VSDS-Tech-Docs/blob/main/files/GRAR.json)), please modify the credentials for the Kafka topic accordingly:

To try out the demo, you need to make sure the required ports for LDES Server and NIFI are free to be used. For the details, please refer to [docker-compose.yml](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/blob/d45ecbeee157255ff577728c2f198fa768a24d5a/e2e-test/use-cases/grar/1.addresses-substring-fragmentation/docker-compose.yml).

The steps are composed of the following steps:

1\. Docker run start all required docker images.

2\. Upload a pre-defined NiFi workflow.

3\. Start the NiFi workflow.

4\. Start the address ingestion. (Modify according to your Kafka setup)

Please follow [README.md](https://github.com/Informatievlaanderen/VSDS-LDES-E2E-testing/tree/d45ecbeee157255ff577728c2f198fa768a24d5a/e2e-test/use-cases/grar/1.addresses-substring-fragmentation) for step-by-step guide.

* * * * *




##  MQTT to LDES server


<p align="center"><img src="/VSDS-Tech-Docs/images/MQTT.png"  width="60%" text-align="center"></p>


## Fiware to LDES server

The FIWARE-Orion Context Broker (OCB) can be integrated as a data provider with the VSDS LDES (Linked Data Event Streams) Server. The OCB is an open-source software component developed by FIWARE that can manage real-time context information by receiving updates from IoT devices, sensors, and other sources and storing this information in a centralized location.

One example of this integration is demonstrated in the diagram below, which illustrates the use case of onboarding the Internet of Water (VMM) data. The details of this use case locate at [Orien Context Broker - IOW.](https://github.com/Informatievlaanderen/VSDS-Onboarding-VMM/tree/main/iow) 


<p align="center"><img src="/VSDS-Tech-Docs/images/orion_onboarding_iow.png"  width="70%" text-align="center"></p>

In this case, the OCB is integrated into the LDES ecosystem to publish context updates to an LDES stream. The VSDS NIFI solution is used to translate the context data into LDES events and publish them to the LDES stream via an update attributes processor, an OSLO converter processor, and an LdesConverter process NIFI pipeline.

Once the context updates are published to the LDES Sever in LDES formatted stream, they can be processed and stored in the LDES Server as linked data. This makes the context information available for further analysis and uses in other systems. An example NIFI setup with Fiware-Orien Context Broker can be as follow, which locates at [workflow.json](https://github.com/Informatievlaanderen/VSDS-Onboarding-VMM/blob/main/iow/workflow.json).

Please follow [README.md](https://github.com/Informatievlaanderen/VSDS-Onboarding-VMM/blob/main/iow/README.md) for step-by-step guide.

