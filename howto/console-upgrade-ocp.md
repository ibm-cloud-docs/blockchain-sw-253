---

copyright:
  years: 2019, 2022
lastupdated: "2022-07-20"

keywords: OpenShift, IBM Blockchain Platform console, deploy, resource requirements, storage, parameters

subcollection: blockchain-sw-253

---

{{site.data.keyword.attribute-definition-list}}



# Upgrading your console and components
{: #upgrade-ocp}

Running a different version of IBM Blockchain Platform? Switch to version
<a href="/docs/blockchain-sw?topic=blockchain-sw-upgrade-ocp">2.1.2</a>,
<a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-ocp">2.1.3</a>,
<a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-upgrade-ocp">2.5</a>,
<a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-upgrade-ocp">2.5.1</a>,
<a href="/docs/blockchain-sw-252?topic=blockchain-sw-252-upgrade-ocp">2.5.2</a>.


You can upgrade the {{site.data.keyword.blockchainfull}} Platform without disrupting a running network. Because the platform is deployed by using a Kubernetes operator, you can pull the latest {{site.data.keyword.blockchainfull_notm}} Platform images from the {{site.data.keyword.IBM_notm}} Entitlement registry without having to reinstall the platform. You can use these instructions to upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3.
{: shortdesc}

## {{site.data.keyword.blockchainfull_notm}} Platform overview
{: #upgrade-ocp-platform-overview}

Use these instructions to upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from versions 2.5.2, 2.5.1, 2.5, 2.1.3, 2.1.2, 2.1.1, and 2.1.0. The table provides an overview of the current and past releases.

| Version | Release date | Image tags | New features |
|----|----|----|----|
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5.3](/docs/blockchain-sw-253?topic=blockchain-sw-253-whats-new#whats-new-05-03-2022) | 03 May 2022| **Console and tools** <ul><li>2.5.3-20220719-amd64</li><li>2.5.3-20220719-amd64</li><li>2.5.3-20220503-amd64</li><li>2.5.2-20210616-amd64</li><li>2.5.2-20210505-amd64</li><li>2.5.2-20210325-amd64</li></ul> **Fabric nodes** <ul><li>1.4.12-20210616</li></ul> **CouchDB** <ul> <li>3.1.2-20220503</li> <li>2.3.1-20210505</li><li>2.3.1-20210325</li> <li>3.1.1-20210505</li> <li>3.1.1-20210325</li> <li>3.1.2-20220503</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.12-12, 2.2.5-4, and 2.4.3-1</li></ul> **Improvements to the Console UI** <ul><li>Support for Fabric v2.x Lifecycle.</li><li>Upgrade CA, peer, and ordering nodes from Fabric v1.4 to Fabric v2.x.</li><li>Certificate renewal enhancements added to the console.</li><li>Support for new Fabric Gateway.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5.2](/docs/blockchain-sw-252?topic=blockchain-sw-252-whats-new#whats-new-03-29-2021) | 29 Mar 2021| **Console and tools** <ul><li>2.5.2-20210616-amd64</li><li>2.5.2-20210505-amd64</li><li>2.5.2-20210325-amd64</li></ul> **Fabric nodes** <ul><li>1.4.12-20210616</li><li>1.4.11-20210505</li><li>1.4.11-20210325</li></ul> **CouchDB** <ul> <li>2.3.1-20210505</li><li>2.3.1-20210325</li> <li>3.1.1-20210505</li> <li>3.1.1-20210325</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.12 and 2.2.4</li><li>Fabric version 1.4.11 and 2.2.2</li></ul> **Improvements to the Console UI** <ul><li>Support for Fabric v2.x Lifecycle.</li><li>Upgrade CA, peer, and ordering nodes from Fabric v1.4 to Fabric v2.x.</li><li>Certificate renewal enhancements added to the console.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5.1](/docs/blockchain-sw-251?topic=blockchain-sw-251-release-notes-saas-20#01-12-2021) | 12 Jan 2021| **Console and tools** <ul><li>2.5.1-20210112-amd64</li> <li>2.5.1-20201208-amd64</li> <li>2.5.1-20201119-amd64</li> <li>2.5.1-20201030-amd64</li></ul> **Fabric nodes** <ul><li>1.4.9-20210112-amd64</li><li>1.4.9-20201208-amd64</li> <li>1.4.9-20201119-amd64</li> <li>1.4.9-20201030-amd64</li><li>2.2.1-20210112-amd64</li><li>2.2.1-20201208-amd64</li><li>2.2.1-20201119-amd64</li><li>2.2.1-20201030-amd64</li></ul> **CouchDB** <ul> <li>2.3.1-20210112-amd64</li> <li>2.3.1-20201208-amd64</li>  <li>2.3.1-20201119-amd64</li><li>2.3.1-20201030-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.9 and 2.2.1</ul> <strong>Improvements to the Console UI</strong> <ul><li>Support for Fabric v2.x Lifecycle.</li><li>Upgrade CA, peer, and ordering nodes from Fabric v1.4 to Fabric v2.x.</li><li>Certificate renewal enhancements added to the console.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5](/docs/blockchain-sw-25?topic=blockchain-sw-25-release-notes-saas-20#08-25-2020){: external} | 9 Sept 2020| **Console and tools** <ul><li>2.5.0-20200825-amd64</li><li>2.5.0-20200714-amd64</li><li>2.5.0-20200618-amd64</li></ul> **Fabric nodes** <ul><li>1.4.7-20200825-amd64</li><li>1.4.7-20200714-amd64</li><li>1.4.7-20200618-amd64</li><li>2.1.1-20200825-amd64</li><li>2.1.1-20200714-amd64</li><li>2.1.1-20200618-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20200825-amd64</li><li>2.3.1-20200714-amd64</li><li>2.3.1-20200618-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.7 and 2.1.1</ul> <strong>Improvements to the Console UI</strong> <ul><li>Ability to select Fabric version when you deploy a new peer or ordering node.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.3](/docs/blockchain-sw-213?topic=blockchain-sw-213-whats-new#whats-new-03-24-2020){: external} | 24 March 2020| **Console and tools** <ul><li>2.1.3-20200520-amd64</li><li>2.1.3-20200416-amd64</li><li>2.1.3-20200324-amd64</li></ul> **Fabric nodes** <ul><li>1.4.6-20200520-amd64</li><li>1.4.6-20200416-amd64</li><li>1.4.6-20200324-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20200520-amd64</li><li>2.3.1-20200416-amd64</li><li>2.3.1-20200324-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.6</ul> <strong>Additional platforms</strong> <ul><li>Platform can be deployed on the OpenShift Container Platform 4.2 on LinuxONE (s390x)</ul> <strong>Improvements to the Console UI</strong> <ul><li>Hardware Security Module (HSM) support for node identities</li><li>Ability to override CA, peer, and ordering node configuration</li><li>Ability to add and remove Raft ordering nodes</li><li>Java smart contract instantiation</li><li>Updated create channel and create organization panels</ul> |
| <a href="/docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-12-17-2019">{{site.data.keyword.blockchainfull_notm}} Platform v2.1.2</a> <img src="../icons/launch-glyph.svg" alt="External link icon"> | 17 December 2019 | <strong>Console and tools</strong> <ul><li>2.1.2-20191217-amd64</li><li>2.1.2-20200213-amd64</li></ul> **Fabric nodes** <ul><li>1.4.4-20191217-amd64</li><li>1.4.4-20200213-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20191217-amd64</li><li>2.3.1-20200213-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.4</ul> <strong>Additional platforms</strong> <ul><li>Platform can be deployed on the OpenShift Container Platform 4.1 and 4.2</ul> <strong>Improvements to the Console UI</strong> <ul><li>Simplified component creation flows</li><li>Zone selection for ordering nodes</li><li>Add peer to a channel from Channels tab</li><li>Anchor peer during join</li><li>Export/Import all</ul> |
| <a href="/docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-11-08-2019">{{site.data.keyword.blockchainfull_notm}} Platform v2.1.1</a> <img src="../icons/launch-glyph.svg" alt="External link icon">| 8 November 2019 | <strong>Console and tools</strong> <ul><li>2.1.1-20191108-amd64</ul> <strong>Fabric nodes</strong> <ul><li>1.4.3-20191108-amd64</ul> <strong>CouchDB</strong> <ul><li>2.3.1-20191108-amd64</ul> | <strong>Additional platforms</strong> <ul><li>Platform can be deployed on Kubernetes v1.14 - v1.16</li><li>Platform can be deployed on {{site.data.keyword.cloud_notm}} Private 3.2.1</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.0](/docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-9-24-2019){: external} | 24 September 2019 | **Console and tools** <ul><li>2.1.0-20190918-amd64</ul> **Fabric nodes** <ul><li>1.4.3-20190918-amd64</ul> **CouchDB** <ul><li>2.3.1-20190918-amd64</ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.3</ul> **Additional platforms** <ul><li>Platform can be deployed on the OpenShift Container Platform 3.11</ul> |
{: caption="Table 1. {{site.data.keyword.blockchainfull_notm}} Platform versions" caption-side="bottom"}

## Before you begin
{: #upgrade-ocp-before}

The upgrade process that you follow depends on the version of the platform that you are upgrading from v2.1.x or v2.5.x.
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from v2.5.x](#upgrade-ocp-steps-253)
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from v2.1.x](#upgrade-ocp-steps-21x)  

Or, if you are upgrading from behind a firewall
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from v2.5.x](#upgrade-ocp-steps-253)
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from v2.1.x](#upgrade-ocp-firewall)

After you upgrade the {{site.data.keyword.blockchainfull_notm}} Platform operator, the operator will automatically upgrade the console that is deployed on your OpenShift project. You can then use the upgraded console to upgrade your blockchain nodes.

You can continue to submit transactions to your network while you are upgrading your network. However, you cannot use the console to deploy new nodes, deploy smart contracts, or create new channels during the upgrade process.

Updating the Operator triggers a restart of all components managed by this installation of the {{site.data.keyword.blockchainfull_notm}} Platform including Fabric nodes. To avoid disruption of service, a multiregion setup is recommended.
{: note}

It is a best practice to upgrade your SDK to the latest version as part of a general upgrade of your network. While the SDK will always be compatible with equivalent releases of Fabric and lower, it might be necessary to upgrade to the latest SDK to leverage the latest Fabric features. Also, after upgrading, it's possible your client application may experience errors. Consult the your Fabric SDK documentation for information about how to upgrade.
{: tip}

## Platform limitations
{: #upgrade-ocp-platform}

If your {{site.data.keyword.blockchainfull_notm}} Platform is running on OpenShift Container Platform 3.11, you cannot upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 unless you first upgrade your OpenShift cluster from 3.11 to 4.10. For more information, see [Upgrading your migration](https://docs.openshift.com/container-platform/4.10/migration_toolkit_for_containers/about-mtc.html).


## Upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from 2.5.x
{: #upgrade-ocp-steps-253}

When you upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from 2.5.x you need to update the webhook, the custom resource definitions (CRDs), the ClusterRole, and the operator using the following steps. **These same steps can be followed even if your deployment is behind a firewall.**

1. [Update webhook image.](#upgrade-ocp-steps-253-webhook)
2. [Update the CRDs.](#upgrade-ocp-steps-253-crds) (Not required when upgrading from 2.5.1)
3. [Update the ClusterRole.](#upgrade-ocp-steps-253-clusterrole) (Not required when upgrading from 2.5.1)
4. [Update the operator.](#upgrade-ocp-steps-253-operator)
5. [Use your console to upgrade your running blockchain nodes.](#upgrade-ocp-nodes)
6. [Update MSPs in consortium to add organization-level endorsement policy.](#upgrade-ocp-update-consortium)

You need to repeat steps 3-5 for each network that that runs on a separate project. If you experience any problems, see the instructions for [rolling back an upgrade](#upgrade-ocp-rollback). If you deployed your network behind a firewall, without access to the external internet, see the separate set of instructions for [Upgrading the {{site.data.keyword.blockchainfull_notm}} Platform behind a firewall](#upgrade-ocp-firewall).

### Step one: Update the webhook image
{: #upgrade-ocp-steps-253-webhook}

Log in to your cluster and run the following command to update the webhook image in the `ibpinfra` namespace or project:

```
kubectl set image deploy/ibp-webhook -n ibpinfra ibp-webhook="cp.icr.io/cp/ibp-crdwebhook:2.5.3-20220719-amd64"
```
{: codeblock}

If you are running the platform on LinuxONE, replace `-amd64` with `-s390x`.

### Step two: Update the CRDs
{: #upgrade-ocp-steps-253-crds}
**This step is not required when upgrading from 2.5.1.**

1. Extract the webhook TLS certificate from the `ibpinfra` namespace by running the following command:
    ```
    TLS_CERT=$(kubectl get secret/webhook-tls-cert -n ibpinfra -o jsonpath={'.data.cert\.pem'})
    ```
    {: codeblock}

2. When you deploy {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3, you need to apply the following four CRDs for the CA, peer, orderer, and console. If you are upgrading to 2.5.3, before you can update the operator, you need to update the CRDs to include a new `v1beta1` section as well as the webhook TLS certificate that you just stored in the `TLS_CERT` environment variable. In either case, run the following four commands to apply or update each CRD.

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

### Step three: Update the ClusterRole
{: #upgrade-ocp-steps-253-clusterrole}
**This step is not required when upgrading from 2.5.1.**

You need to update the ClusterRole that is applied to your project. Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: <PROJECT_NAME>
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp"
    app.kubernetes.io/managed-by: "ibp-operator"
rules:
  - apiGroups:
      - apiextensions.k8s.io
    resources:
      - persistentvolumeclaims
      - persistentvolumes
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - apiextensions.k8s.io
    resources:
      - customresourcedefinitions
    verbs:
      - get
  - apiGroups:
      - route.openshift.io
    resources:
      - routes
      - routes/custom-host
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - ""
    resources:
      - pods
      - pods/log
      - persistentvolumeclaims
      - persistentvolumes
      - services
      - endpoints
      - events
      - configmaps
      - secrets
      - nodes
      - serviceaccounts
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - "batch"
    resources:
      - jobs
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - "authorization.openshift.io"
      - "rbac.authorization.k8s.io"
    resources:
      - roles
      - rolebindings
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
      - bind
      - escalate
  - apiGroups:
      - ""
    resources:
      - namespaces
    verbs:
      - get
  - apiGroups:
      - apps
    resources:
      - deployments
      - daemonsets
      - replicasets
      - statefulsets
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - monitoring.coreos.com
    resources:
      - servicemonitors
    verbs:
      - get
      - create
  - apiGroups:
      - apps
    resourceNames:
      - ibp-operator
    resources:
      - deployments/finalizers
    verbs:
      - update
  - apiGroups:
      - ibp.com
    resources:
      - ibpcas.ibp.com
      - ibppeers.ibp.com
      - ibporderers.ibp.com
      - ibpconsoles.ibp.com
      - ibpcas
      - ibppeers
      - ibporderers
      - ibpconsoles
      - ibpcas/finalizers
      - ibppeers/finalizers
      - ibporderers/finalizers
      - ibpconsoles/finalizers
      - ibpcas/status
      - ibppeers/status
      - ibporderers/status
      - ibpconsoles/status
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
  - apiGroups:
      - extensions
      - networking.k8s.io
      - config.openshift.io
    resources:
      - ingresses
      - networkpolicies
    verbs:
      - get
      - list
      - create
      - update
      - patch
      - watch
      - delete
      - deletecollection
```
{: codeblock}

After you edit and save the file, run the following commands. Replace `<PROJECT_NAME>` with the name of your project.
```
oc apply -f ibp-clusterrole.yaml
oc adm policy add-scc-to-group <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{: codeblock}

### Step four: Upgrade the {{site.data.keyword.blockchainfull_notm}} operator
{: #upgrade-ocp-steps-253-operator}

Before updating the operator image, you need to stop the ibpconsole by running the following command. Replace <PROJECT_NAME> with the name of your project:
```
kubectl patch ibpconsole ibpconsole -n <PROJECT_NAME> -p='[{"op": "replace", "path":"/spec/replicas", "value":0}]' --type=json
```
{: codeblock}

Wait a few minutes for the console to stop.

While the console is stopped you are unable to deploy or manage your blockchain components.
{: note}

Run the following command to upgrade the operator. Replace <PROJECT_NAME> with the name of your project:

```
kubectl set image deploy/ibp-operator -n <PROJECT_NAME> ibp-operator="cp.icr.io/cp/ibp-operator:2.5.3-20220719-amd64"
```
{: codeblock}

After applying the new image to the operator deployment, the operator will restart and pull the latest image. The upgrade takes about a minute. While the upgrade is taking place, you can still access your console UI. However, you cannot use the console to deploy smart contracts, or use the console or the APIs to create or remove a node.

Run the command `kubectl get deployment ibp-operator -o yaml` command to confirm that the command updated the operator spec.

You can check that the upgrade is complete by running `kubectl get deployment`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
ibpconsole     1/1       1            1           4m
```
{: codeblock}

After the operator restarts, you can now restart the console by running the following command:

```
kubectl patch ibpconsole ibpconsole -n <PROJECT_NAME> -p='[{"op": "replace", "path":"/spec/replicas", "value":1}]' --type=json
```
{: codeblock}

### Step six: Upgrade your nodes

You can now follow the [steps](#upgrade-ocp-nodes) to upgrade your blockchain nodes. Be aware that after the nodes are upgraded, there is no way to roll back the upgrade from 2.5.3 to 2.5.x. After you upgrade to 2.5.3, you can take advantage of the new Fabric v2.x Lifecycle deployment process for your  smart contracts. But to avoid your peers crashing, you need to ensure that you upgrade your peers before you upgrade your channels. Learn more about considerations when [Upgrading to a new version of Fabric](/docs/blockchain-sw-253?topic=blockchain-sw-253-ibp-console-govern-components#ibp-console-govern-components-upgrade).

After you upgrade your nodes, you can [update the MSPs in your consortium to add organization-level endorsement policies](#upgrade-ocp-update-consortium).

### Step seven: Update MSPs in consortium to add organization-level endorsement policy
{: #upgrade-ocp-update-consortium}

To use the 2.x smart contract lifecycle, an organization must have an endorsement policy defined. If any organization in the consortium (the list of organizations maintained by the ordering service that are allowed to create channels) do not have an endorsement policy defined, a warning message will appear on the **Details** page of the ordering service with a list of organization MSPs that must be updated.

The best practice to add this endorsement policy to the MSP is to delete the MSP from the system channel and then re-add the MSP. The console detects the fact that the MSP does not contain the endorsement policy and automatically adds it. Note that this action can only be completed by an ordering service administrator. You do not need to delete and re-add the MSPs in the configuration of any application channels that have already been created. For these MSPs, the endorsement policy is added as part of the process of deploying the smart contract.

## Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from 2.1.x
{: #upgrade-ocp-steps-21x}

Installations prior to v2.5.0 must first be [upgraded to v2.5.1](https://cloud.ibm.com/docs/blockchain-sw-251?topic=blockchain-sw-251-upgrade-ocp), and then upgraded to v2.5.3.

## Upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.3 from 2.1.x from behind a firewall
{: #upgrade-ocp-firewall}

Installations prior to v2.5.0 must first be [upgraded to v2.5.1](https://cloud.ibm.com/docs/blockchain-sw-251?topic=blockchain-sw-251-upgrade-ocp#upgrade-ocp-firewall), and then upgraded to v2.5.3.

## Upgrade your blockchain nodes
{: #upgrade-ocp-nodes}

After you upgrade your console, you can use the console UI to upgrade the nodes of your blockchain network. Browse to the console UI and open the nodes overview tab. You can find the **Upgrade available** text on a node tile if there is an update available for the component. You can install this upgrade whenever you are ready. These upgrades are optional, but they are recommended. You cannot upgrade nodes that were imported into the console.

Apply upgrades to nodes one at a time. Your nodes are unavailable to process requests or transactions while the patch is being applied. Therefore, to avoid any disruption of service, you need to ensure that another node of the same type is available to process requests whenever possible. Installing upgrades on a node takes about a minute to complete and when it is complete, the node is ready to process requests.
{: important}

To upgrade a node, open the node tile and click the **Upgrade available** button. You cannot upgrade nodes that you imported to the console. Learn more about considerations when [Upgrading to a new version of Fabric](/docs/blockchain-sw-253?topic=blockchain-sw-253-ibp-console-govern-components#ibp-console-govern-components-upgrade).

## Roll back an upgrade
{: #upgrade-ocp-rollback}

When you upgrade your operator, the operator saves the secrets, deployment spec, and network information of your console before attempting to upgrade the console. If your upgrade fails for any reason, the {{site.data.keyword.IBM_notm}} Support can roll back your upgrade and restore your previous deployment by using the information on your cluster. If you need to roll back your upgrade, you can submit a support case from the [mysupport](https://www.ibm.com/support/pages/node/1072956){: external} page.

You can roll back an upgrade after you use the console to operate your network. However, after you use the console to upgrade your blockchain nodes, you can no longer roll back your console to a previous version of the platform.
