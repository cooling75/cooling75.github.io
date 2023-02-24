# Use kubectl without 'sudo' 

***

Install using the correct flag solves the issue upfront:

```
curl -sfL https://get.k3s.io | sh -s - --write-kubeconfig-mode 644
```