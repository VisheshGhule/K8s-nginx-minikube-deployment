## Kubernetes with Minikube (Nginx Deployment)
---
### Quick checks. Confirm you have intsall below things.
```bash
docker --version
kubectl version --client --short
minikube version
```
<img width="400" height="150" alt="Screenshot from 2025-08-11 13-28-47" src="https://github.com/user-attachments/assets/79ee09f8-8074-45e6-a47e-49fb1a355c42" />

---

### Step 1: Start Minikube (use Docker driver)
- (Recommended: Docker driver because you already have Docker.)
```bash
minikube start --driver=docker
```
- Wait until it finishes. Verify:
```bash
minikube status
```
<img width="576" height="389" alt="Screenshot from 2025-08-11 13-41-08" src="https://github.com/user-attachments/assets/30c67fbf-c4d1-425e-a2af-8c97a0810a12" />

---

### Step 2: Apply it to k8s:
```bash
kubectl apply -f deployment.yaml
```
- Check if the pod is created:
```bash
kubectl get pods
```

- Apply the service:
```bash
kubectl apply -f service.yaml
```

- Check services:
```bash
kubectl get svc
```

- To access the app in browser:
```bash
minikube service nginx-service
```

<img width="485" height="303" alt="Screenshot from 2025-08-11 13-44-31" src="https://github.com/user-attachments/assets/dce36530-05f6-4826-8a9a-b8202fe37e88" />
<br> <br>
<img width="1000" height="205" alt="Screenshot from 2025-08-11 13-44-47" src="https://github.com/user-attachments/assets/41aa23c6-b039-42e2-9ef4-e02f435b22b6" />

---

### Step 3: Scale the Deployment
- Run the following command to scale Nginx to 3 replicas:
```bash
kubectl scale deployment nginx-deployment --replicas=3
```
- Verify pods:
```bash
kubectl get pods
```
(You should see 3 pods running.)
- Check if service is still accessible:
```bash
minikube service nginx-service
```
<img width="780" height="267" alt="Screenshot from 2025-08-11 13-46-44" src="https://github.com/user-attachments/assets/9a3d644b-298b-42d1-bd17-98fc1e70c5fb" />

---

### Step 4: Update the Nginx version
- Run:
```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.19.10
```
- Check the rollout status
```bash
kubectl rollout status deployment/nginx-deployment
```
- Verify the updated pods
```bash
kubectl get pods
```
<img width="700" height="290" alt="Screenshot from 2025-08-11 13-52-44" src="https://github.com/user-attachments/assets/7ad6dc58-ec34-4608-87f9-b78865c5190c" />
<br> <br>
<img width="900" height="500" alt="Screenshot from 2025-08-11 13-53-20" src="https://github.com/user-attachments/assets/f16f3bc1-232a-4021-883a-c9d7d4848e8b" />

---

### Step 5: Rollback to the previous version
- Run
```bash
kubectl rollout undo deployment/nginx-deployment
```
- Check rollout status
```bash
kubectl rollout status deployment/nginx-deployment
```
- Confirm pods are back to the old version
```bash
kubectl get pods
```
<img width="700" height="290" alt="Screenshot from 2025-08-11 13-55-59" src="https://github.com/user-attachments/assets/7475f096-8831-4c4c-9c34-b26dc0b185b6" />
<br> <br>
<img width="900" height="500" alt="Screenshot from 2025-08-11 13-56-10" src="https://github.com/user-attachments/assets/7ed3711b-6a5b-4d6d-a37c-62bdc5f59068" />

