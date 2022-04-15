---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-01"

keywords: IBM Blockchain Platform console, deploy, resource requirements, storage, parameters, multicloud

subcollection: blockchain-sw-252

---

{{site.data.keyword.attribute-definition-list}}


# Deploying {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 for {{site.data.keyword.cloud_notm}} Private
{: #deploy-icp}

You can use the following instructions to deploy {{site.data.keyword.blockchainfull}} Platform 2.5.2 on IBM Cloud Private with a minimum fix pack level of 3.2.2.2008.

{{site.data.keyword.blockchainfull}} Platform 2.5.2 has been tested on IBM Cloud Private 3.2.2.2105, which contains Kubernetes v1.19. However, the minimum fix level for IBM Cloud Private (3.2.2.2008) contains an earlier version of  Kubernetes. Though IBM Blockchain Platform is functional with earlier versions of Kubernetes, they are no longer supported and may be missing fixes for identified vulnerabilities.
{: important}

{{site.data.keyword.blockchainfull_notm}} Platform uses a [Kubernetes Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/){: external} to install the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster and manage the deployment and your blockchain nodes. When the {{site.data.keyword.blockchainfull_notm}} Platform console is running on your cluster, you can use the console to create blockchain nodes and operate a multicloud blockchain network.
{: shortdesc}

Kubernetes does not download and update the latest version of {{site.data.keyword.blockchainfull_notm}} Platform automatically. To get the latest update, you need to create a new cluster and a new service instance.
{: note}

## Resources required
{: #deploy-icp-resources-required}

Ensure your Kubernetes cluster has sufficient resources for the {{site.data.keyword.blockchainfull_notm}} Platform console and for the blockchain nodes that you create. The amount of resources that are required can vary depending on your infrastructure, network design, and performance requirements. To help you deploy a cluster of the appropriate size, the default CPU, memory, and storage requirements for each component type are provided in this table. Your actual resource allocations are visible in your blockchain console when you deploy a node and can be adjusted at deployment time or after deployment according to your business needs.

The resources for the CA, peer, and ordering nodes need to be multiplied by the number of these nodes that you require. The operator and console resources are per blockchain deployment. For example, if you deployed development, staging, and test networks in a single cluster, you need to have enough resources for three instances of the operator and console, one for each blockchain deployment. On the other hand, the webhook resources are per Kubernetes cluster, only one instance is required, regardless of the number of blockchain networks in the cluster.

| **Component** (all containers) | CPU**  | Memory (GB) | Storage (GB) |
|--------------------------------|---------------|-----------------------|------------------------|
| **Peer (Hyperledger Fabric v1.4)**                       | 1.1           | 2.8                   | 200 (includes 100GB for peer and 100GB for state database)|
| **Peer (Hyperledger Fabric v2.x)**                       | 0.7           | 2.0                   | 200 (includes 100GB for peer and 100GB for state database)|
| **CA**                         | 0.1           | 0.2                   | 20                     |
| **Ordering node**              | 0.35          | 0.7                   | 100                    |
| **Operator**                   | 0.1           | 0.2                   | 0                      |
| **Console**                    | 1.2           | 2.4                   | 10                     |
| **Webhook**                    | 0.1           | 0.2                   | 0                      |
{: caption="Table 1. Default resource allocations" caption-side="bottom"}

** These values can vary slightly. Actual VPC allocations are visible in the blockchain console when a node is deployed.

Note that when smart contracts are installed on peers that run a Fabric v2.x image, the smart contract is launched in its own pod instead of a separate container on the peer, which accounts for the smaller amount of resources required on the peer.

## Browsers
{: #deploy-icp-browsers}
The {{site.data.keyword.blockchainfull_notm}} Platform console has been successfully tested on the following browsers:

- Chrome Version 91.0.4472.114 (Official Build) (64-bit)
- Safari Version 14.1.1 (16611.2.7.1.4)

## Storage
{: #deploy-icp-storage}

In addition to a small amount of storage (10 GB) required by the {{site.data.keyword.blockchainfull_notm}} console, persistent storage is required for each CA, peer, and ordering node that you deploy. Because blockchain components do not use the Kubernetes node local storage, network-attached remote storage is required so that blockchain nodes can fail over to a different Kubernetes worker node in the event of a node outage.  And because you cannot change your storage type after deploying peer, CA, or ordering nodes, you need to decide the type of persistent storage that you want to use _before_ you deploy any blockchain nodes.

The {{site.data.keyword.blockchainfull_notm}} Platform console uses dynamic provisioning to allocate storage for each blockchain node that you deploy by using a pre-defined storage class. You can choose your persistent storage from the available Kubernetes storage options.

If the storage includes support for the `volumeBindingMode: WaitForFirstCustomer` setting, you should configure it to delay volume binding until the pod is scheduled. Read more in the [Kubernetes Storage Classes documentation](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode){: external}.
{: tip}

Before you deploy the {{site.data.keyword.blockchainfull_notm}} Platform, you must create a storage class with enough backing storage for the {{site.data.keyword.blockchainfull_notm}} console and the nodes that you create. You can set this storage class to use the default storage class of your Kubernetes cluster or create a new class that is used by the {{site.data.keyword.blockchainfull_notm}} Platform console. If you are using a multizone cluster in {{site.data.keyword.cloud_notm}} and you change the default storage class definition, then you must configure the default storage class for each zone.  
After you create the storage class, run the following command to set the storage class of the multizone region to be the default storage class:
```
kubectl patch storageclass
```
{: codeblock}

If you prefer not to choose a persistent storage option, the default storage class of your namespace or OpenShift project is used. `Host-local` volume storage is not supported.
{: note}


### Considerations when choosing your persistent storage
{: ibp-storage-considerations}

| **Consideration** | **Recommendations** |
|---------------|------|
| **Type** | Fabric supports three types of storage for your nodes: File, Block, and Portworx.  All three types support snapshots, which are important for backups and disaster recovery. Portworx is also useful when you have multiple zones in your cluster. Object storage is not supported by Fabric but can be used for backups. |
| **Performance**| When you choose your storage, you need to factor in the read/write speed (IOPS/GB). {{site.data.keyword.blockchainfull_notm}} Platform suggests at least 2 IOPS/GB for a development or test environment and 4 IOPS/GB for production networks. Your results may vary depending on your use case and how your client application is written. |
| **Scalability **| When a node runs out of storage, it ceases to operate. Even if Kubernetes attempts to redeploy the node elsewhere, when the storage is full, the node cannot operate. Because the ledger is immutable and can only grow over time, expandable storage is nice to have for blockchain networks whenever available. At some point, you will run out of storage on your peers and ordering nodes and expandable storage helps to avoid this situation. If the storage is not expandable, when a peer or ordering runs out of storage, you need to provision a new node with a larger storage capacity and then delete the old one. When the new node is deployed, it must replicate the ledger, which can take time depending on the depth of the block history. |
| **Monitoring** | It's critical to monitor the storage consumption by your nodes. Consider the scenario where you deploy five ordering nodes, all with the same amount of storage. They are all replicating the same ledgers so they will all run out of storage at approximately the same time and you will lose consensus, causing the network to stop functioning. Therefore, you might want to consider varying the storage across the nodes and monitoring it as the ledger grows to avoid this situation. Before storage is exhausted on a node, you can expand it or provision a new node. |
| **Encryption** | Fabric does not require storage to be encrypted but it is a best practice for Security. You need to decide whether encryption is important for your business. If you have the option of encrypting the persistent volume, there may be some performance implications with encryption to consider.  |
| **High Availability (HA)** | There should be redundancy in the storage to avoid a single point of failure. |
| **Multi-zone capable storage** | {{site.data.keyword.cloud_notm}} includes the ability to create a single Kubernetes cluster across multiple data centers or "zones". Portworx offers multi-zone capable storage that can be used to potentially reduce the number of peers required. Consider a scenario where you build two zones with two peers for redundancy, one zone can go down and you still have two peers up in another zone. With multi-zone capable storage, you could instead have two zones with one peer each. If one zone goes down, the peer comes up in the other zone with its storage intact, reducing the overall redundant peer requirements. |

## Filesystem permissions
{: #deploy-icp-fs-perm}

{{site.data.keyword.blockchainfull_notm}} Platform uses Kubernetes [init containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: externnal} to set the correct filesystem permissions for the mounted volumes. The init containers run as the root user. The volumes are mounted on the init container which then changes the owner of the mounted folder to be the non-root user of the container that will use it. Learn  more about [how to give non-root users write permission on the volume mount path](/docs/containers?topic=containers-nonroot){: external}.

## Get your entitlement key
{: #deploy-icp-k8-entitlement-key}

When you purchase the {{site.data.keyword.blockchainfull_notm}} Platform from PPA, you receive an entitlement key for the software is associated with your MyIBM account. You need to access and save this key to deploy the platform.

1. Log in to [MyIBM Container Software Library](https://myibm.ibm.com/products-services/containerlibrary){: external} with the IBMid and password that are associated with the entitled software.

2. In the Entitlement keys section, select **Copy key** to copy the entitlement key to the clipboard. Save this value for use later during deployment.

## Before you begin
{: #deploy-icp-k8-prerequisites}

1. The {{site.data.keyword.blockchainfull_notm}} Platform can be installed only on the [Supported Platforms](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-ocp-about#console-ocp-about-prerequisites){: external}.

2. You cannot deploy an {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x and 2.5.x instance to the same cluster. If you need to run both instances of the product, then they must be running in separate clusters.

3. You need to install and connect to your cluster by using the [kubectl CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl){: external} to deploy the platform.

4. If you have a Hardware Security Module (HSM) that you plan to use to generate and store the private key for your CA, peer, or ordering nodes, you need to create an HSM client image and push it to your container registry. Follow instructions in the [advanced deployment](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-build-docker) topic to build the image.

**Looking for a way to script the deployment of the service?** Check out the [Ansible playbooks](/docs/blockchain-sw-252?topic=blockchain-sw-252-ansible), a powerful tool for scripting the deployment of components in your blockchain network. If you prefer a manual installation, proceed to the next section.

## Log in to your cluster
{: #deploy-icp-k8-login}

Before you can complete the next steps, you need to log in to your {{site.data.keyword.cloud_notm}} Private cluster and select the target namespace of your deployment..
```
cloudctl login -a https://<cluster_CA_domain>:8443 --skip-ssl-validation
```
{: codeblock}

Log in to the docker image registry for your cluster:

```
docker login <cluster_CA_domain>:8500
```
{: codeblock}

## Add security and access policies
{: #deploy-icp-k8-scc}

The {{site.data.keyword.blockchainfull_notm}} Platform requires specific security and access policies to be added to your namespace. The contents of a set of `.yaml` files are provided here for you to copy and edit to define the security policies. You must save these files to your local system and then add them your namespace by using the kubectl CLI. These steps need to be completed by a cluster administrator. Also, be aware that the peer `init` and `dind` containers that get deployed are required to run in privileged mode.

## Create the `ibpinfra` namespace for the webhook
{: #deploy-icp-k8-ibpinfra}

Because the platform has updated the internal apiversion from `v1alpha1` in previous versions to `v1beta1`, a Kubernetes conversion webhook is required to update the CA, peer, operator, and console to the new API version. This webhook will continue to be used in the future, so new deployments of the platform are required to deploy it as well.  The webhook is deployed to its own namespace, referred to as  `ibpinfra` throughout these instructions.

After you log in to your cluster, you can create the new `ibpinfra` namespace for the Kubernetes conversion webhook using the kubectl CLI. The new namespace needs to be created by a cluster administrator.

Run the following command to create the namespace.
```
kubectl create namespace ibpinfra
```
{: codeblock}

## Create a new namespace for your {{site.data.keyword.blockchainfull_notm}} Platform deployment
{: #deploy-icp-k8-namespace}

Next, you need to create a second project for your deployment of {{site.data.keyword.blockchainfull_notm}} Platform. You can create a namespace by using the kubectl CLI. The namespace needs to be created by a cluster administrator.

If you are using the CLI, create a new namespace by running the following command:
```
kubectl create namespace <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name you want to use for your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

It is required that you create a namespace for each blockchain network that you deploy with the {{site.data.keyword.blockchainfull_notm}} Platform. For example, if you plan to create different networks for development, staging, and production, then you need to create a unique namespace for each environment. Using a separate namespace provides each network with separate resources and allows you to set unique access policies for each network. You need to follow these deployment instructions to deploy a separate operator and console for each namespace.
{: important}

You can also use the CLI to find the available storage classes for your namespace. If you created a new storage class for your deployment, that storage class must be visible in the output in the following command:
```
kubectl get storageclasses
```
{: codeblock}

If you are not using the default storage class, additional configuration is required. See [Storage](/docs/blockchain-sw-252?topic=blockchain-sw-252-deploy-k8#deploy-k8-storage) for the considerations.

## Download and extract {{site.data.keyword.blockchainfull_notm}} Platform images
{: #deploy-icp-download-extract-images}

Extract and load the {{site.data.keyword.blockchainfull_notm}} Platform archive file into the docker registry.  

Use the following command to extract the images and load into the docker registry.
```
tar -xzvf IBM_BLOCKCHAIN_PF_F_IBM_CL.2.0.7.tar.gz amd64/ibp.tar.gz &&
tar -xzvf amd64/ibp.tar.gz &&
for file in images/*; do docker load < $file; done
```
{: codeblock}

**Note:** For s390 systems, substitute s390x for amd64.

## Tag the webhook image for the 'ibpinfra' namespace:
{: #deploy-icp-k8-tag-webhook-images-ibpinfra-namespace}

Execute the following command to tag the webhook image:
```
docker tag icr.io/cp/ibp-crdwebhook:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/ibpinfra/ibp-crdwebhook:2.5.2-20210713-amd64
```
{: codeblock}

## Tag the images image for the blockchain namespace:
{: #deploy-icp-k8-tag-images-ibp-namespace}

Execute the following command to tag the webhook image:
```
docker tag icr.io/cp/ibp-orderer:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-orderer:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-peer:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-peer:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-orderer:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-orderer:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-peer:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-peer:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-ca:1.5.0-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ca:1.5.0-20210713-amd64
docker tag icr.io/cp/ibp-couchdb:3.1.1-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-couchdb:3.1.1-20210713-amd64
docker tag icr.io/cp/ibp-chaincode-launcher:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-chaincode-launcher:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-javaenv:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-javaenv:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-nodeenv:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-nodeenv:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-goenv:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-goenv:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-utilities:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-utilities:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-ccenv:2.2.3-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ccenv:2.2.3-20210713-amd64
docker tag icr.io/cp/ibp-couchdb:2.3.1-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-couchdb:2.3.1-20210713-amd64
docker tag icr.io/cp/ibp-javaenv:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-javaenv:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-nodeenv:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-nodeenv:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-goenv:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-goenv:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-dind:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-dind:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-utilities:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-utilities:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-ccenv:1.4.12-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ccenv:1.4.12-20210713-amd64
docker tag icr.io/cp/ibp-enroller:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-enroller:2.5.2-20210713-amd64
docker tag icr.io/cp/ibp-init:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-init:2.5.2-20210713-amd64
docker tag icr.io/cp/ibp-fluentd:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-fluentd:2.5.2-20210713-amd64
docker tag icr.io/cp/ibp-grpcweb:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-grpcweb:2.5.2-20210713-amd64
docker tag icr.io/cp/ibp-console:2.5.2-20210810-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-console:2.5.2-20210810-amd64
docker tag icr.io/cp/ibp-deployer:2.5.2-20210713-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-deployer:2.5.2-20210713-amd64
docker tag icr.io/cp/ibp-operator:2.5.2-20210810-amd64 <cluster_CA_domain>:8500/<NAMESPACE>/ibp-operator:2.5.2-20210810-amd64
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

## Push the webhook image to the `ibpinfra` namespace
{: #deploy-icp-k8-push-webhook-images-ibpinfra-namespace}

Execute the following command to push the webhook image to the private image repository:
```
docker push <cluster_CA_domain>:8500/ibpinfra/ibp-crdwebhook:2.5.2-20210713-amd64
```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with the domain you use to log in to your {{site.data.keyword.cloud_notm}} Private cluster.

## Push the {{site.data.keyword.blockchainfull_notm}}  images to the blockchain namespace
{: #deploy-icp-k8-push-images-ibp-namespace}

Execute the following command to push the blockchain images to the private image repository:
```
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-orderer:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-peer:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-orderer:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-peer:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ca:1.5.0-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-couchdb:3.1.1-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-chaincode-launcher:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-javaenv:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-nodeenv:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-goenv:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-utilities:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ccenv:2.2.3-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-couchdb:2.3.1-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-javaenv:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-nodeenv:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-goenv:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-dind:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-utilities:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-ccenv:1.4.12-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-enroller:2.5.2-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-init:2.5.2-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-fluentd:2.5.2-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-grpcweb:2.5.2-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-console:2.5.2-20210810-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-deployer:2.5.2-20210713-amd64
docker push <cluster_CA_domain>:8500/<NAMESPACE>/ibp-operator:2.5.2-20210810-amd64
```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with the domain you use to log in to your {{site.data.keyword.cloud_notm}}Private cluster.
- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

## Create a secret for your internal registry
{: #deploy-icp-k8-create-ibpinfra-secret-docker-registry}

Add credentials to the internal registry for the `ibpinfra` namespace. Run the following command to create the secret and add it to your `ibpinfra` namespace:
```
kubectl create secret docker-registry docker-key-secret --docker-server=<cluster_CA_domain>:8500 --docker-username=<USERNAME> --docker-password=<PASSWORD> --docker-email=<EMAIL> -n ibpinfra
```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with the domain you use to log in to your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<USERNAME>` with the admin username for your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<PASSWORD>` with the admin password for your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<EMAIL>` with your email address.

## Deploy the webhook and custom resource definitions (CRDS) to your Kubernetes cluster
{: #deploy-icp-k8s-webhook-crd}

Before you can upgrade an existing 2.1.x network to 2.5.x, or deploy a new instance of the platform to your Kubernetes cluster, you need to create the conversion webhook by completing the steps in this section. The webhook is deployed to its own namespace or project, referred to `ibpinfra` throughout these instructions.

The first three steps are for deployment of the webhook. The last step is for the custom resource definitions for the CA, peer, orderer, and console components that the {{site.data.keyword.blockchainfull_notm}} Platform requires. You only have to deploy the webhook and custom resource definitions **once per cluster**. If you have already deployed this webhook and custom resource definitions to your cluster, you can skip these four steps below.
{: important}

### 1. Configure role-based access control (RBAC) for the webhook
{: #webhook-rbac}

First, copy the following text to a file on your local system and save the file as `rbac.yaml`. This step allows the webhook to read and create a TLS secret in its own project.

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: webhook
  namespace: ibpinfra
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: webhook
rules:
- apiGroups:
  - "*"
  resources:
  - secrets
  verbs:
  - "*"
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: ibpinfra
subjects:
- kind: ServiceAccount
  name: webhook
  namespace: ibpinfra
roleRef:
  kind: Role
  name: webhook
  apiGroup: rbac.authorization.k8s.io

```
{: codeblock}

Run the following command to add the file to your cluster definition:
```
kubectl apply -f rbac.yaml -n ibpinfra
```
{: codeblock}

When the command completes successfully, you should see something similar to:
```
serviceaccount/webhook created
role.rbac.authorization.k8s.io/webhook created
rolebinding.rbac.authorization.k8s.io/ibpinfra created
```
{: codeblock}

### 2.  Apply the Pod Security Policy
The IBM Blockchain Platform requires specific security and access policies to be added to the `ibpinfra` project.

Run the following commands to apply the pop security policy to the ibpinfra service account:
```
kubectl create role webhook-psp \
    --verb=use \
    --resource=podsecuritypolicy \
    --resource-name=ibm-blockchain-platform-psp -n ibpinfra

kubectl create rolebinding ibpinfra:webhook-psp \
    --role=webhook-psp \
    --serviceaccount=ibpinfra:webhook -n ibpinfra
```
{: codeblock}

If the commands are successful, you can see a response that is similar to the following example:
```
role.rbac.authorization.k8s.io/webhook-psp created
rolebinding.rbac.authorization.k8s.io/ibpinfra:webhook-psp created
```
{: codeblock}

### 3. Deploy the webhook
{: #webhook-deploy}

In order to deploy the webhook, you need to create two `.yaml` files and apply them to your Kubernetes cluster.

#### deployment.yaml
{: #webhook-deployment-yaml}

Copy the following text to a file on your local system and save the file as `deployment.yaml`. If you are deploying on OpenShift Container Platform on LinuxONE, you need to replace `amd64` with `s390x`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: "ibp-webhook"
  labels:
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp-webhook"
spec:
  replicas: 1
  selector:
    matchLabels:
      app.kubernetes.io/instance: "ibp-webhook"
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        helm.sh/chart: "ibm-ibp"
        app.kubernetes.io/name: "ibp"
        app.kubernetes.io/instance: "ibp-webhook"
      annotations:
        productName: "IBM Blockchain Platform"
        productID: "54283fa24f1a4e8589964e6e92626ec4"
        productVersion: "2.5.2"
    spec:
      serviceAccountName: webhook
      imagePullSecrets:
        - name: docker-key-secret
      hostIPC: false
      hostNetwork: false
      hostPID: false
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 2000
      containers:
        - name: "ibp-webhook"
          image: "<cluster_CA_domain>:8500/ibpinfra/ibp-crdwebhook:2.5.2-20210713-amd64"
          imagePullPolicy: Always
          securityContext:
            privileged: false
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            runAsNonRoot: true
            runAsUser: 1000
            capabilities:
              drop:
              - ALL
              add:
              - NET_BIND_SERVICE
          env:
            - name: "LICENSE"
              value: "accept"
            - name: NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: server
              containerPort: 3000
          livenessProbe:
            httpGet:
              path: /healthz
              port: server
              scheme: HTTPS
            initialDelaySeconds: 30
            timeoutSeconds: 5
            failureThreshold: 6
          readinessProbe:
            httpGet:
              path: /healthz
              port: server
              scheme: HTTPS
            initialDelaySeconds: 26
            timeoutSeconds: 5
            periodSeconds: 5
          resources:
            requests:
              cpu: 0.1
              memory: "100Mi"

```
{: codeblock}

Replace `<cluster_CA_domain>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

Run the following command to add the file to your cluster definition:
```
kubectl apply -n ibpinfra -f deployment.yaml
```
{: codeblock}

When the command completes successfully, you should see something similar to:
```
deployment.apps/ibp-webhook created
```
{: codeblock}

#### service.yaml
{: #webhook-service-yaml}

Second, copy the following text to a file on your local system and save the file as `service.yaml`.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: "ibp-webhook"
  labels:
    type: "webhook"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp-webhook"
    helm.sh/chart: "ibm-ibp"
spec:
  type: ClusterIP
  ports:
    - name: server
      port: 443
      targetPort: server
      protocol: TCP
  selector:
    app.kubernetes.io/instance: "ibp-webhook"

```
{: codeblock}

Run the following command to add the file to your cluster definition:
```
kubectl apply -n ibpinfra -f service.yaml
```
{: codeblock}

When the command completes successfully, you should see something similar to:
```
service/ibp-webhook created
```
{: codeblock}

### 4. Extract the certificate and create the custom resource definitions
{: #webhook-extract-cert}

1. Extract the webhook TLS certificate from the `ibpinfra` namespace by running the following command:
    ```
    TLS_CERT=$(kubectl get secret/webhook-tls-cert -n ibpinfra -o jsonpath={'.data.cert\.pem'})
    ```
    {: codeblock}

2. When you deploy the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.2 you need to apply the following four CRDs for the CA, peer, orderer, and console. If you are upgrading to 2.5.2, before you can update the operator, you need to update the CRDs to include a new `v1beta1` section as well as the webhook TLS certificate that you just stored in the `TLS_CERT` environment variable. In either case, run the following four commands to apply or update each CRD.

Run this command to update the CA CRD:   
```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: ibpcas.ibp.com
  labels:
    app.kubernetes.io/instance: ibpca
    app.kubernetes.io/managed-by: ibp-operator
    app.kubernetes.io/name: ibp
    helm.sh/chart: ibm-ibp
    release: operator
spec:
  conversion:
    strategy: Webhook
    webhook:
      clientConfig:
        caBundle: "${TLS_CERT}"
        service:
          name: ibp-webhook
          namespace: ibpinfra
          path: /crdconvert
      conversionReviewVersions:
      - v1beta1
      - v1alpha2
      - v1alpha1
  group: ibp.com
  names:
    kind: IBPCA
    listKind: IBPCAList
    plural: ibpcas
    singular: ibpca
  scope: Namespaced
  versions:
  - name: v1beta1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: true
    subresources:
      status: {}
  - name: v1alpha2
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
  - name: v210
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: false
    storage: false
    subresources:
      status: {}
  - name: v212
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: false
    storage: false
    subresources:
      status: {}
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
status:
  acceptedNames:
    kind: IBPCA
    listKind: IBPCAList
    plural: ibpcas
    singular: ibpca
  conditions: []
  storedVersions:
  - v1beta1
EOF
```
{: codeblock}

Depending on whether you are creating or updating the CRD, when successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibpcas.ibp.com created
```
{: codeblock}

or
```
customresourcedefinition.apiextensions.k8s.io/ibpcas.ibp.com configured
```
{: codeblock}

Run this command to update the peer CRD:
```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: ibppeers.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibppeer"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  conversion:
    strategy: Webhook
    webhook:
      clientConfig:
        caBundle: "${TLS_CERT}"
        service:
          name: ibp-webhook
          namespace: ibpinfra
          path: /crdconvert
      conversionReviewVersions:
      - v1beta1
      - v1alpha2
      - v1alpha1
  group: ibp.com
  names:
    kind: IBPPeer
    listKind: IBPPeerList
    plural: ibppeers
    singular: ibppeer
  scope: Namespaced
  versions:
  - name: v1beta1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: true
    subresources:
      status: {}
  - name: v1alpha2
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
status:
  acceptedNames:
    kind: IBPPeer
    listKind: IBPPeerList
    plural: ibppeers
    singular: ibppeer
  conditions: []
  storedVersions:
  - v1beta1
EOF
```
{: codeblock}

When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibppeers.ibp.com created
```
{: codeblock}

or
```
customresourcedefinition.apiextensions.k8s.io/ibppeers.ibp.com configured
```
{: codeblock}

Run this command to update the console CRD:
```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: ibpconsoles.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibpconsole"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  conversion:
    strategy: Webhook
    webhook:
      clientConfig:
        caBundle: "${TLS_CERT}"
        service:
          name: ibp-webhook
          namespace: ibpinfra
          path: /crdconvert
      conversionReviewVersions:
      - v1beta1
      - v1alpha2
      - v1alpha1
  group: ibp.com
  names:
    kind: IBPConsole
    listKind: IBPConsoleList
    plural: ibpconsoles
    singular: ibpconsole
  scope: Namespaced
  versions:
  - name: v1beta1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: true
    subresources:
      status: {}
  - name: v1alpha2
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
status:
  acceptedNames:
    kind: IBPConsole
    listKind: IBPConsoleList
    plural: ibpconsoles
    singular: ibpconsole
  conditions: []
  storedVersions:
  - v1beta1

EOF
```
{: codeblock}

When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibpconsoles.ibp.com created
```
{: codeblock}

or
```
customresourcedefinition.apiextensions.k8s.io/ibpconsoles.ibp.com configured
```
{: codeblock}

Run this command to update the orderer CRD:  
```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: ibporderers.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibporderer"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  conversion:
    strategy: Webhook
    webhook:
      clientConfig:
        caBundle: "${TLS_CERT}"
        service:
          name: ibp-webhook
          namespace: ibpinfra
          path: /crdconvert
      conversionReviewVersions:
      - v1beta1
      - v1alpha2
      - v1alpha1
  group: ibp.com
  names:
    kind: IBPOrderer
    listKind: IBPOrdererList
    plural: ibporderers
    singular: ibporderer
  scope: Namespaced
  versions:
  - name: v1beta1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: true
    subresources:
      status: {}
  - name: v1alpha2
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        x-kubernetes-preserve-unknown-fields: true
    served: true
    storage: false
    subresources:
      status: {}
status:
  acceptedNames:
    kind: IBPOrderer
    listKind: IBPOrdererList
    plural: ibporderers
    singular: ibporderer
  conditions: []
  storedVersions:
  - v1beta1
EOF
```
{: codeblock}

When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibporderers.ibp.com created
```
{: codeblock}

or
```
customresourcedefinition.apiextensions.k8s.io/ibporderers.ibp.com configured
```
{: codeblock}

## Create a secret for your internal registry
{: #deploy-icp-k8-create-docker-secret-ibp-namespace}

Add credentials to the internal registry for the blockchain namespace. Run the following command to create the secret and add it to your blockchain namespace:
```
kubectl create secret docker-registry docker-key-secret --docker-server=<cluster_CA_domain>:8500 --docker-username=<USERNAME> --docker-password=<PASSWORD> --docker-email=<EMAIL> -n <NAMESPACE>
```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with the domain you use to log in to your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<USERNAME>` with the admin username for your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<PASSWORD>` with the admin password for your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<EMAIL>` with your email address.
- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


### Apply the ClusterRole
{: #deploy-icp-k8-clusterrole}

Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. This file defines the required ClusterRole for the PodSecurityPolicy. Edit the file and replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: <NAMESPACE>
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp"
    app.kubernetes.io/managed-by: "ibp-operator"
rules:
- apiGroups:
  - extensions
  resourceNames:
  - ibm-blockchain-platform-psp
  resources:
  - podsecuritypolicies
  verbs:
  - use
- apiGroups:
  - "*"
  resources:
  - pods
  - pod/logs
  - services
  - endpoints
  - persistentvolumeclaims
  - persistentvolumes
  - events
  - configmaps
  - secrets
  - ingresses
  - roles
  - rolebindings
  - serviceaccounts
  - nodes
  - jobs
  verbs:
  - '*'
- apiGroups:
  - ""
  resources:
  - namespaces
  - nodes
  verbs:
  - 'get'
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - persistentvolumeclaims
  - persistentvolumes
  verbs:
  - '*'
- apiGroups:
  - ibp.com
  resources:
  - '*'
  - ibpservices
  - ibpcas
  - ibppeers
  - ibpfabproxies
  - ibporderers
  verbs:
  - '*'
- apiGroups:
  - ibp.com
  resources:
  - '*'
  verbs:
  - '*'
- apiGroups:
  - apps
  resources:
  - deployments
  - daemonsets
  - replicasets
  - statefulsets
  verbs:
  - '*'

```
{: codeblock}

After you save and edit the file, run the following commands.
```
kubectl apply -f ibp-clusterrole.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


### Apply the ClusterRoleBinding
{: #deploy-icp-k8-clusterrolebinding}

Copy the following text to a file on your local system and save the file as `ibp-clusterrolebinding.yaml`. This file defines the ClusterRoleBinding. Edit the file and replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.  

```yaml
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: <NAMESPACE>
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp"
    app.kubernetes.io/managed-by: "ibp-operator"
subjects:
- kind: ServiceAccount
  name: default
  namespace: <NAMESPACE>
roleRef:
  kind: ClusterRole
  name: <NAMESPACE>
  apiGroup: rbac.authorization.k8s.io

```
{: codeblock}

After you save and edit the file, run the following commands.
```
kubectl apply -f ibp-clusterrolebinding.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

### Create the role binding
{: #deploy-icp-k8-rolebinding}

After applying the policies, you must grant your service account the required level of permissions to deploy your console. Run the following command with the name of your target namespace:
```
kubectl -n <NAMESPACE> create rolebinding ibp-operator-rolebinding --clusterrole=<NAMESPACE> --group=system:serviceaccounts:<NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform operator
{: #deploy-icp-operator}

The {{site.data.keyword.blockchainfull_notm}} Platform uses an operator to install the {{site.data.keyword.blockchainfull_notm}} Platform console. You can deploy the operator on your cluster by adding a custom resource to your namespace by using the kubectl CLI. The custom resource pulls the operator image from the Docker registry and starts it on your cluster.  

Copy the following text to a file on your local system and save the file as `ibp-operator.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ibp-operator
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  replicas: 1
  strategy:
    type: "Recreate"
  selector:
    matchLabels:
      name: ibp-operator
  template:
    metadata:
      labels:
        name: ibp-operator
        release: "operator"
        helm.sh/chart: "ibm-ibp"
        app.kubernetes.io/name: "ibp"
        app.kubernetes.io/instance: "ibp"
        app.kubernetes.io/managed-by: "ibp-operator"  
      annotations:
        productName: "IBM Blockchain Platform"
        productID: "54283fa24f1a4e8589964e6e92626ec4"
        productVersion: "2.5.2"
        productChargedContainers: ""
        productMetric: "VIRTUAL_PROCESSOR_CORE"
    spec:
      hostIPC: false
      hostNetwork: false
      hostPID: false
      serviceAccountName: default
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: beta.kubernetes.io/arch
                operator: In
                values:
                - amd64
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
        fsGroup: 2000
      imagePullSecrets:
        - name: docker-key-secret
      containers:
        - name: ibp-operator
          image: <cluster_CA_domain>:8500/<NAMESPACE>/ibp-operator:2.5.2-20210810-amd64
          command:
          - ibp-operator
          imagePullPolicy: Always
          securityContext:
            privileged: false
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: false
            runAsNonRoot: false
            runAsUser: 1001
            capabilities:
              drop:
              - ALL
              add:
              - CHOWN
              - FOWNER
          livenessProbe:
            tcpSocket:
              port: 8383
            initialDelaySeconds: 10
            timeoutSeconds: 5
            failureThreshold: 5
          readinessProbe:
            tcpSocket:
              port: 8383
            initialDelaySeconds: 10
            timeoutSeconds: 5
            periodSeconds: 5
          env:
            - name: WATCH_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: OPERATOR_NAME
              value: "ibp-operator"
            - name: CLUSTERTYPE
              value: ICP
          resources:
            requests:
              cpu: 100m
              memory: 200Mi
            limits:
              cpu: 100m
              memory: 200Mi

```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with domain you use to log in to your {{site.data.keyword.cloud_notm}} Private cluster
- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

- If you changed the name of the Docker key secret, then you need to edit the field of `name: docker-key-secret`.

Then, use the kubectl CLI to add the custom resource to your namespace.

```
kubectl apply -f ibp-operator.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

You can confirm that the operator deployed by running the command `kubectl get deployment -n <NAMESPACE>`. If your operator deployment is successful, then you can see the following tables with four ones displayed. The operator takes about a minute to deploy.
```
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1     1            1           1m
```
{: codeblock}

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform console
{: #deploy-icp-console}

When the operator is running on your namespace, you can apply a custom resource to start the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster. You can then access the console from your browser. Note that you can deploy only one console per namespace.

Save the custom resource definition below as `ibp-console.yaml` on your local system.
```
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
  - amd64
  license:
    accept: true
  serviceAccountName: default
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: <cluster_CA_domain>:8500/<NAMESPACE>
  images:
    configtxlatorImage: ibp-utilities
    configtxlatorTag: 2.2.3-20210713
    consoleImage: ibp-console
    consoleInitImage: ibp-init
    consoleInitTag: 2.5.2-20210713
    consoleTag: 2.5.2-20210810
    couchdbImage: ibp-couchdb
    couchdbTag: 2.3.1-20210713
    deployerImage: ibp-deployer
    deployerTag: 2.5.2-20210713
  imagePullSecrets:
    - docker-key-secret
  networkinfo:
    domain: <DOMAIN>
    consolePort: <CONSOLE_PORT>
    proxyPort: <PROXY_PORT>
  storage:
    console:
      class: default
      size: 10Gi
  versions:
    ca:
      1.5.0-0:
        default: true
        image:
          caImage: ibp-ca
          caInitImage: ibp-init
          caInitTag: 2.5.2-20210713
          caTag: 1.5.0-20210713
          enrollerImage: ibp-enroller
          enrollerTag: 2.5.2-20210713
        version: 1.5.0-0
    orderer:
      1.4.12-0:
        default: true
        image:
          enrollerImage: ibp-enroller
          enrollerTag: 2.5.2-20210713
          grpcwebImage: ibp-grpcweb
          grpcwebTag: 2.5.2-20210713
          ordererImage: ibp-orderer
          ordererInitImage: ibp-init
          ordererInitTag: 2.5.2-20210713
          ordererTag: 1.4.12-20210713
        version: 1.4.12-0
      2.2.3-0:
        default: false
        image:
          enrollerImage: ibp-enroller
          enrollerTag: 2.5.2-20210713
          grpcwebImage: ibp-grpcweb
          grpcwebTag: 2.5.2-20210713
          ordererImage: ibp-orderer
          ordererInitImage: ibp-init
          ordererInitTag: 2.5.2-20210713
          ordererTag: 2.2.3-20210713
        version: 2.2.3-0
    peer:
      1.4.12-0:
        default: true
        image:
          couchdbImage: ibp-couchdb
          couchdbTag: 2.3.1-20210713
          dindImage: ibp-dind
          dindTag: 1.4.12-20210713
          enrollerImage: ibp-enroller
          enrollerTag: 2.5.2-20210713
          fluentdImage:ibp-fluentd
          fluentdTag: 2.5.2-20210713
          grpcwebImage: ibp-grpcweb
          grpcwebTag: 2.5.2-20210713
          goEnvImage: ibp-goenv
          goEnvTag: 1.4.12-20210713
          javaEnvImage: ibp-javaenv
          javaEnvTag: 1.4.12-20210713
          nodeEnvImage: ibp-nodeenv
          nodeEnvTag: 1.4.12-20210713
          peerImage: ibp-peer
          peerInitImage: ibp-init
          peerInitTag: 2.5.2-20210713
          peerTag: 1.4.12-20210713
        version: 1.4.12-0
      2.2.3-0:
        default: false
        image:
          builderImage:ibp-ccenv
          builderTag: 2.2.3-20210713
          chaincodeLauncherImage: ibp-chaincode-launcher
          chaincodeLauncherTag: 2.2.3-20210713
          couchdbImage: ibp-couchdb
          couchdbTag: 3.1.1-20210713
          enrollerImage: ibp-enroller
          enrollerTag: 2.5.2-20210713
          fluentdImage: ibp-fluentd
          fluentdTag: 2.5.2-20210713
          goEnvImage: ibp-goenv
          goEnvTag: 2.2.3-20210713
          grpcwebImage: ibp-grpcweb
          grpcwebTag: 2.5.2-20210713
          javaEnvImage: ibp-javaenv
          javaEnvTag: 2.2.3-20210713
          nodeEnvImage: ibp-nodeenv
          nodeEnvTag: 2.2.3-20210713
          peerImage: ibp-peer
          peerInitImage: ibp-init
          peerInitTag: 2.5.2-20210713
          peerTag: 2.2.3-20210713
        version: 2.2.3-0
```
{: codeblock}

- Replace `<cluster_CA_domain>:8500` with the domain you use to log in to your {{site.data.keyword.cloud_notm}} Private cluster.
- Replace `<DOMAIN>` with the Proxy IP address of your cluster.
- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

Accept the license:  

- Accept the [{{site.data.keyword.blockchainfull_notm}} Platform license](https://www-03.ibm.com/software/sla/sladb.nsf/lilookup/6CE1C5684689691C852586000043982B?OpenDocument){: external} by replacing the `license` parameter `accept: false` with the text `accept: true`.

Specify the external endpoint information of the console in the `ibp-console.yaml` file:
-  Replace <DOMAIN> with the Proxy IP address your cluster. You can retrieve the value of your Proxy IP address from the {{site.data.keyword.cloud_notm}} Private console. Note: You need to be a Cluster administrator to access your proxy IP. Log in to the {{site.data.keyword.cloud_notm}} Private cluster. In the left navigation panel, click Platform and then Nodes to view the nodes that are defined in the cluster. Click the node with the role proxy and then copy the value of the Host IP from the table.
- Replace <CONSOLE_PORT> with a number between 30000 and 32767. This port is used to access the Console UI from your browser.
-   Replace <PROXY_PORT> with a number between 30000 and 32767. Select a different port than the one you selected for your console port. This port is used by the console to communicate with your blockchain nodes.

If you are deploying on {{site.data.keyword.cloud_notm}} Private on LinuxONE (s390x), you need to replace the `arch` field in the `ibp_console.yaml` as follow:
```
arch:
- amd64
```
{: codeblock}

with:

```
arch:
- s390x
```
{: codeblock}

Provide the user name and password that is used to access the console for the first time:
- Replace `<EMAIL>` with the email address of the console administrator.
- Replace `<PASSWORD>` with the password of your choice. This password also becomes the default password of the console until it is changed.

You may need to make additional edits to the file depending on your choices in the deployment process:
- If you changed the name of your Docker key secret, change corresponding value of the `imagePullSecrets:` field.
- If you created a new storage class for your network, provide the storage class that you created to the `class:` field.

Because you can only run the following command once, you should review the [Advanced deployment options](#console-deploy-k8-advanced) in case any of the options are relevant to your configuration, before you install the console.  For example, if you are deploying your console on a multizone cluster, you need to configure that before you run the following step to install the console.
{: important}

After you update the file, you can use the CLI to install the console.
```
kubectl apply -f ibp-console.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace. Before you install the console, you might want to review the advanced deployment options in the next section. The console can take a few minutes to deploy.

### Advanced deployment options
{: #console-icp-deploy-k8-advanced}

Before you deploy the console, you can edit the `ibp-console.yaml` file to allocate more resources to your console or use zones for high availability in a multizone cluster. To take advantage of these deployment options, you can use the console resource definition with the `resources:` and `clusterdata:` sections added:

```yaml
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
  - amd64
  license:
    accept: false
  serviceAccountName: default
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: cp.icr.io/cp
  imagePullSecrets:
    - docker-key-secret
  networkinfo:
    domain: <DOMAIN>
  storage:
    console:
      class: ""
      size: 5Gi
  clusterdata:
    zones:
  resources:
    console:
      requests:
        cpu: 500m
        memory: 1000Mi
      limits:
        cpu: 500m
        memory: 1000Mi
    configtxlator:
      limits:
        cpu: 25m
        memory: 50Mi
      requests:
        cpu: 25m
        memory: 50Mi
    couchdb:
      limits:
        cpu: 500m
        memory: 1000Mi
      requests:
        cpu: 500m
        memory: 1000Mi
    deployer:
      limits:
        cpu: 100m
        memory: 200Mi
      requests:
        cpu: 100m
        memory: 200Mi
  version: 2.5.2

```
{: codeblock}

- You can use the `resources:` section to allocate more resources to your console. The values in the example file are the default values allocated to each container. Allocating more resources to your console allows you to operate a larger number of nodes or channels. You can allocate more resources to a currently running console by editing the resource file and applying it to your cluster. The console will restart and return to its previous state, allowing you to operate all of your exiting nodes and channels.

- If you plan to use the console with a multizone Kubernetes cluster, you need to add the zones to the `clusterdata.zones:` section of the file. When zones are provided to the deployment, you can select the zone that a node is deployed to using the console or the APIs. As an example, if you are deploying to a cluster across the zones of dal10, dal12, and dal13, you would add the zones to the file by using the format below.
    ```yaml
    clusterdata:
      zones:
        - dal10
        - dal12
        - dal13
    ```
    {: codeblock}

- Accept the [{{site.data.keyword.blockchainfull_notm}} Platform license](https://www-03.ibm.com/software/sla/sladb.nsf/lilookup/6CE1C5684689691C852586000043982B?OpenDocument){: external} by replacing the `license` parameter `accept: false` with the text `accept: true`.

When you finish editing the file, apply it to your cluster.
```
kubectl apply -f ibp-console.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

Unlike the resource allocation, you cannot add zones to a running network. If you have already deployed a console and used it to create nodes on your cluster, you will lose your previous work. After the console restarts, you need to deploy new nodes.s
{: important}

### Use your own TLS Certificates (Optional)
{: #deploy-icp-tls}

The {{site.data.keyword.blockchainfull_notm}} Platform console uses TLS certificates to secure the communication between the console and your blockchain nodes and between the console and your browser. You have the option of creating your own TLS certificates and providing them to the console by using a Kubernetes secret. If you skip this step, the console creates its own self-signed TLS certificates during deployment.

This step needs to be performed before the console is deployed.
{: important}

You can use a Certificate Authority or tool to create the TLS certificates for the console. The TLS certificate needs to include the hostname of the console and the proxy in the subject name or the alternative domain names. The console and proxy hostname are in the following format:

**Console hostname:** ``<NAMESPACE>-proxy:ip.<DOMAIN>``  
**Proxy hostname:** ``<NAMESPACE>-proxy:ip.<DOMAIN>``

- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.
- Replace `<DOMAIN>` with the name of your cluster domain.

Navigate to the TLS certificates that you plan to use on your local system. Name the TLS certificate `tlscert.pem` and the corresponding private key `tlskey.pem`. Run the following command to create the Kubernetes secret and add it to your Kubernetes namespace. The TLS certificate and key need to be in PEM format.
```
kubectl create secret generic console-tls-secret --from-file=tls.crt=./tlscert.pem --from-file=tls.key=./tlskey.pem -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

After you create the secret, add the `tlsSecretName` field to the `spec:` section of `ibp-console.yaml` with one indent added, at the same level as the `resources:` and `clusterdata:` sections of the advanced deployment options. You must provide the name of the TLS secret that you created to the field. The following example deploys a console with the TLS certificate and key stored in a secret named `"console-tls-secret"`. Replace `"<CONSOLE_TLS_SECRET_NAME>"` with `"console-tls-secret"` unless you used a different name for the secret.
```yaml
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
    - amd64
  license:
    accept: false
  serviceAccountName: default
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: cp.icr.io/cp
  imagePullSecrets:
    - docker-key-secret
    - ibm-entitlement-key
  networkinfo:
    domain: <DOMAIN>
  storage:
    console:
      class: default
      size: 10Gi
  tlsSecretName: "<CONSOLE_TLS_SECRET_NAME>"

```
{: codeblock}

Accept the license:  

- Accept the [{{site.data.keyword.blockchainfull_notm}} Platform license](https://www-03.ibm.com/software/sla/sladb.nsf/lilookup/6CE1C5684689691C852586000043982B?OpenDocument){: external} by replacing the `license` parameter `accept: false` with the text `accept: true`.

When you finish editing the file, you can apply it to your cluster in order to secure communications with your own TLS certificates:
```
kubectl apply -f ibp-console.yaml -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

### Verifying the console installation
{: #deploy-icp-verify}

You can confirm that the operator deployed by running the command `kubectl get deployment -n <NAMESPACE>`. If your console deployment is successful, you can see `ibpconsole` added to the deployment table, with four ones displayed. The console takes a few minutes to deploy. You might need to click refresh and wait for the table to be updated.
```
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1     1            1           10m
ibpconsole     1/1     1            1           4m
```
{: codeblock}

The console consists of four containers that are deployed inside a single pod:
- `optools`: The console UI.
- `deployer`: A tool that allows your console to communicate with your deployments.
- `configtxlator`: A tool used by the console to read and create channel updates.
- `couchdb`: An instance of CouchDB that stores the data from your console, including your authorization information.

If there is an issue with your deployment, you can view the logs from one of the containers inside the pod. First, run the following command to get the name of the console pod:
```
kubectl get pods -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

Then, use the following command to get the logs from one of the four containers listed above:
```
kubectl logs -f <pod_name> <container_name> -n <NAMESPACE>
```
{: codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

As an example, a command to get the logs from the UI container would look like the following example:
```
kubectl logs -f ibpconsole-55cf9db6cc-856nz optools -n blockchain-project
```
{: codeblock}

## Log in to the console
{: #deploy-icp-log-in}

You can access the console by browsing to the following URL:
```
https://<DOMAIN>:<CONSOLE_PORT>
```
{: codeblock}

- Replace `<DOMAIN>` with the value of the `domain:` field in the `ibp-console.yaml` file.
- Replace `<CONSOLE_PORT>` with the port you specified in the `consolePort:` in the `ibp-console.yaml` file.

Your console URL looks similar to the following example:
```
https://9.30.252.107:32615
```
{: codeblock}

If you navigate to the console URL in your browser, you can see the console login screen:
- For the **User ID**, use the value you provided for the `email:` field in the `ibp-console.yaml` file.
- For the **Password**, use the value you encoded for the `password:` field in the `ibp-console.yaml` file. This password becomes the default password for the console that all new users use to log in to the console. After you log in for the first time, you will be asked to provide a new password that you can use to log in to the console.

If you are unable to log in, ensure that you are not using the ESR version of Firefox. If you are, switch to another
browser such as Chrome and log in. Otherwise, clear your browser cache and try logging in again.
{: tip}

The administrator who provisions the console can grant access to other users and restrict the actions they can perform. For more information, see [Managing users from the console](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-icp-manage#console-icp-manage-users).

## Next steps
{: #deploy-icp-k8-next-steps}

When you access your console, you can view the **nodes** tab of your console UI. You can use this screen to deploy components on the cluster where you deployed the console. See the [Build a network tutorial](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-build-network#ibp-console-build-network) to get started with the console. You can also use this tab to operate nodes that are created on other clouds. For more information, see [Importing nodes](/docs/blockchain-sw-252?topic=blockchain-sw-252-ibp-console-import-nodes#ibp-console-import-nodes).

To learn how to manage the users that can access the console, view the logs of your console and your blockchain components, see [Administering your console](/docs/blockchain-sw-252?topic=blockchain-sw-252-console-icp-manage#console-icp-manage).  

Ready to automate the entire deployment process? Check out the [Ansible Playbook](/docs/blockchain-sw-252?topic=blockchain-sw-252-ansible-install-ibp) that can be used to complete all of the steps  in this topic for you.

## Docker in Docker considerations
{: #deploy-icp-docker-in-docker-considerations}

Kubernetes default values for IP addresses prevent conflicts between pods, services, and worker nodes. However, if IP address ranges are assigned during installation of Kubernetes, the potential for IP address conflicts exists. Therefore, if your Docker in Docker (dind) container is not reachable from the peer container, there may be an issue with the bridge IP address. To address this scenario, edit the `ibppeer` specification for the peer and add the bridge IP `-bip` argument to the `dind` container, as described below.

Take the following steps to allow the container to set the IP address and subnet for the Docker in Docker container:

Get the custom resource definition for all peers:

`kubectl get ibppeers -n <ibp namespace>`

Edit the custom resource definition for the peer to add default settings for the `dind` args:

`kubectl edit ibppeer <peername> -n <ibp namespace>`

Add the following `dindArgs` configuration under the `spec`. Change the `bip` argument to a IP address/subnet that does not conflict with other pods, services, or worker nodes:

`  
  spec:
    action:
      enroll: {}
      reenroll: {}
    configoverride: {}
    customNames:
      pvc: {}
    dindArgs:
    - --log-driver
    - fluentd
    - --log-opt
    - fluentd-address=localhost:9880
    - --mtu
    - "1400"
    - --bip
    - 172.22.1.1/16
`

This configuration change is not required if you are using Hyperledger Fabric 2.x peers, which do not use Docker in Docker containers. Using Fabric 2.x is the recommended resolution for this case, but the procedure can be used to resolve potential IP address conflicts in nodes running Hyperledger Fabric 1.4.x.
{: note}
