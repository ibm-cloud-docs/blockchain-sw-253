---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-01"

keywords: smart contract, private data, private data collection, anchor peer, multicloud

subcollection: blockchain-sw-252

---



{{site.data.keyword.attribute-definition-list}}

# Deploy a smart contract
{: #ibp-console-smart-contracts}

<p>
<strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
<a href="/docs/blockchain-sw?topic=blockchain-sw-ibp-console-smart-contracts">2.1.2</a>,
<a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-smart-contracts">2.1.3</a>,
<a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-ibp-console-smart-contracts">2.5</a>,
<a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-smart-contracts">2.5.1</a>,
<a href="/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts">2.5.2</a>
</p>

A smart contract is the code, packaged as chaincode, that applications interact with to read and update data on the blockchain ledger. A smart contract turns business logic into an executable program that is agreed to and verified by all members of a blockchain network. This tutorial is the third part in the [sample network tutorial series](#ibp-console-smart-contracts-structure) and describes how to deploy smart contracts to start transactions in the blockchain network.
{: shortdesc}

**Target audience:** This topic is designed for network operators who are responsible for creating, monitoring, and managing the blockchain network. Additionally, application developers might be interested in the sections that reference how to create a smart contract.

## Sample network tutorial series
{: #ibp-console-smart-contracts-structure}

You are currently on the third part of our three-part tutorial series. This tutorial guides you through the process of using the console to deploy a smart contract onto a channel in your {{site.data.keyword.blockchainfull_notm}} Platform network.

* [Build a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-build-network#ibp-console-build-network) guides you through the process of hosting a network by creating an orderer and peer.
* [Join a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-join-network#ibp-console-join-network) guides you through the process of joining an existing network by creating a peer and joining it to a channel.
* **Deploy a smart contract on the network** (Current tutorial) Provides information on how to write a smart contract and deploy it on your network.

You can use the steps in these tutorials to build a network with multiple organizations in one cluster for the purposes of development and testing. Use the **Build a network** tutorial if you want to form a blockchain consortium by creating an orderer node and adding organizations. Use the **Join a network** tutorial to connect a peer to the network. Following the tutorials with different consortium members helps you create a truly **distributed** blockchain network.

Select the tutorial that corresponds to your channel configuration:
- <img src="../images/2-x_Pill.png" alt="version 2.x" width="30" style="width:30px; border-style: none"/>*** [Channel application capabilities and peer Fabric images are 2.x](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v2)
- <img src="../images/1-4_Pill.png" alt="version 1.4" width="30" style="width:30px; border-style: none"/> [Channel application capabilities are 1.4 and peer Fabric images are 1.4 or 2.x](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14)

*** Fabric v2.0 introduced a new distributed process to manage the lifecycle of a smart contract that allows for decentralizing the governance of smart contracts on a channel. Whenever possible, it is recommended that customers should move to using the new smart contract lifecycle to avoid any interruption of service in later upgrades when Fabric no longer supports the v1.4 process for installing and instantiating smart contracts.
{: important}
