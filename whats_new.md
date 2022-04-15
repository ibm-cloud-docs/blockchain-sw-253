---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-01"

keywords: IBM Blockchain Platform, release, new features, multicloud

subcollection: blockchain-sw-252

---



{{site.data.keyword.attribute-definition-list}}

# What's new
{: #whats-new}

<p>
<strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
<a href="/docs/blockchain-sw?topic=blockchain-sw-whats-new">2.1.2</a>,
<a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-whats-new">2.1.3</a>,
<a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-whats-new">2.5</a>,
<a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-whats-new">2.5.1</a>,
<a href="/docs/blockchain-sw-252?topic=blockchain-sw-252-whats-new">2.5.2</a>
</p>




## March 29, 2021
{: #whats-new-03-29-2021}

{{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 is now available with support for:

- For customers who want to use openCryptoki Hardware Security Module (HSM) on s390x, the platform now supports configuration of HSM with a daemon. For more information, see [Configure an HSM daemon](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-daemon).



## January 19, 2021
{: #whats-new-01-19-2021}

The {{site.data.keyword.blockchainfull}} Platform extension for VS Code V2.0 is now available for download from the Visual Studio Marketplace. This new version includes support for Fabric v2.0 lifecycle along with updated tutorials. [Download the extension](https://marketplace.visualstudio.com/items?itemName=IBMBlockchain.ibm-blockchain-platform) from the marketplace to get started then visit our [Developer Tooling](/docs/blockchain-sw-252?topic=blockchain-sw-252-develop-vscode#develop-vscode-install) topic for more information.

## November 02, 2020
{: #whats-new-11-02-2020}

{{site.data.keyword.blockchainfull_notm}} Platform now supports the Fabric v2.x smart contract lifecycle that allows for decentralized governance of smart contract definitions on a channel. The platform has been updated to support Kubernetes v1.17-v1.19 and OpenShift container Platform 4.4, 4.5.

**Support for Fabric v2.x lifecycle**

The series of processes around installing, managing, and using smart contracts, collectively known as the "lifecycle" of the smart contract, has been updated. This new lifecycle allows organizations to collaborate in the channel-level decision making process regarding smart contracts, eliminate the need for smart contract fingerprint matches, and allow smart contracts to be written with only the code relevant to an organization's business role.

The {{site.data.keyword.IBM_notm}} Developer tooling has been updated to support generation of Fabric v2.x smart contract packages as well as testing smart contracts by using the new lifecycle process. Learn more about how to [deploy a smart contract using Fabric v2.x](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v2) and [how to write powerful smart contracts](/docs/blockchain-sw-252?topic=blockchain-sw-252-write-powerful-smart-contracts) that leverage the new governance.

**New process for enabling Hardware Security Module (HSM) support**

A new process for configuring an HSM to work with your blockchain nodes is available and offers faster performance over the use of the existing HSM PKCS #11 proxy which is now deprecated. Current customers who are using the PKCS #11 proxy should check out the new process in the [Advanced deployment](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-build-docker) options.

**Ability to upgrade existing nodes and channel application capability to Fabric v2.x**

You continue to have the option to select the Fabric v1.4 or v2.x image when creating your CAs, peers, and ordering nodes. However, you now have the ability to upgrade your existing nodes that are running Fabric v1.4.x to the Fabric v2.x image. If you have peers using the Fabric v1.4.x image, you must upgrade your nodes and update your channel capabilities to take advantage of the new smart contract lifecycle.

For information about upgrading nodes, check out [Upgrading to a new version of Fabric](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern-components#ibp-console-govern-components-upgrade). For information about updating the capabilities of your channels, check out [Capabilities](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern#ibp-console-govern-capabilities).

**Enhancements to the certificate renewal process**

Because all actions on a blockchain network depend on the existence of valid and verifiable certificates, renewing certificate is vital to avoiding network outages. To streamline the certificate renewal process, the console now allows you to renew your CA TLS certificate, and peer and ordering node enrollment and TLS certificates. While it is preferable to renew certificates before they expire, it is possible to restore components whose certificates have already expired in many cases. Learn more about the new options in [Certificate management](/docs/blockchain-sw-252?topic=blockchain-sw-252-cert-mgmt#cert-mgmt-cert-types).

See the [Release notes](/docs/blockchain?topic=blockchain-release-notes-saas-20#11-02-2020) for more details on the new features that are included in this release.

## August 27, 2020
{: #whats-new-08-19-2020}

The {{site.data.keyword.blockchainfull_notm}} Platform can now be deployed onto OpenShift clusters from the Red Hat Marketplace, an open cloud catalog that makes it easier to discover and access certified software. Red Hat certified {{site.data.keyword.blockchainfull_notm}} Platform operator images are available in the marketplace and accessible from your OpenShift web console. This new deployment option is immediately available to deploy on any Red Hat OpenShift 4.3+ cluster, and provides a fast, integrated experience for deploying the blockchain console that can be used to create Certificate Authorities (CAs), peers, and ordering nodes, in the public cloud. See [Deploy from Red Hat Marketplace](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-ocp-rhm) to learn how.


## June 18, 2020
{: #whats-new-06-18-2020}

{{site.data.keyword.blockchainfull_notm}} Platform provides tighter integration with Red Hat solutions, including additional integration with Red Hat OpenShift 4.3. This latest release also makes available a set of Ansible Content Collections to help accelerate the deployment of blockchain solutions.

**IBM Blockchain Platform Ansible Playbooks**  

The {{site.data.keyword.blockchainfull_notm}} Platform improvements are designed to enable enterprises to launch production blockchain networks faster. This release helps organizations accelerate deployment through support of Ansible, an open source tool that automates provisioning, configuration management, and application deployment. **Ansible Content Collections** are packages of modules, plug-ins, and other Ansible content that automate these processes. The platform has published a set of Ansible Content Collections to help organizations deploy blockchain components and networks with greater speed. See [Getting started with Ansible playbooks on the {{site.data.keyword.blockchainfull_notm}} Platform](/docs/blockchain-sw-252?topic=blockchain-sw-252-ansible) to learn more.

**Hyperledger Fabric 2.0 images**

This release also includes improved usability and security by using **Hyperledger Fabric v2** and introduces the capability to deploy new peer and ordering nodes based on either Hyperledger Fabric v1.4.7 or v2.1.1. While all of the new Fabric v2 capabilities are not yet available on the platform, when you deploy a peer based on the Fabric v2.1.1 image, smart contracts are deployed into their own pod rather than inside a container on the peer pod, eliminating the dependency on the Docker daemon. Deploying peer and ordering nodes with the Fabric v2.x images is recommended to ensure that going forward you have access to the latest Fabric fixes and features. It is not currently possible to migrate existing nodes to Fabric 2.1.1 images.  The ordering service requires that all ordering nodes be running either Fabric v1.4.x or Fabric 2.x. Mixing ordering nodes with these different Fabric versions can introduce problems when attempting to update the consenter set. Peers, on the other hand can coexist on a channel even when they run different Fabric levels, as long as the channel application capability is not higher than the lowest peer Fabric version. **Customers running OpenShift Container Platform 3.11 in {{site.data.keyword.cloud_notm}} should upgrade their clusters to 4.3 now to fully take advantage of these new features.**


See the [Release notes](/docs/blockchain?topic=blockchain-release-notes-saas-20#06-18-2020) for more details on the new features that are included in this release.

## May 20, 2020
{: #whats-new-05-20-2020}

In addition to being able to link your {{site.data.keyword.blockchainfull_notm}} Platform instance to an {{site.data.keyword.cloud_notm}} Kubernetes service cluster, you can now also link your platform service instance to a Red Hat OpenShift cluster that is running in {{site.data.keyword.cloud_notm}}. The process is identical, the only difference is that when you link a cluster, you can now select your OpenShift cluster from the list of available clusters. See [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks) to review the deployment process.

If you are an Enterprise customer who is migrating to the {{site.data.keyword.blockchainfull_notm}} Platform, you must link your blockchain service instance to an {{site.data.keyword.cloud_notm}} Kubernetes service cluster. OpenShift clusters are not supported for Enterprise migration.
{: note}

## March 24, 2020
{: #whats-new-03-24-2020}

The following enhancements are included in this latest release:
- Support for Hyperledger Fabric v1.4.6
- Hardware Security Module (HSM) support for node identities
- Support for adding and removing ordering nodes from an existing ordering service
- Ability to override default CA, peer, ordering node configuration
- Full Java smart contract development support

See the [Release notes](/docs/blockchain?topic=blockchain-release-notes-saas-20#03-24-2020) for more details on the new features that are included in this release.

We've streamlined the documentation. If you are an existing customer, you might notice that a new `Tutorials` section was added in the table of contents under `Learn`. We've aggregated all of the tutorials in a single location under the Tutorials heading to make them easier to find.


## February 14, 2020
{: #whats-new-2-14-2019}

Enterprise Plan users can now upgrade their networks to the latest version of the {{site.data.keyword.blockchainfull_notm}} Platform, {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}. As part of the upgrade process, {{site.data.keyword.IBM_notm}} will upgrade your Enterprise Plan network from Fabric v1.1 to Fabric v1.4.3 and migrate your ordering service from Kafka to Raft consensus. You can then use the self guided upgrade tool to create new nodes on the {{site.data.keyword.blockchainfull_notm}} Platform 2.0 side by side with your Enterprise Plan network.

If possible, Enterprise Plan customers are encouraged to migrate to the {{site.data.keyword.blockchainfull_notm}} Platform 2.0 right away. If you do not need to preserve your ledger data on Enterprise Plan, you are encouraged to skip the upgrade process and create a new network on the {{site.data.keyword.blockchainfull_notm}} for {{site.data.keyword.cloud_notm}}. If you are ready to create a new network, go to [Getting Started with {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}](/docs/blockchain/reference?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks).

Since the Enterprise Upgrade documentation was released as a preview, version 1.4.5 of the Fabric Node SDK has been released. If your application uses the Node SDK, you need to upgrade the SDK to version 1.4.5 before you start using the upgrade tool.

## February 06, 2020
{: #whats-new-02-06-2020}

**Service availability in a new region**

The {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} is now available to be provisioned in one new region: **UK South** (London). Refer to the [locations](/docs/blockchain?topic=blockchain-ibp-regions-locations) information to see the data centers that are available in those regions.

## October 02, 2019
{: #whats-new-10-02-2019}

### Reminders for Starter Plan users
{: #whats-new-10-02-2019-reminders}

**Admin certificates for Starter plan instances expire one year from date of service instance creation.**
- When an admin certificate expires, you are no longer able to perform operations from the UI.  Admin certificates cannot be renewed because Starter Plan has been deprecated. 
- If you want to continue using Starter Plan after your admin certificate expires, you need to reset your network. Your network is reset back to the original one channel, two peers and one peer per organization. Any new nodes, channels, and smart contracts you have added since your Starter network was originally deployed need to be recreated in the new network.
- If you no longer need to use Starter Plan, now would be a good time to deploy a new instance of the next generation {{site.data.keyword.blockchainfull}} Platform. You can [preview the platform for free](/docs/blockchain?topic=blockchain-ibp-saas-pricing#ibp-saas-pricing-free) for 30 days.

**There is no migration from Starter Plan to the next generation {{site.data.keyword.blockchainfull_notm}}, but your chaincode can be reused.**
- Check out this [tutorial series](https://developer.ibm.com/series/ibm-blockchain-platform-console-video-series/){: external} to learn how to deploy the blockchain console and build a network.
- [Create](/docs/blockchain?topic=blockchain-ibp-saas-pricing#ibp-saas-pricing-free){: external} your next generation {{site.data.keyword.blockchainfull_notm}} Platform instance.
- See [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks){: external}.
- Check out our [FAQs](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-v2-faq).   

### The {{site.data.keyword.blockchainfull_notm}} Platform console UI has been updated
{: #whats-new-10-02-2019-Console}

Review the [release notes](/docs/blockchain-sw-252?topic=blockchain-sw-252-release-notes-sw-252) to see the latest features available for your network.

## August 27, 2019
{: #whats-new-8-27-2019}

The process to view logs for Starter Plan nodes has changed. Instead of viewing Starter logs by using the {{site.data.keyword.la_full_notm}} service and Kibana, you can now use the Open Dashboard service in {{site.data.keyword.cloud_notm}} to view the logs of your CA, peers and ordering nodes.

## August 7, 2019
{: #whats-new-8-7-2019}

Networks on Enterprise Plan will soon be upgraded to Fabric v1.4.3. The Upgrade allows your network to be migrated to a Raft based ordering service from Kafka.

This upgrade may cause breaking changes in your applications if they still use the peer based EventHub class of the Fabric SDKs. The peer based EventHub has been removed in Fabric v1.4.3. You must update your applications to use the new channel based event service. Because you can use channel events on Fabric v1.1, you can migrate your application at any time. For more information, see [How to use the channel-based event service](https://hyperledger.github.io/fabric-sdk-node/release-1.4/tutorial-channel-events.html){: external} in the Node SDK documentation.

If you are using Hyperledger Composer v0.19.x, upgrading your network to Fabric 1.4.3 will disrupt your application. You need to plan on shutting down your application before upgrading your network. When your upgrade is complete, you can upgrade your application to Composer v0.20.8.

Fabric v1.4 is the first long term support release of Hyperledger Fabric. You can learn more by visiting the [Whats new in v1.4](https://hyperledger-fabric.readthedocs.io/en/release-1.4/whatsnew.html){: external} in the Fabric documentation.

## June 18, 2019
{: #whats-new-6-18-2019}

The {{site.data.keyword.blockchainfull_notm}} Platform for Multicloud, which enables the use of the second-generation {{site.data.keyword.blockchainfull_notm}} Platform in your own infrastructure and the Kubernetes cloud provider of your choice, becomes generally available. This release allows the user interface console to be used to deploy and manage blockchain components in your own environment using {{site.data.keyword.cloud_notm}} Private. The {{site.data.keyword.blockchainfull_notm}} Platform for Multicloud uses Hyperledger Fabric v1.4.1 code base and supports deployment on {{site.data.keyword.cloud_notm}} Private v3.2.

This {{site.data.keyword.blockchainfull_notm}} Platform release includes the following key features:

**BUILD ---- Integrated developer experience**
- **Easily code** your smart contracts in Node.js, Golang, or Java, write client applications using the new {{site.data.keyword.blockchainfull_notm}} VS Code extension, leverage **SDK integration** with the user interface console, and learn from our rich tutorials and samples.
- **Simplified DevOps** allows you to move from development to test to production in a single environment by scaling up your Kubernetes resources to add more components.
- **Kubernetes service integration.** Leverage services such as Grafana and Prometheus for logging and Kibana for monitoring.
- **Up-to-date Fabric key features**. Leverage the latest features of Hyperledger Fabric v1.4.1:
    - [Raft ordering service](https://hyperledger-fabric.readthedocs.io/en/release-1.4/orderer/ordering_service.html#raft){: external}
    - [Private data collections](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14#ibp-console-smart-contracts-private-data) that provide increased data privacy by ensuring that ledger data is shared to only authorized peers via the gossip protocol.
    - [Service discovery](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html){: external}, allowing you to dynamically discover and update how your application interacts with your network.
    - [Channel access control lists](https://hyperledger-fabric.readthedocs.io/en/release-1.4/access_control.html){: external} that allow you additional control of the governance of your channels and smart contracts.

**OPERATE --- Total control of your deployments**
- **Deploy only the components you need**. Connect a peer to multiple channels and networks, or host an ordering service that business partners can connect to.
- **Maintain complete control of your identities**. Store and manage the keys that are used to administer your nodes in your own secure environment.
- **Unified operation**. The {{site.data.keyword.blockchainfull_notm}} Platform console allows you to deploy and manage all of your organizations and nodes in **one console** without having to rely on {{site.data.keyword.IBM_notm}} or other vendors to manage your orderers or Certificate Authority. You can also add or remove members from a blockchain consortium, create and join channels, and deploy smart contracts from your console.
- **Host or join a network**. Deploy peers hosted in your cluster to multiple channels on multiple clouds, or invite other organizations to join your consortium or channels while the organizations manage their nodes independently across infrastructures.
- **Manage access** of the users who can administer or monitor your nodes.
- **Direct access to the logs** of your nodes from your Kubernetes service. Use any supported third-party service to extract and analyze your logs.
- **Interact directly with your pods** using your Kubernetes service.
- **Dynamic signature collection** that allows better control over collaborative governance over channel configurations.

**GROW --- Scalability and flexibility**
- **Choose your compute**. You have the flexibility to decide the amount of CPU, memory, and storage you want to provision in your Kubernetes cluster. For more information, see [Allocating resources](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-allocate-resources).
- **Scale** up and down the resources in your Kubernetes cluster, paying for only what you need. For more information see [Pricing](/docs/blockchain-sw?topic=blockchain-sw-ibp-sw-pricing).
- **Disaster recovery and multizone high availability.** This ability duplicates your Kubernetes deployment across zones, enabling high availability (HA) of your components and disaster recovery (DR).
- **Run Anywhere**. Thanks to the **unified codebase** of the {{site.data.keyword.blockchainfull_notm}} Platform console, it is possible to run your components on any environment supported by {{site.data.keyword.cloud_notm}} Private.


**Instructions for deployment are in [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform for Multicloud](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks).**

- You can find more information in [About {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/blockchain?topic=blockchain-ibp-console-overview#ibp-console-overview).
- Updated tutorials for using the {{site.data.keyword.blockchainfull_notm}} Platform are available in the **{{site.data.keyword.blockchainfull_notm}} Platform console** subsection under the **HOW TO** category.
    * [Build a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-build-network#ibp-console-build-network) guides you through the process of hosting a network by creating CAs, an ordering service, and a peer.
    * [Join a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-join-network#ibp-console-join-network) explains how to join an existing network by creating a peer and joining it to a channel.
    * [Deploy a smart contract on the network](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14) provides information on how to write a smart contract and deploy it on your network.
- The {{site.data.keyword.blockchainfull_notm}} Platform offering is based on Hyperledger Fabric v1.4.1 and supports peer-to-peer gossip, service discovery, and private data. Visit this [topic](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14#ibp-console-smart-contracts-private-data) to learn how to configure private data on your network.

For more information about Hyperledger Fabric v1.4.1, see [Hyperledger Fabric documentation](https://hyperledger-fabric.readthedocs.io/en/release-1.4/){: external}. For more information about {{site.data.keyword.cloud_notm}} Private, see [{{site.data.keyword.cloud_notm}} Private v3.2 documentation](https://www.ibm.com/docs/en/cloud-private/3.2.0){: external}.

## May 31, 2019
{: #whats-new-5-31-2019}

The second-generation {{site.data.keyword.blockchainfull_notm}} Platform, which enables you to deploy, operate, and monitor your blockchain network, becomes generally available. This release includes a new user interface console that can be used to deploy and manage blockchain components in your own {{site.data.keyword.IBM_notm}} Kubernetes Service cluster on {{site.data.keyword.cloud_notm}}.

This {{site.data.keyword.blockchainfull_notm}} Platform release includes the following key features:

**BUILD ---- Integrated developer experience**
- **Easily code** your smart contracts in Node.js, Golang, or Java, write client applications using the new {{site.data.keyword.blockchainfull_notm}} VS Code extension, leverage **SDK integration** with the console, and learn from our rich tutorials and samples.
- **Simplified DevOps** allows you to move from development to test to production in a single environment by scaling up your Kubernetes resources to add more components.
- **Up-to-date Fabric key features**. Leverage the latest features of Hyperledger Fabric v1.4.1:
    -  [Raft ordering service](https://hyperledger-fabric.readthedocs.io/en/release-1.4/orderer/ordering_service.html#raft){: external}
    - **{{site.data.keyword.cloud_notm}} service integration.** Leverage the built-in {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cloud_notm}} Kubernetes Service Dashboard, {{site.data.keyword.la_full_notm}}, and {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).
    - [**Private data** collections](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14#ibp-console-smart-contracts-private-data) that provide increased data privacy by ensuring that ledger data is shared to only authorized peers via the gossip protocol.
    - [Service Discovery](https://hyperledger-fabric.readthedocs.io/en/release-1.4/discovery-overview.html){: external}, allowing you to dynamically discover and update how your application interacts with your network.
    - [Channel Access Control Lists](https://hyperledger-fabric.readthedocs.io/en/release-1.4/access_control.html){: external} that allow you additional control of the governance of your channels and smart contracts.

**OPERATE --- Total control of your deployments**
- **Deploy only the components you need**. Connect a peer to multiple channels and networks, or host an ordering service that business partners can connect to.
- **Maintain complete control of your identities**. Store and manage the keys that are used to administer your nodes without storing your private keys on the {{site.data.keyword.cloud_notm}}.
- **Centralized operation**. The {{site.data.keyword.blockchainfull_notm}} Platform console allows you to deploy and manage all of your organizations and nodes in **one central console** without having to rely on {{site.data.keyword.IBM_notm}} or other vendors to manage your orderers or Certificate Authority. You can also add or remove members from a blockchain consortium, create and join channels, and deploy smart contracts from your console.
- **Host or join a network**. Deploy peers hosted in your cluster to multiple channels on multiple clouds, or invite other organizations to join your consortium or channels while the organizations manage their nodes independently across infrastructures.
- **Manage access** of the users who can administer or monitor your nodes.
- **Direct access to the logs** of your nodes from the {{site.data.keyword.IBM_notm}} Kubernetes service. Use the {{site.data.keyword.la_full_notm}} service or a third-party service to extract and analyze your logs.
- **Interact directly with your pods** using the Kubernetes Dashboard. Exec into your pods and containers to execute commands and update certificates from the command line.
- **Dynamic signature collection** that allows better control over collaborative governance over channel configurations.

**GROW --- Scalability and flexibility**
- **Choose your compute**. You have the flexibility to decide the amount of CPU, memory, and storage you want to provision in your Kubernetes cluster. For more information, see see [Allocating resources](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-allocate-resources).
- **Scale** up and down the resources in your Kubernetes cluster, paying for only what you need. For more information see [Pricing](/docs/blockchain?topic=blockchain-ibp-saas-pricing).
- **Disaster recovery and multizone high availability.** This option duplicates your Kubernetes deployment across zones, enabling high availability (HA) of your components and disaster recovery (DR).
- **Run Anywhere** (instructions coming soon). Thanks to the **unified codebase** of the {{site.data.keyword.blockchainfull_notm}} Platform console, it is possible to run your components on {{site.data.keyword.cloud_notm}}, {{site.data.keyword.cloud_notm}} Private, and third-party public clouds.

- More information about the {{site.data.keyword.blockchainfull_notm}} Platform is available in [About {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/blockchain?topic=blockchain-ibp-console-overview#ibp-console-overview).
- Instructions on how to deploy the release into an {{site.data.keyword.IBM_notm}} Kubernetes Service cluster is available in [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks).
- New tutorials for using the {{site.data.keyword.blockchainfull_notm}} Platform are available in the **{{site.data.keyword.blockchainfull_notm}} Platform 2.0** subsection under the **HOW TO** category.
    * [Build a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-build-network#ibp-console-build-network) guides you through the process of hosting a network by creating an orderer and peer.
    * [Join a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-join-network#ibp-console-join-network) explains how to join an existing network by creating a peer and joining it to a channel.
    * [Deploy a smart contract on the network](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14) provides information on how to write a smart contract and deploy it on your network.
- The {{site.data.keyword.blockchainfull_notm}} Platform offering is based on Hyperledger Fabric v1.4.1 and supports peer-to-peer gossip, service discovery, and private data. Visit this [topic](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14#ibp-console-smart-contracts-private-data) to learn how to configure private data on your network.

## May 9, 2019
{: #whats-new-5-09-2019}

{{site.data.keyword.blockchainfull_notm}} releases version 1.0.0 of the {{site.data.keyword.blockchainfull_notm}} Platform Visual Studio (VS) Code Extension. This developer toolkit contains the following key capabilities:

**A reconfigured user interface for simpler navigation**

**Prescriptive and detailed tutorials that cover how to:**
- Develop a smart contract
- Provision an instance of the {{site.data.keyword.blockchainfull_notm}} service on {{site.data.keyword.cloud_notm}}
- Deploy and transact with your {{site.data.keyword.blockchainfull_notm}} Platform service instance

**All the popular features from previous releases, including:**
- Ability to debug smart contracts
- Sample code
- Updated wallet capability

For more information, see [Developing smart contracts with Visual Studio Code extension](/docs/blockchain?topic=blockchain-develop-vscode "Developing smart contracts with Visual Studio Code extension").

## April 23, 2019
{: #whats-new-4-23-2019}

{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private releases v1.0.2, which uses Hyperledger Fabric v1.4.0 code base and supports deployment on {{site.data.keyword.cloud_notm}} Private v3.1.2.

For more information about Hyperledger Fabric v1.4.0, see [Hyperledger Fabric documentation](https://hyperledger-fabric.readthedocs.io/en/release-1.4/){: external}. For more information about {{site.data.keyword.cloud_notm}} Private, see [{{site.data.keyword.cloud_notm}} Private v3.1.2 documentation](https://www.ibm.com/docs/en/cloud-private/3.1.2){: external}.

## February 8, 2019
{: #whats-new-2-08-2019}

{{site.data.keyword.blockchainfull_notm}} Platform releases a free 2.0 beta, the next generation of {{site.data.keyword.blockchainfull_notm}} Platform solutions that enables you to deploy, operate, and monitor your blockchain network. {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta includes a new user interface console, that can be used to deploy and manage blockchain components in your own {{site.data.keyword.IBM_notm}} Kubernetes Service cluster on {{site.data.keyword.cloud_notm}}. The {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta will allow you to:

**Build your network faster and easier within a seamless experience**

* Smooth integration between smart contract development (VS Code) and network management
* Simplified DevOps allows you to move from development to test to production from a single console
* Support for writing smart contracts in JavaScript, Java, and Go languages

**Operate and govern networks with total control**

* Deploy only the blockchain components you need (peer, ordering service, Certificate Authority)
* Redesigned console lets you manage network components in one place, no matter where they are deployed
* Maintain complete control of your identities, ledger, and smart contracts

**Grow distributed networks with ease with newly enabled multicloud flexibility**

* Connect to nodes running in any environment (on-prem, public, hybrid clouds)
* Easily connect a single peer to multiple industry networks
* Start small, pay as you grow for what you use with no upfront investment, and upgrade easily through Kubernetes

- More information about the {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta is available in [About {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/blockchain?topic=blockchain-ibp-console-overview#ibp-console-overview).
- Instructions on how to deploy the free 2.0 beta release into an {{site.data.keyword.IBM_notm}} Kubernetes Service cluster is available in [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform 2.0](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks#ibp-v2-deploy-iks).
- New tutorials for using the {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta are available in the **{{site.data.keyword.blockchainfull_notm}} Platform 2.0** subsection under the **HOW TO** category.
    * [Build a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-build-network#ibp-console-build-network) guides you through the process of hosting a network by creating an orderer and peer.
    * [Join a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-join-network#ibp-console-join-network) explains how to  joining an existing network by creating a peer and joining it to a channel.
    * [Deploy a smart contract on the network](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14) provides information on how to write a smart contract and deploy it on your network.
- The {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta offering is based on Hyperledger Fabric v1.4 and supports peer-to-peer gossip, service discovery, and private data. Visit this [topic](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v14#ibp-console-smart-contracts-private-data) to learn how to configure private data on your network.

- The {{site.data.keyword.blockchainfull_notm}} Visual Studio Code extension is available from the Visual Studio Code Marketplace. Developers can use the extension to create, test, and deploy smart contracts to an instance of Hyperledger Fabric. The extension is compatible with Hyperledger Fabric 1.3 and greater. For information about using the VS Code extension, see [Tools for smart contracts](/docs/blockchain-sw-252?topic=blockchain-sw-252-develop-vscode#develop-vscode).  

The table of contents is enhanced by grouping all getting started topics together into a section called **Getting started tutorials**. Additionally, each of the {{site.data.keyword.blockchainfull_notm}} Platform offerings is described in the **About {{site.data.keyword.blockchainfull_notm}} Platform** subsections are now contained under the **LEARN** section.

**Note:** Free cloud credits are no longer available for users of Starter Plan.

## December 7, 2018
{: #whats-new-12-07-2018}

The *Operate Starter Plan Network* and *Operate Enterprise Plan Network* topics are combined and replaced by a single tutorial about Using the Network Monitor.

## November 27, 2018
{: #whats-new-11-27-2018}

{{site.data.keyword.blockchainfull_notm}} Platform releases {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private. {{site.data.keyword.cloud_notm}} Private is an application platform for developing and managing containerized applications that are based on Kubernetes and it allows users to deploy Certificate Authorities (CAs), orderers, and peers on x86, LinuxONE and {{site.data.keyword.IBM_notm}} Z. {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private is based on Hyperledger Fabric v1.2.1 and is deployed by using Kubernetes Helm charts. After you install the Helm chart, you can find it as a bundled service in the {{site.data.keyword.cloud_notm}} Private Catalog. Note that this offering is more suitable for experienced Fabric users.

For more information about {{site.data.keyword.cloud_notm}} Private, see [{{site.data.keyword.cloud_notm}} Private v3.1.0 documentation](https://www.ibm.com/docs/en/cloud-private/3.1.0){: external}.

The release of {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} Private also marks the end of the {{site.data.keyword.blockchainfull_notm}} Platform Remote Peer (Beta) program. It is still possible to deploy a peer in {{site.data.keyword.cloud_notm}} Private or in AWS and connect it to a Starter Plan or Enterprise Plan network.

This release also debuts some improvements to the documentation table of contents. If you are a Starter or Enterprise user, your content can still be found in the **LEARN**, **HOW TO**, **REFERENCE**, and **HELP** sections, and the links are still the same. It might just be in a different subsection in the table of contents.

## November 13, 2018
{: #whats-new-11-13-2018}

{{site.data.keyword.blockchainfull_notm}} Platform releases {{site.data.keyword.blockchainfull_notm}} Platform for Amazon Web Services (AWS).

{{site.data.keyword.blockchainfull_notm}} Platform for AWS enables you to run peers in the AWS Cloud and connect the peers to existing blockchain networks in {{site.data.keyword.cloud_notm}}. Your peers in AWS can leverage the connection profile and other blockchain components in the existing networks, while giving you more flexibility to colocate your peers with other applications outside {{site.data.keyword.cloud_notm}}.

## October 4, 2018
{: #whats-new-10-04-2018}

{{site.data.keyword.blockchainfull_notm}} Platform upgrades Starter Plan from Hyperledger Fabric v1.1.0 to v1.2.1.

**Important:** Fabric v1.2.1 is currently not compatible with the Remote Peer beta, which uses a v1.1.0 peer. Starter Plan networks, which are created before October 4, 2018 and are based on Fabric v1.1.0, are not impacted and can still be used with the Remote Peer beta. {{site.data.keyword.blockchainfull_notm}} Platform will update the Remote Peer beta to use the v1.2.1 peer, which will be compatible with new Starter networks, which are at Fabric v1.2.1 level, and Enterprise networks, which are at Fabric v1.1.0 level. Until the Remote Peer beta is updated to Fabric v1.2.1, do not attempt to deploy a v1.1.0 remote peer with a new v1.2.1 Starter network.

## September 4, 2018
{: #whats-new-9-04-2018}

{{site.data.keyword.blockchainfull_notm}} Platform releases Remote Peer offering Beta. Remote Peer offering is based on Hyperledger Fabric v1.1.0. By using the Remote Peer, you can run {{site.data.keyword.blockchainfull_notm}} Platform peer nodes in your own {{site.data.keyword.cloud_notm}} Private or Amazon Web Services (AWS) cloud environment.

## June 15, 2018
{: #whats-new-6-15-2018}

{{site.data.keyword.blockchainfull_notm}} Platform releases Starter Plan GA.

## May 15, 2018
{: #whats-new-5-15-2018}

{{site.data.keyword.blockchainfull_notm}} Platform upgrades Enterprise Plan from Hyperledger Fabric v1.0.0 to v1.1.0.

## March, 18, 2018
{: #whats-new-3-18-2018}

{{site.data.keyword.blockchainfull_notm}} Platform releases Starter Plan Beta. Starter Plan offers you a development and testing environment to learn and practice in an {{site.data.keyword.blockchainfull_notm}} Platform network.

## August 11, 2017
{: #whats-new-8-11-2017}

{{site.data.keyword.blockchainfull_notm}} Platform replaces {{site.data.keyword.blockchainfull_notm}} on Cloud and releases Enterprise Plan.
