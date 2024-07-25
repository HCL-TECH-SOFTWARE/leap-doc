# Prepare a namespace {#helm_prepare_namespace .concept}

Namespaces are used to group and isolate resources in the Kubernetes cluster. Leap is a deployment in the cluster, and it is recommended to create a namespace, then scope related resources to the namespace. 

Once you have created your namespace, you must append the namespace argument (-n namespace)  in helm and kubectl commands to ensure the command is scoped to the namespace that was created for the Leap deployment.

For information about namespaces, see https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ 

Identify a name for your namespace and create it using the following syntax:

**On Kubernetes platforms:**

Kubectl

``` {#codeblock_btl_jh4_hzb}
# Command to create a namespace using kubectl 
# This example creates a namespace called "my-namespace" 
kubectl create ns my-namespace 
```

**OpenShift:**

For OpenShift, you must create a namespace with specific settings.

Use the following namespace definition and save it as namespace.yaml. You must replace my-namespace in the template with the name of the namespace you are using:

``` {#codeblock_gh3_nh4_hzb}
apiVersion: v1 
kind: Namespace 
metadata: 
  name: my-namespace 
  annotations: 
    openshift.io/sa.scc.mcs: "s0:c24,c4" 
    openshift.io/sa.scc.supplemental-groups: "1001/10000" 
    openshift.io/sa.scc.uid-range: "1000/10000" 
```

**OpenShift client:**

``` {#codeblock_bzk_qh4_hzb}
# Command to create namespace from template file 
oc apply -f namespace.yaml 
```

**Parent topic: **[Preparation](helm_preparation.md)

