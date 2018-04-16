# chirper-helm
Example lib for running the lagom chirper services on kubernetes via helm

This repo makes use of https://github.com/lagom/lagom-java-chirper-example - it assumes kubernetes is running 
and the docker images from the chirper example project have been published.

# Istio
This version uses the istio project to handle the routing layer of the lagom services, using the automatic sidecar injection approach, e.g it assumes minikube was started with a configuration like:

```
  minikube start \
    --memory 8192 \
    --cpus 4 \
    --profile localkube \
	--extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0
```

Hopefully, if all goes according to plan, after the pods become available, the following command should bring up the chirper frontend in a browser: 

`minikube service -n istio-system istio-ingress`
