# K8s_HPA


`kind create cluster --name=pavantest --config=kind-cluster-nodes.yml` 

`k apply -f metrics.yaml`

`k apply -f deploy.yaml`

`k get pods`

![image](https://github.com/user-attachments/assets/843a5833-4029-4dcc-b6fb-486768c81921)

`k get service`

![image](https://github.com/user-attachments/assets/ad52887a-5f60-4aa7-804e-e45e077d6779)

### Performing Autoscaling - 

`kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`

OR

`kubectl apply -f hpa.yaml`

`k get hpa`

![image](https://github.com/user-attachments/assets/7d9f3ff9-31d7-40da-aeb4-766666c6c69f)

---

### Simulate the Load test - 

`kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"`

![image](https://github.com/user-attachments/assets/c3999db7-f5e4-4b3c-b6e9-1f19fd61a2b2)

`k get hpa -w`

![image](https://github.com/user-attachments/assets/6292ffd9-a7bc-49a8-a640-377213e799f1)

`k get pods`

![image](https://github.com/user-attachments/assets/497ebd7e-c0a7-4295-bf1b-d863b6ed1efb)

---

### Stopping the Load test which decreases the CPU in turn brings down the pods - 

`k get hpa -w`

![image](https://github.com/user-attachments/assets/ed9324f0-0316-4756-a23c-4e904bc51ea1)

