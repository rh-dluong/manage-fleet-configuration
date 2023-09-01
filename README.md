
# Note

1. This simple subscription deploys payload to the hub cluster. -
    - In the first example - it is deployed to a regular ACM hub
    - In the second example - it is deplyed to a ACM hub at Global Level and that propagates it to the ACM hub that it manages (or lets call it the managed Hub).
    - In this case the payload is a bunch of [policies](https://github.com/bjoydeep/fleet-configuration/tree/main). 
    - All the policies have their placements set to whereever they are needed to be deployed.
1. Starting in 2.4 you need to be Subscription-Admin. One option is to execute: [community/CM-Configuration-Management/policy-configure-subscription-admin-hub](https://github.com/stolostron/policy-collection/blob/main/community/CM-Configuration-Management/policy-configure-subscription-admin-hub.yaml) from the command-line and set it to enforce. Or follow the `oc edit clusterrolebinding` shown below.
1. This accompanying [repository](https://github.com/bjoydeep/fleet-configuration/tree/main) is used.

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
### If deploying into regular ACM hub (or managed hub if being managed from Global Hub)

1. 
    ```
    kubectl apply -k deploy-to-acm-hub
    ```

    Note: The local placement syntax used in this example works even when self management is disabled in ACM hub.   

### If deploying into Global Hub
1. 
    ```
    kubectl apply -k deploy-to-global-hub
    ```

### I
