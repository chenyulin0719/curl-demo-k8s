## Kubernates YAML explanation
1. Create a `Role` named __list-pods-role__ within the `default` namespace. Grant it permission of get/list pods. 
2. Create a `ServiceAccount` named __list-pods-sa__ within the `default` namespace.
3. Create a `RoleBinding` named __list-pods-role-binding__ within the `default` namespace.  Associate the __list-pods-role__ with the ServiceAccount __list-pods-sa__.
4. Create a `Pod` named __curl-pod__ with image `curlimages/curl` within `default` namespace and attach service account __list-pods-sa__. 

### Demo
1. kubectl apply -f curl-demo.yaml
2. kubectl exec -it curl-pod -- /bin/sh
3. curl -k -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" \
     https://kubernetes.default.svc/api/v1/namespaces/default/pods
4. exit
5. kubectl delete -f curl-demo.yaml

(Notes: This code was referenced from ChatGPT and tested in my MiniKube env.)