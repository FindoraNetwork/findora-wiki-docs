---
description: >-
  This tutorial will demonstrate how to build a subgraph and deploy it on
  Findora's Graph node
---

# Building & Deploying Subgraph (public Graph node)

{% hint style="danger" %}
Note: Projects wanting to deploy Subgraphs on Findora's public Graph node must first obtain approval. Once verified, your IP address will be whitelisted.
{% endhint %}

## Install the graph-cli <a href="#install-the-graph-cli" id="install-the-graph-cli"></a>

​[https://github.com/graphprotocol/graph-cli#installation](https://github.com/graphprotocol/graph-cli#installation)​

## Our first subgraph <a href="#our-first-subgraph" id="our-first-subgraph"></a>

Let's use blocklytics/ethereum-blocks subgraph as an example

```bash
git clone https://github.com/FindoraNetwork/ethereum-blocks
cd ethereum-blocks
```

We will use Findora's Graph node (you can [run your local](building-and-deploying-subgraph-local-node.md) one or set up a server for large projects)

Graph: [https://graph.findora.org](https://graph.findora.org)​

Management: [https://graph.findora.org:8020/](https://graph.findora.org:8020/)

Metrics: [https://graph.findora.org:8030/](https://graph.findora.org:8030/)

### Edit package.json file and add these lines <a href="#edit-package.json-file-and-add-these-lines" id="edit-package.json-file-and-add-these-lines"></a>

```bash
"create-findora": "graph create --node https://graph.findora.org:8020 findora/blocks",
"deploy-findora": "graph deploy --node https://graph.findora.org:8020 --ipfs http://graph.findora.org:5001 findora/blocks",
```

### Update the manifest <a href="#update-the-manifest" id="update-the-manifest"></a>

Update the manifest `subgraph.yaml` file `datasources[0]['network']` to `mainnet` or `testnet` accordingly to how you edited the network in your `docker-compose.yaml`\


If there is no need to index the entire blockchain, you can update the attribute `startBlock` to speed up the sync : `datasources[0]['source']['startBlock']`

{% hint style="info" %}
It is highly recommended to minimize the number of blocks to be indexed to avoid putting load on the RPCs and to speed up the usage of your subgraph/application
{% endhint %}

### Create and deploy the subgraph <a href="#create-and-deploy-the-subgraph" id="create-and-deploy-the-subgraph"></a>

```bash
yarn
yarn codegen
yarn build
yarn create-findora 
yarn deploy-findora
```

Sync begins and you are good to query your subgraph [https://graph.findora.org/graphql](https://graph.findora.org/graphql)

{% hint style="danger" %}
If multiple developers are deploying a graph and they deploy with the same name (ie findora/blocks), you will encounter conflict issues. It's recommended to build your own indexer node for your own testing. [See here](building-and-deploying-subgraph-local-node.md).
{% endhint %}
