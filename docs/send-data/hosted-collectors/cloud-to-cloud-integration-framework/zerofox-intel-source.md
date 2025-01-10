---
id: zerofox-intel-source
title: ZeroFox Threat Intel Source
sidebar_label: ZeroFox Threat Intel
tags:
  - cloud-to-cloud
  - zerofox-threat-intel
description: This integration collects threat indicators using the ZeroFox API and sends them to Sumo Logic for analysis.
---
import CodeBlock from '@theme/CodeBlock';
import ExampleJSON from '/files/c2c/zerofox/example.json';
import MyComponentSource from '!!raw-loader!/files/c2c/zerofox/example.json';
import TerraformExample from '!!raw-loader!/files/c2c/zerofox/example.tf';
import useBaseUrl from '@docusaurus/useBaseUrl';

<head>
  <meta name="robots" content="noindex" />
</head>

<p><a href="/docs/beta"><span className="beta">Beta</span></a></p>

<img src={useBaseUrl('img/integrations/security-threat-detection/zerofox-logo.png')} alt="ZeroFox threat intel logo" width="50" />

ZeroFox is a cybersecurity firm specializing in providing cyber threat intelligence services.

The ZeroFox source collects threat indicators using the [ZeroFox CTI API](https://api.zerofox.com/cti/docs/) and sends them to Sumo Logic as normalized threat indicators for analysis.

## Data collected

| Polling Interval | API Endpoint              |
|:-----------------|:------------------|
| 1 hour           | `/cti/botnet`     |
| 1 hour           | `/cti/c2-domains` |
| 1 hour           | `/cti/disruption` |
| 1 hour           | `/cti/malware`    |
| 1 hour           | `/cti/phishing`   |
| 1 hour           | `/cti/ransomware` |

## Setup

### Vendor configuration

The ZeroFox Threat Intel source requires you to provide your ZeroFox account username and password.

### Source configuration

When you create an ZeroFox Threat Intel source, you add it to a Hosted Collector. Before creating the source, identify the Hosted Collector you want to use or create a new Hosted Collector. For instructions, see [Configure a Hosted Collector and Source](/docs/send-data/hosted-collectors/configure-hosted-collector).

To configure an ZeroFox Threat Intel source:

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the main Sumo Logic menu, select **Manage Data > Collection > Collection**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the Sumo Logic top menu select **Configuration**, and then under **Data Collection** select **Collection**. You can also click the **Go To...** menu at the top of the screen and select **Collection**.  
1. On the Collectors page, click **Add Source** next to a Hosted Collector.
1. Search for and select **ZeroFox Threat Intel**.
1. Enter a **Name** to display for the Source in the Sumo web application. The description is optional.
1. (Optional) For **Source Category**, enter any string to tag the output collected from the Source. Category metadata is stored in a searchable field called `_sourceCategory`.
1. (Optional) **Fields.** Click the **+Add Field** link to define the fields you want to associate, each field needs a name (key) and value.
   * ![green check circle.png](/img/reuse/green-check-circle.png) A green circle with a check mark is shown when the field exists in the Fields table schema.
   * ![orange exclamation point.png](/img/reuse/orange-exclamation-point.png) An orange triangle with an exclamation point is shown when the field doesn't exist in the Fields table schema. In this case, an option to automatically add the nonexistent fields to the Fields table schema is provided. If a field is sent to Sumo that does not exist in the Fields schema it is ignored, known as dropped. 
1. **Username**. Enter your ZeroFox username.
1. **Password**. Enter your Zerofox password.
1. **Sumo Logic Threat Intel Source ID**. Enter the Sumo Logic namespace where the indicators will be stored.
1. **Polling Interval**. The polling interval is set for one hour by default. You can adjust it based on your needs. This sets how often the source checks for new data.
1. **Processing Rules for Logs**. Configure any desired filters, such as allowlist, denylist, hash, or mask, as described in [Create a Processing Rule](/docs/send-data/collection/processing-rules/create-processing-rule).
1. When you are finished configuring the source, click **Save**.

## JSON schema

Sources can be configured using UTF-8 encoded JSON files with the Collector Management API. See [Use JSON to Configure Sources](/docs/send-data/use-json-configure-sources) for details.

| Parameter  | Type        | Value                                         | Required | Description                      |
|:-----------|:------------|:----------------------------------------------|:---------|:---------------------------------|
| schemaRef  | JSON Object | `{“type”: “ZeroFox Threat Intel”}`            | Yes      | Define the specific schema type. |
| sourceType | String      | `"Universal"`                                 | Yes      | Type of source.                  |
| config     | JSON Object | [Configuration object](#configuration-object) | Yes      | Source type specific values.     |

### Configuration Object

| Parameter | Type   | Required | Default | Description                                                                                                                                                                                               | Example      |
|:----------|:-------|:---------|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------|
| name      | String | Yes      | `null`  | Type a desired name of the source. The name must be unique per Collector. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_source`. | `"mySource"` |
| description | String | No | `null` | Type a description of the source. | `"Testing source"`
| category | String | No | `null` | Type a category of the source. This value is assigned to the [metadata](/docs/search/get-started-with-search/search-basics/built-in-metadata) field `_sourceCategory`. See [best practices](/docs/send-data/best-practices) for details. | `"mySource/test"`
| fields | JSON Object | No | `null` | JSON map of key-value fields (metadata) to apply to the Collector or source. Use the boolean field `_siemForward` to enable forwarding to SIEM.|`{"_siemForward": false, "fieldA": "valueA"}` |
| username | String | Yes | `null` | ZeroFox username. |  |
| password | String | Yes | `null` | Zerofox password. |  |
| userSourceId | String | Yes | `null` | The Sumo Logic namespace in which the indicators will be stored. |  |
| pollingIntervalHour | integer | Yes | `1 hour` | Time interval (in hours) after which the source will check for new data. |  |

### JSON example

<CodeBlock language="json">{MyComponentSource}</CodeBlock>

<a href="/files/c2c/zerofox/example.json" target="_blank">Download example</a>

### Terraform example

<CodeBlock language="json">{TerraformExample}</CodeBlock>

<a href="/files/c2c/zerofox/example.tf" target="_blank">Download example</a>

## FAQ

:::info
Click [here](/docs/c2c/info) for more information about Cloud-to-Cloud sources.
:::