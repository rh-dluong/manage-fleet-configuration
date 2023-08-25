
# Note

1. This simple channel-subscription deploys payload to the hub cluster. In this case the payload is a bunch of [policies](https://github.com/bjoydeep/fleet-configuration/tree/main). All the policies have their placements set to whereever they are needed to be deployed.
1. Starting in 2.4 you need to be Subscription-Admin. One option is to execute: [community/CM-Configuration-Management/policy-configure-subscription-admin-hub](https://github.com/stolostron/policy-collection/blob/main/community/CM-Configuration-Management/policy-configure-subscription-admin-hub.yaml) from the command-line and set it to enforce. Or follow the `oc edit clusterrolebinding` shown below.

## Steps

1. Log on to the cluster using oc login .

1. Enable subscription-admin for the user who just connected to the ACM hub. 

    Command:
    ```
    oc edit clusterrolebinding open-cluster-management:subscription-admin
    ```
    Add the following to the bottom of the clusterRoleBinding (the user here is kube:admin).:
    
    ```
    subjects:
    - apiGroup: rbac.authorization.k8s.io
    kind: User
    name: kube:admin
    ```  
1. Then run 3 the scripts:
    ```
    kubectl apply -f namespace.yaml
    kubectl apply -f channenl.yaml
    kubectl apply -f subscription.yaml
    ```
