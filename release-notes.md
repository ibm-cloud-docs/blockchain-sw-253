---

copyright:
  years: 2014, 2022
lastupdated: "2022-04-05"

keywords: release note, latest changes, Hyperledger Fabric, multicloud

subcollection: blockchain-sw-252

---



{{site.data.keyword.attribute-definition-list}}

# Release notes
{: #release-notes-sw-252}

Use these release notes to learn about the latest changes to {{site.data.keyword.blockchainfull}} Platform for {{site.data.keyword.cloud_notm}} built on Hyperledger Fabric [v1.4.12](https://github.com/hyperledger/fabric/releases/tag/v1.4.12) and [v2.2.5](https://github.com/hyperledger/fabric/releases/tag/v2.2.5).
{: shortdesc}


[Installing the 2.5.2 fix pack](/docs/blockchain-sw-252?topic=blockchain-sw-252-install-fixpack) provides instructions on how to apply the latest fix pack to your blockchain instance.  

[Installing patches](/docs/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-manage-patch) provides instructions on how to apply patches to your existing blockchain nodes. Patches are cumulative, so select the latest available patch to include all earlier patches.

## 05 Apr 2022
{: #05-04-2022}

**Certificate Authority (CA) patch 1.5.2-8, Peer and ordering node patch 1.4.12-11, 2.2.5-3.**

Miscellaneous bug fixes and security patches.

Severity: medium

## 08 Mar 2022
{: #08-03-2022}

**Certificate Authority (CA) patch 1.5.2-7, Peer and ordering node patch 1.4.12-10, 2.2.5-2.**

Miscellaneous bug fixes and security patches.

Severity: medium

## 08 Feb 2022
{: #08-02-2022}

**Certificate Authority (CA) patch 1.5.2-6, Peer and ordering node patch 1.4.12-9, 2.2.5-1.**

Miscellaneous bug fixes and security patches.

Severity: medium

## 11 Jan 2022
{: #11-01-2022}

**Certificate Authority (CA) patch 1.5.2-5, Peer and ordering node patch 1.4.12-8, 2.2.4-5.**

Miscellaneous bug fixes and security patches.


## 14 Dec 2021
{: #14-12-2021}

**Certificate Authority (CA) patch 1.5.2-4, Peer and ordering node patch 1.4.12-7, 2.2.4-4.**

Miscellaneous bug fixes and security patches.


## 16 Nov 2021
{: #16-11-2021}

**Certificate Authority (CA) patch 1.5.2-3, Peer and ordering node patch 1.4.12-6, 2.2.4-3.**

Miscellaneous bug fixes and security patches.




## 26 Oct 2021
{: #26-10-2021}

**Certificate Authority (CA) patch 1.5.2-2, Peer and ordering node patch 1.4.12-5, 2.2.4-2.**

Miscellaneous bug fixes and security patches.


## 05 Oct 2021
{: #05-10-2021}

**Certificate Authority (CA) patch 1.5.2-1, Peer and ordering node patch 1.4.12-3, 2.2.4-1.**

Miscellaneous bug fixes and security patches.


## 10 Aug 2021
{: #10-08-2021}

Miscellaneous bug fixes and security patches.

Export certificates in .pem format for easy management and maintenance in {{site.data.keyword.cloud_notm}} Certificate Manager. See [viewing and updating identities](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-identities#ibp-console-identities-update-identities) to learn more details.



## 14 Jul 2021
{: #14-07-2021}

**Certificate Authority (CA) patch 1.5.0-1, Peer and ordering node patch 1.4.12-2, 2.2.3-2**

Miscellaneous bug fixes and security patches.



## 16 Jun 2021
{: #16-06-2021}

**Certificate Authority (CA) patch 1.4.9-8, Peer and ordering node patch 1.4.12-1, 2.2.3-1**

Miscellaneous bug fixes and security patches.

The platform has been updated to include support for Hyperledger Fabric v1.4.12 and v2.2.3.


## 05 May 2021
{: #05-05-2021}

**Certificate Authority (CA) patch 1.4.9-7, Peer and ordering node patch 1.4.11-2, 2.2.2-2**

Miscellaneous bug fixes and security patches.





## 29 Mar 2021
{: #29-03-2021}

**Certificate Authority (CA) patch 1.4.9-6, Peer and ordering node patch 1.4.11-1, 2.2.2-1** 

## 22 Feb 2021
{: #02-22-2021}

**Certificate Authority (CA) patch 1.4.9-5, Peer and ordering node patch 1.4.9-5 and 2.2.1-5**

## 12 Jan 2021
{: #01-12-2021}

**Certificate Authority (CA) patch 1.4.9-4, Peer and ordering node patch 1.4.9-4, 2.2.1-4**

Miscellaneous bug fixes and security patches.

### New logging configuration panel
{: #01-12-2021-logger-ui}

A new panel is available to override peer and ordering node log levels for specific component loggers. See [Configuring node logging](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-icp-manage#ibp-console-manage-logger) for more information.

## 08 Dec 2020
{: #12-08-2020}

**Certificate Authority (CA) patch 1.4.9-3, Peer and ordering node patch 1.4.9-3, 2.2.1-3**

Miscellaneous bug fixes and security patches.  


## 19 Nov 2020
{: #11-19-2020}

**Certificate Authority (CA) patch 1.4.9-2, Peer and ordering node patch 1.4.9-2, 2.2.1-2**

Miscellaneous bug fixes and security patches.  




## 30 Oct 2020
{: #10-20-2020}


**Certificate Authority (CA) patch 1.4.9-1, Peer and ordering node patch 1.4.9-1, 2.2.1-1**

Miscellaneous bug fixes and security patches.  

If you are running **OpenShift Container Platform 3.11** in {{site.data.keyword.cloud_notm}}, it is recommended that you [upgrade your cluster to 4.4](https://docs.openshift.com/container-platform/4.4/migration/migrating_3_4/planning-migration-3-to-4.html){: external} now in order to fully take advantage of the new features. After you upgrade your cluster, follow instructions to [refresh your blockchain console](/docs/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-refresh) to experience the latest functionality in this release.
{: important}

### Fabric v2.x node upgrade
{: #11-02-2020-upgrade}

In addition to deploying new nodes based on the latest Fabric v2.2.1 image, you can upgrade your existing nodes to Fabric v2.x and the capabilities of your channels, allowing organizations to take advantage of the new smart contract lifecycle process.

For information about upgrading nodes, check out [Upgrading to a new version of Fabric](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern-components#ibp-console-govern-components-upgrade). For information about updating the capabilities of your channels, check out [Capabilities](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-govern#ibp-console-govern-capabilities).

### Support for Fabric v2.x smart contract lifecycle
{: #11-02-2020-lc}

The platform has been updated to include support for Fabric v2.x smart contract lifecycle process, which enables the distributed governance of smart contracts. Learn mode about how to [Deploy a smart contract using Fabric v2.x](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-smart-contracts-v2).

### Improvements for HSM support
{: #11-02-2020-hsm}

A new [process](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-build-docker) is available to configure an HSM for your blockchain nodes, delivering faster performance.

### Certificate renewal enhancements
{: #11-02-2020-cert-renew}

Customers can now use the console to renew certificates that have expired or are about to expire, including the Certificate Authority (CA) TLS certificate, peer and ordering node enrollment certificates, and peer and ordering node TLS certificates.

### Remove registered user from CA
{: #11-02-2020-delete-user}

You can now delete registered users from a CA.


