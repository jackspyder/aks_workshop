# aks_workshop

Once docker-for-desktop is installed with kubernetes enabled we want to install the kubernetes dashboard.

we'll pull the deployment from the official repo. This step usually isn't required when using a managed service.

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml --record
```

next we need to setup a service account and role so we can access the dashboard.

```bash
kubectl apply -f setup/service-account.yaml --record
```
```bash
kubectl apply -f setup/sa-role-binding.yaml --record 
```

with this done we want to collect our token with the following command which we need to copy to login to the dashboard:
```bash
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```
and now we want to expose the dashboard with: kubectl proxy

dashboard URL:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

We must select token, and paste our token from one of the above steps.

