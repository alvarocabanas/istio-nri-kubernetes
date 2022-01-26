# istio-nri-kubernetes

---

kubectl apply -f istio-init.yaml

---
kubectl apply -f minikube.yaml

Adds eggressGateway with:     
``` 
outboundTrafficPolicy:
    mode: REGISTRY_ONLY
```    
All outbound traffic will be disallowed.    

I had to add :
```
"excludeIPRanges": "172.17.0.0/16",
```
In order for the ksm component to scrape ksm, it's not a good solution.

---

kubectl create namespace newrelic
kubectl label namespace newrelic istio-injection=enabled
---
Install helm nri-kubernetes with webhook.enabled=false or it gets stuck

---
The integration won't be able to resolve the required api calls so applying this will solve it

kubectl apply -f egress-traffic.yaml

