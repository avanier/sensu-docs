---
title: "How to install plugins using assets"
linkTitle: "Installing Plugins with Assets"
description: "Assets are shareable, reusable packages that make it easy to deploy Sensu plugins. You can use assets to provide the plugins, libraries, and runtimes you need to power your monitoring workflows. Read the guide to get started using assets."
weight: 40
version: "5.3"
product: "Sensu Go"
platformContent: False
menu: 
  sensu-go-5.3:
    parent: guides
---

- [1. Download an asset definition from Bonsai](#1-download-an-asset-definition-from-bonsai)
- [2. Register the asset with Sensu](#2-register-the-asset-with-sensu)
- [3. Create a workflow](#3-create-a-workflow)
- [Next steps](#next-steps)

Assets are shareable, reusable packages that make it easy to deploy Sensu plugins.
You can use assets to provide the plugins, libraries, and runtimes you need to power your monitoring workflows.
See the [asset reference](../../reference/assets) for more information about assets.

### 1. Download an asset definition from Bonsai

You can discover, download, and share assets using [Bonsai, the Sensu asset index][16].
To use an asset, select the Download button on the asset page in Bonsai to download the asset definition for your platform and architecture.
Asset definitions tell Sensu how to download and verify the asset when required by a check, filter, mutator, or handler.

For example, here's the asset definition for version 1.0.1 of the [Sensu PagerDuty handler asset][19] for Linux AMD64.

{{< highlight json >}}
{
  "type": "Asset",
  "api_version": "core/v2",
  "metadata": {
    "name": "sensu-pagerduty-handler",
    "namespace": "default",
    "labels": {},
    "annotations": {}
  },
  "spec": {
    "url": "https://github.com/sensu/sensu-pagerduty-handler/releases/download/1.0.1/sensu-pagerduty-handler_1.0.1_linux_amd64.tar.gz",
    "sha512": "5facfb0706e5e36edc5d13993ecc813a4689c5ca502d70670268ca1c0679e9e2af79af75ee4f7a423b48f2e55524f6d81ce81485975eb3b70048cfa58f4af961",
    "filters": [
      "entity.system.os == 'linux'",
      "entity.system.arch == 'amd64'"
    ]
  }
}
{{< /highlight >}}

**Enterprise-only assets** (like the [ServiceNow](https://bonsai.sensu.io/assets/sensu/sensu-servicenow-handler) and [Jira event handlers](https://bonsai.sensu.io/assets/sensu/sensu-jira-handler)) require an active enterprise license. For more information about enterprise-only features and to active your license, see the [getting started guide](../../getting-started/enterprise).

### 2. Register the asset with Sensu

Once you've downloaded the asset definition, you can register the asset with Sensu using sensuctl.

{{< highlight shell >}}
sensuctl create --file sensu-sensu-pagerduty-handler-1.0.1-linux-amd64.json
{{< /highlight >}}

You can use sensuctl to verify that the asset is registered and ready to use.

{{< highlight shell >}}
sensuctl asset list
{{< /highlight >}}

### 3. Create a workflow

Now we can use assets in a monitoring workflow.
Depending on the asset, you may want to create Sensu checks, filters, mutators, and handlers.
The asset details in Bonsai are the best resource for information about asset capabilities and configuration.

For example, to use the [Sensu PagerDuty handler asset][19], create a `pagerduty` handler that includes your PagerDuty service API key and `sensu-pagerduty-handler` as a runtime asset.

{{< highlight json >}}
{
    "api_version": "core/v2",
    "type": "Handler",
    "metadata": {
        "namespace": "default",
        "name": "pagerduty"
    },
    "spec": {
        "type": "pipe",
        "command": "sensu-pagerduty-handler --token SECRET",
        "runtime_assets": ["sensu-pagerduty-handler"],
        "timeout": 10,
        "filters": [
            "is_incident"
        ]
    }
}
{{< /highlight >}}

Save the definition to a file, and add to Sensu using sensuctl.

{{< highlight shell >}}
sensuctl create --file filename.json
{{< /highlight >}}

Now that Sensu can create incidents in PagerDuty, we can automate this workflow by adding the `pagerduty` handler to our Sensu service checks.
To get started with checks, see the [guide to monitoring server resources](../monitor-server-resources).

You can use sensuctl to see available checks, handlers, and other Sensu resources.

{{< highlight shell >}}
sensuctl check list

sensuctl mutator list

sensuctl handler list
{{< /highlight >}}

### Next steps

See the [asset reference](../../reference/assets) more information about creating and sharing assets.

[1]: ../../reference/assets/
[2]: #creating-an-asset
[3]: https://bonsai.sensu.io
[6]: ../checks
[7]: ../filters
[8]: ../mutators
[9]: ../handlers
[16]: https://bonsai.sensu.io
[17]: ../../getting-started/enterprise
[19]: https://bonsai.sensu.io/assets/sensu/sensu-pagerduty-handler