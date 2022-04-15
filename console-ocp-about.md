---

copyright:
  years: 2019, 2022
lastupdated: "2022-04-01"

keywords: IBM Blockchain Platform, system requirements, Kubernetes, behind a firewall, azure, multicloud

subcollection: blockchain-sw-252

---

{{site.data.keyword.attribute-definition-list}}



# About {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2
{: #console-ocp-about}

<p>
<strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
<a href="/docs/blockchain-sw?topic=blockchain-sw-console-ocp-about">2.1.2</a>,
<a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-console-ocp-about">2.1.3</a>,
<a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-console-ocp-about">2.5</a>,
<a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-console-ocp-about">2.5.1</a>,
<a href="/docs/blockchain-sw-252?topic=blockchain-sw-252-console-ocp-about">2.5.2</a>
</p>

The {{site.data.keyword.blockchainfull}} Platform 2.5.2 enables a consortium of organizations to easily build and join a blockchain network [on-prem](#x4561212){: term}, or on any private, public, or hybrid multicloud that uses Kubernetes. Customers can deploy their nodes on the cloud platform of their choice and connect to any {{site.data.keyword.blockchainfull_notm}} Platform network, whether it is deployed on your own Kubernetes cluster or with the {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}. The {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 leverages Hyperledger Fabric v1.4.12 and v2.2.5 and supports deployment on multiple Kubernetes distributions.
{: shortdesc}

{{site.data.keyword.blockchainfull_notm}} Platform is based on Hyperledger Fabric v1.4.12 and v2.2.5 and is {{site.data.keyword.IBM_notm}}'s commercial distribution of Hyperledger Fabric. A key benefit of the platform is that {{site.data.keyword.IBM_notm}} tests the open source code for security vulnerabilities daily and provides 24x7x365 support with SLAs appropriate for production environments.

Watch the following video for an introduction to blockchain and the {{site.data.keyword.blockchainfull}} Platform:

![Key concepts video](https://www.youtube.com/embed/AvQa1W38J4I){: video output="iframe" data-script="#video-transcript-key-concepts" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

## Video script
{: #video-transcript-key-concepts}
{: notoc}

By now you’ve probably heard of the IBM Blockchain Platform, the leading permissioned enterprise blockchain solution in the world. But what is a permissioned blockchain? And what is the IBM Blockchain Platform? The modern world is interwoven and interactive place.

But under the surface it’s still following some pretty old rules.

Jerry here on the left uses a different record keeping system than Door2Door Logistics on the right, which means they have to spend a lot of time figuring out what the truth is before they can make a deal.

This process is not just slow, it’s vulnerable. A successful hack or other problem can mean records are lost forever. As a result, businesses sacrifice efficiency for security and lock their records away.

But what if businesses shared their records, and shared the burden of protecting them? What if Jerry’s Modern Fabrics and Door2Door Logistics and their business partners never had to spend time arguing over who’s right because every time an asset moves from one to the other everyone’s records updated at the same time? And what if those records, once written, could never been changed?

This network, leveraging what’s called Distributed Ledger Technology, already exists. It’s an open blockchain network like Bitcoin. But there’s a problem. Businesses don’t necessarily want the records of their transactions shared with everyone, especially in a network like Bitcoin where users are unknown. In some industries, it’s actually illegal to share data that way.

What Jerry’s Modern Fabrics and Door2Door Logistics need is a permissioned blockchain like IBM Blockchain Platform, where businesses can form networks with known, established partners and still take advantage of the robustness and efficiency of blockchains. But this too creates a problem. Who owns this network? Who runs it? The answer is: no one does.

Once an IBM Blockchain network has been established, its rules and practices are managed collectively, mimicking the kind of consensus process that governs the way transactions themselves are approved and written to the ledgers in the network.

But the IBM Blockchain Platform doesn’t just stop with permissions and identities, users also have the ability to create channels where a few members of a network can get together and transact privately.

Additionally, private data collections can be established, which allows a few channel members to share certain transactions just with each other, without needing a whole separate channel.

Because components are hosted in clusters that are owned and controlled by users, the IBM Blockchain Platform is naturally compliant with data residency rules.

All of these processes are managed through an award winning UI we call the console, which, along with custom APIs, makes the powerful open-source Hyperledger Fabric blockchain painless to use.

The console integrates seamlessly with the rest of the IBM Blockchain Platform suite, including a powerful VS Code extension which allows users to create and test smart contracts and applications and then package and install them on production networks.

Because the console can run on both IBM Cloud and any cloud supported by Red Hat’s Open Shift, the console can run nearly everywhere and consoles in different clouds can connect to each other and to nodes deployed on Hyperledger Fabric.

But how many CAs, which create identities and define organizations, do I need?

How many peers, which host ledgers and have smart contracts installed on them, should I deploy on a channel to make sure I have no downtime?

Because you only pay for the compute you use, it’s painless to transition from pilot programs to full production networks using the IBM Blockchain Platform. The IBM Garage is here to help assist you in finding the right configuration for every use case.

The world is moving too fast to keep doing things the old way. Go to cloud dot IBM dot com today and check out the IBM blockchain platform.

## What {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 offers
{: #console-ocp-about-offers}

The {{site.data.keyword.blockchainfull_notm}} Platform provides a flexible management platform that runs on Kubernetes. The offering includes an award-winning management console that allows you to easily deploy blockchain components, build a multicloud blockchain network, and perform network management and maintenance.

This offering includes two deployment options:  

**Full platform**

Includes the operator, management console, peer, CA, ordering node, and smart contract container images. The {{site.data.keyword.blockchainfull_notm}} Platform management console can be used to create all of the fundamental components of a Hyperledger Fabric network: a Certificate Authority (CA), an ordering service, and peers, on your local cluster. You can also use your console to operate a distributed multicloud network by importing nodes that were deployed by using other consoles. For more information about the building blocks of Hyperledger Fabric networks, see the [blockchain component overview](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-component-overview).

**{{site.data.keyword.blockchainfull_notm}} images**  

For experienced Hyperledger Fabric customers, a purchase of {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 includes an entitlement to the peer, CA, ordering node, and smart contract container images that are signed and supported by {{site.data.keyword.IBM_notm}}. These images are based on the open source Hyperledger Fabric code base and contain a number of enhancements for stability and serviceability. The images are bundled with support from {{site.data.keyword.IBM_notm}}. The {{site.data.keyword.blockchainfull_notm}} Platform management console and operator are not among the images that are included in this entitlement. For more information, see [{{site.data.keyword.blockchainfull_notm}} images for Hyperledger Fabric](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-images#blockchain-images).

The {{site.data.keyword.blockchainfull_notm}} Platform includes the following key features:

**BUILD ---- Integrated developer experience**
- **Deploy easily**. Use Ansible Playbooks or the Red Hat Marketplace to deploy networks quicker than ever before.
- **Easily code** your [smart contracts](#x8888420){: term} in Node.js, Golang, Java, or JavaScript. Use the {{site.data.keyword.blockchainfull_notm}} Platform Developer Tools to easily develop smart contracts locally. Leverage **SDK integration** with the console, and learn from our rich tutorials and samples.
- **Simplified DevOps** allows you to move from development to test to production in a single environment by scaling up your Kubernetes resources to add more components.
- **Up-to-date Fabric key features**. Choose which version of Hyperledger Fabric you want to use when deploying peers or ordering nodes. Leverage the latest features of Hyperledger Fabric v1.4.12 and v2.2.5:
    - [Smart contract lifecycle](https://hyperledger-fabric.readthedocs.io/en/release-2.2/chaincode_lifecycle.html){: external}
    - [Raft ordering service](https://hyperledger-fabric.readthedocs.io/en/release-2.2/orderer/ordering_service.html#raft){: external}
    - [Private data collections](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v2#ibp-console-smart-contracts-v2-private-data) that provide increased data privacy by ensuring that ledger data is shared to only authorized peers via the gossip protocol.
    - [Fabric Node OUs](https://hyperledger-fabric.readthedocs.io/en/release-2.2/membership/membership.html#node-ou-roles-and-msps){: external}
    - [Service discovery](https://hyperledger-fabric.readthedocs.io/en/release-2.2/discovery-overview.html){: external}, allowing you to dynamically discover and update how your application interacts with your network.
    - [Channel access control lists](https://hyperledger-fabric.readthedocs.io/en/release-2.2/access_control.html){: external} that allow you additional control of the governance of your channels and smart contracts.

**OPERATE --- Total control of your deployments**
- **Host or join a network**. Deploy peers that are hosted in your cluster to multiple channels on multiple clouds, or invite other organizations to join your consortium or channels while the organizations manage their nodes independently across infrastructures.
- **Maintain complete control of your identities**. Store and manage the keys that are used to administer your nodes. Optionally, use a [Hardware Security Module (HSM)](#x6704988){: term} to generate and store the private key of your nodes.
- **Run Anywhere**. Thanks to the **unified codebase** of the {{site.data.keyword.blockchainfull_notm}} Platform console, it is possible to run your components on any Kubernetes v1.20 - v1.23 container platform on x86_64 or s390x.
- **Unified operation**. The {{site.data.keyword.blockchainfull_notm}} Platform console allows you to deploy and manage all of your organizations and nodes in **one console**. You can also add or remove members from a blockchain consortium, create and join channels, and deploy smart contracts from your console.
- **Dynamic signature collection** that allows better control over collaborative governance over channel configurations.
- **Elimination of Docker-in-Docker for smart contracts** allows smart contract pods to be run more securely, without peers needing privileged access.
- **Manage access** of the users who can administer or monitor your nodes.
- **Interact directly with your pods** using your Kubernetes service.
- **Direct access to the logs** of your nodes from your  Kubernetes service. Use  any supported third-party service to extract and analyze your logs.
- **Kubernetes service integration.** Leverage services such as {{site.data.keyword.la_full_notm}} for logging and Prometheus and {{site.data.keyword.mon_full_notm}} for monitoring.
- **Upgrade the Fabric version of your nodes.** Nodes running Fabric version 1.4.x can be [upgraded to 2.x](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern-components#ibp-console-govern-components-upgrade). After which, the capabilities of your channels can also be increased to v2.0, allowing full access to the latest Fabric features like the smart contract lifecycle.

**GROW --- Scalability and flexibility**
- **Choose your compute**. You have the flexibility to decide the amount of CPU, memory, and storage you want to provision in your Kubernetes cluster. For more information, see [Allocating resources](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-allocate-resources).
- **Scale** up and down the resources in your Kubernetes cluster, paying for only what you need. For more information, see [Pricing](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-sw-pricing).
- **Disaster recovery and multi-region high availability (HA).** This option duplicates your Kubernetes deployment across  regions, enabling high availability (HA) of your components and disaster recovery (DR).
- **Connect to other Fabric networks**: Join {{site.data.keyword.blockchainfull_notm}} Platform peers to any network running Hyperledger Fabric components. Similarly, you can invite Fabric peers to join channels hosted on an ordering service deployed on the {{site.data.keyword.blockchainfull_notm}} Platform. Note that you will need to use Hyperledger Fabric APIs or the CLI.

Have questions and want to speak to an {{site.data.keyword.blockchainfull_notm}} Platform expert? [Schedule a consult](https://www.ibm.com/cloud/blockchain-platform/developer?schedulerform){: external} now to learn more about how blockchain can transform your business.

## Supported Platforms
{: #console-ocp-about-prerequisites}

**Reminder:** {{site.data.keyword.containerlong_notm}} 1.19 is no longer supported. If your {{site.data.keyword.blockchainfull_notm}} Platform instance is linked to an {{site.data.keyword.containerlong_notm}} 1.19 cluster, you must immediately upgrade it to {{site.data.keyword.containerlong_notm}} 1.20 or 1.21. To get started, see [1.20 considerations](/docs/containers?topic=containers-cs_versions#cs_v120) and [1.21 considerations](/docs/containers?topic=containers-cs_versions#cs_v121). For the actual steps that are required, see [Updating clusters, worker nodes, and cluster components](/docs/containers?topic=containers-update#update). For the list of {{site.data.keyword.containerlong_notm}} supported versions and expiration dates see the [release history](/docs/containers?topic=containers-cs_versions#release-history).

All documentation on supported environments applies to the latest version of the code only. If necessary, refer to the [upgrade information](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern-components). For release-specific details, see [release notes](/docs/blockchain-sw-252?topic=blockchain-sw-252-release-notes-saas-20).


The {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 can be deployed with the Kubernetes distributions on the following platforms:

| Kubernetes distribution | Version | Hardware |  Tested configuration|
|----|----|----|-----|
| OpenShift Container Platform | 4.6, 4.7, 4.8, 4.9 |  x86_64 |  4.6, 4.7, 4.8, 4.9 |
| OpenShift Container Platform on {{site.data.keyword.cloud_notm}} |  4.6, 4.7, 4.8, 4.9 | x86_64 |  4.6, 4.7, 4.8, 4.9 |
| OpenShift Container Platform on LinuxONE |  4.6, 4.7, 4.8 | s390x | 4.6, 4.7, 4.8 |
| Kubernetes ***   | v1.20 - v1.23 | x86_64 | v1.20 - v1.23 |
{: caption="Table 1. Supported platforms" caption-side="bottom"}

*** If you want to use {{site.data.keyword.IBM_notm}} Kubernetes Service, we recommend that you check out the [{{site.data.keyword.blockchainfull_notm}} Platform for IBM Cloud](/docs/blockchain?topic=blockchain-ibp-v2-deploy-iks){: external} offering unless you specifically require this offering. See [Is IBM Blockchain Platform 2.5.2 suitable for you](/docs/blockchain-sw-252?topic=blockchain-sw-252-get-started-console-ocp#get-started-console-ocp-suitable).    

{{site.data.keyword.blockchainfull_notm}} Platform does not support IBM Cloud Virtual Server for VPC and Virtual Private Cloud (VPC).
{: note}

If you are running on Azure Kubernetes Service, Amazon Web Services, Rancher, Amazon Elastic Kubernetes Service, or Google Kubernetes Engine, then you need to set up the NGINX Ingress controller and it needs to be running in SSL passthrough mode. For more information, see [Considerations when using Kubernetes distributions](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-k8#console-deploy-k8-considerations). If you are using OpenShift with a load balancer that is external to the OpenShift cluster, configuring the external load balancer to use SSL passthrough is required.
{: important}


### Fabric Component Support
{: #fabric-component-support}

Support for Hyperledger Fabric **v1.4 is now deprecated**, and support for Fabric v1.4 will be removed from  {{site.data.keyword.blockchainfull_notm}} Platform on March 31, 2023. Users should therefore [upgrade to Fabric v2.2](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern-components#ibp-console-govern-components-upgrade) as soon as possible. Your applications may  require changes as a result of upgrading to v2.2, so please plan for appropriate testing.
Note that Fabric v1.4 has not been supported by the Hyperledger community since April of 2021. In addition, Fabric v1.4 uses Golang v1.14, which is no longer receiving security updates from the Golang community.
{: important}

The following support levels are provided for Hyperledger Fabric v1.4.12 (Deprecated), v2.2.4, v2.2.5, and Fabric CA v1.5.0 and v1.5.2.

Using IBM Certified Fabric Images, Kubernetes Operator, and Certified Fabric Operations Console **are required for support** and provide Hyperledger Fabric clients with a verified production setup, simplified management and support, and verified security patches.
{: important}

| Fabric Component | Support Level |
|----|----|
| IBM Certified Fabric images deployed using Kubernetes Operator and managed via the Certified Fabric Operations Console image. | All Certified Fabric images include IBM fix support for [supported Hyperledger Fabric versions](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-ocp-about#fabric-component-support). |
| Supported Environments | Recent [Kubernetes and OpenShift versions](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-ocp-about#console-ocp-about-prerequisites) on IBM Cloud, third-party Cloud or local installations. |
| Hyperledger Fabric without IBM Certified Images, Kubernetes Operator or Certified Fabric Operations Console image. | Not included in support - [community support only](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-support#blockchain-support-resources) |
| Hyperledger Fabric Labs Support | Fabric Operations Console via Certified Image and deployed by Kubernetes Operator is supported. |
| Hyperledger Fabric Open Source Projects - [IBM Blockchain GitHub](https://github.com/ibm-blockchain) | Open source projects are not included in support, with the exception of [Ansible](/docs/blockchain-sw-252?topic=blockchain-sw-252-ansible). All other open source projects are [community support only](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-support#blockchain-support-resources). | 
| Hyperledger Fabric SDK and CLI | Basic connectivity diagnostics is supported. Code support and SDK API usage and tuning are not included in support - [community support only](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-support#blockchain-support-resources). |
| Hyperledger Fabric Chaincode | Basic chaincode diagnostics is supported. Code support and tuning are not included in support - [community support only](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-support#blockchain-support-resources). |
| Deployment Architecture and Design | Basic deployment and management of highly available [peer](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-ha#ibp-console-ha-peers), [orderer](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-ha#ibp-console-ha-ordering-service), and [Certificate Authority](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-ha#ibp-console-ha-ca) nodes via the Console are supported. Detailed Deployment Architecture and Design are not included in support - see [deployment options](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment) for more information. |
| Solution Architecture and Design | [Deploying and managing smart contracts](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v2) via the Console are supported. Solution Architecture and Design are not included in  support. |
| Performance Tuning | [Resource allocation](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-options) via the Console is supported. Detailed performance analysis and tuning of the environment or application code are not included in support - see the documentation on creating [highly available applications and using indexes with CouchDB](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-app#console-app-couchdb). |
| Certificate Renewal | [Automatic](/docs/blockchain-sw-252?topic=blockchain-sw-252-cert-mgmt#cert-mgmt-auto-renewal) and [Manual](/docs/blockchain-sw-252?topic=blockchain-sw-252-cert-mgmt#cert-mgmt-manual-renewal) Certificate renewal via the Certified Console image is supported. The user is responsible for keeping track of identities and performing manual certificate renewal. Using a [Certificate Management Solution](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-identities#storing-and-managing-certificates-in-ibm-cloud-certificate-manager) is recommended for keeping track of identities and certificates. |
{: caption="Table 2. Fabric component support" caption-side="bottom"}

## License and pricing
{: #console-ocp-about-license}

Your {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 entitlement includes both the full platform and the {{site.data.keyword.blockchainfull_notm}} images.

The entitlement does not include a Kubernetes distribution. You must procure that separately.
{: note}

After you purchase an entitlement, you can access your [My IBM dashboard](https://myibm.ibm.com/dashboard/){: external} to obtain your entitlement key for the offering. This key is required to deploy the release. **When  you choose this option, you are responsible for provisioning your own Kubernetes cluster.**

For more information, see [Pricing](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-sw-pricing).

## Considerations and limitations
{: #console-ocp-about-considerations}

- This offering does not include an entitlement to Red Hat OpenShift.
- You are responsible for the management of health monitoring, logging, and resource usage of your blockchain components.
- Users of this offering must manage their own security and infrastructure. The {{site.data.keyword.blockchainfull_notm}} Platform does not provision or provide those services.
- Persistent storage is required. Host-local storage volumes are not supported.
- You must have the cluster admin role in order to deploy the product.
- The console creates nodes based on the Hyperledger Fabric v1.4.12 and v2.2.5 node images.
- You can deploy only one {{site.data.keyword.blockchainfull_notm}} Platform console per Kubernetes namespace or OpenShift project. If you plan to create multiple blockchain networks, for example to create different environments for development, staging, and production, you should create a unique project or namespace for each environment.
- You cannot upgrade a deployed network from {{site.data.keyword.blockchainfull_notm}} Platform for Multicloud to {{site.data.keyword.blockchainfull_notm}} Platform v2.5.2.
- {{site.data.keyword.blockchainfull_notm}} Platform is not supported on OpenShift Online.
- OpenShift customers can preview the {{site.data.keyword.blockchainfull_notm}} Platform at no charge for 30 days when you select the free trial version available from the Red Hat Marketplace.

## Installing {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2
{: #console-ocp-about-install}

The {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 uses a [Kubernetes Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/){: external} to install the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster and manage the deployment of your nodes. When you purchase the {{site.data.keyword.blockchainfull_notm}} Platform license from Passport Advantage Online, you receive a token that provides access to {{site.data.keyword.IBM_notm}} Entitlement registry. You can use your token with the commands and files that are provided in the installation guide to automatically download the Docker images and start the operator and console on your cluster. When you are ready to get started, see [Deploy {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 on the OpenShift Container Platform](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-ocp). If you are deploying the platform on other Kubernetes distributions, see [Deploy {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 on Kubernetes](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-k8).

### Installing behind a firewall
It is also possible to install and deploy the {{site.data.keyword.blockchainfull_notm}} Platform behind a firewall, without having access to the public internet. For more information, see [Deploying IBM Blockchain Platform 2.5.2 on the OpenShift Container Platform behind a firewall](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-ocp-firewall). Otherwise, for other Kubernetes distributions see [Deploying IBM Blockchain Platform 2.5.2 on Kubernetes behind a firewall](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-k8-firewall).

**Looking for a way to script the deployment of the service?** Check out the [Ansible playbooks](/docs/blockchain-sw-252?topic=blockchain-sw-252-ansible), a powerful tool for scripting the deployment of components in your blockchain network.

## Security Considerations
{: #console-ocp-about-security}

Because these components are deployed on your own infrastructure, you are responsible for managing their security. This includes important areas of security, such as Identity and Access Management, key management, and data encryption. Review the following topic on [Security](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-security) for the list of considerations.

## Getting support
{: #console-ocp-about-support}

For more information about how to get support on {{site.data.keyword.blockchainfull_notm}} Platform, in addition to free blockchain developer resources and support forums that you can use to troubleshoot problems, see [Getting support](/docs/blockchain-sw-252?topic=blockchain-sw-252-blockchain-support#blockchain-support).

## Next steps
{: #console-ocp-about-next-steps}

When you are ready to learn how to deploy an instance of the {{site.data.keyword.blockchainfull_notm}} Platform to your Kubernetes cluster see [Getting started with {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2](/docs/blockchain-sw-252?topic=blockchain-sw-252-get-started-console-ocp).
