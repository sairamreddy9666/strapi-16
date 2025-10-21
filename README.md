## 🚀 **Task #16: Build a Kubernetes Cluster Locally with Minikube**

### 🎯 **Objective**

Deploy and manage applications on a **local Kubernetes cluster** using **Minikube**, **kubectl**, and **Docker**.

---

## 🧩 **Tools Required**

- **Docker**
    
- **kubectl**
    
- **Minikube**

<img width="598" height="336" alt="Screenshot 2025-10-21 075628" src="https://github.com/user-attachments/assets/3f7f5c0d-924d-450e-911f-624a261a00eb" />


---

## 🧰 **Step 1: Install Docker and Start the Docker**

### ✅ **Installation**

**For Linux**
```
yum install docker -y && systemctl start docker
```

## 🧰 **Step 2: Install Kubectl**

### ✅ **Installation**

(Choose your OS)

**For Linux**
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
mv kubectl /usr/local/bin/kubectl
```

## 🧰 **Step 3: Install Minikube and Start the Cluster**

### ✅ **Installation**

(Choose your OS)

**For Linux**
```
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

```
minikube start --driver=docker
minikube version
kubectl version
```

<img width="792" height="50" alt="Screenshot 2025-10-21 081252" src="https://github.com/user-attachments/assets/50edd7df-ea86-42a2-891a-f9ffb1376cd1" />


---

## 🧱 **Step 2: Create a Deployment**

Create a file named **`deployment.yaml`**

```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: cycle-container
          image: shaikmustafa/cycle
          ports:
            - containerPort: 80
```

Apply the Deployment
```
kubectl apply -f deployment.yaml
```

Verify Deployment
```
kubectl get deployments
kubectl get pods
```

Output:

<img width="826" height="101" alt="Screenshot 2025-10-21 082130" src="https://github.com/user-attachments/assets/2e46274d-66b7-4606-a8c3-c7a9841e9d92" />

---

## 🌐 **Step 3: Expose the App Using a Service**

Create a file named **`service.yaml`**
```
---
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

Apply the Service
```
kubectl apply -f service.yaml
```

Verify Service
```
kubectl get services
```

**Output:**

<img width="906" height="105" alt="Screenshot 2025-10-21 082521" src="https://github.com/user-attachments/assets/59b02b14-650a-4a34-94cf-4a68e3f5bc68" />


### Test the Service
```
minikube service myapp-service
```

🖥️ This will open your browser at something like `http://127.0.0.1:30008` showing the **default NGINX page**.
<img width="839" height="119" alt="Screenshot 2025-10-21 082705" src="https://github.com/user-attachments/assets/9df95e55-8d61-4e07-9a73-c938e77a4efa" />


---

## ⚙️ **Step 4: Scale the Deployment**

To scale from 2 → 4 replicas:
```
kubectl scale deployment myapp-deployment --replicas=4
```
### Check the pods:
```
kubectl get pods
```

**Output:**

<img width="873" height="117" alt="Screenshot 2025-10-21 091604" src="https://github.com/user-attachments/assets/63985fe3-4945-4992-a0d7-1522229cc8e2" />



---

## 🔍 **Step 5: Describe and View Logs**

### View Deployment Details
```
kubectl describe deployment myapp-deployment
```
<img width="915" height="418" alt="Screenshot 2025-10-21 091733" src="https://github.com/user-attachments/assets/2d65c252-4b25-4c38-820b-572e86bf915c" />

### View Pod Details
```
kubectl describe pod <pod-name>
```

### View Logs
```
kubectl logs <pod-name>
```
<img width="898" height="224" alt="Screenshot 2025-10-21 091949" src="https://github.com/user-attachments/assets/c0d3ab63-2582-4d17-8eb5-daa2c742693b" />


---
## 🧹 **Step 6: Clean Up**
```
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
minikube stop
```

---

## 🎓 **Outcome**

By completing this task, you will:  
✅ Understand Kubernetes architecture and workflow.  
✅ Create and manage Deployments and Services.  
✅ Scale applications easily.  
✅ Gain confidence using kubectl commands.

---
