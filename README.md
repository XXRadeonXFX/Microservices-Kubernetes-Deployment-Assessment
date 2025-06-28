# 📦 Microservices Kubernetes Deployment Assessment

This project is a microservices-based application deployed to a Kubernetes cluster. It consists of 4 main services—**User**, **Product**, **Order**, and a central **Gateway Service**—each containerized with Docker and orchestrated using Kubernetes manifests.

---

## 🗂️ Folder Structure

```
Microservices-Task/
├── Microservices/
│   ├── gateway-service/
│   │   ├── app.js
│   │   ├── Dockerfile
│   │   └── package.json
│   ├── order-service/
│   ├── product-service/
│   └── user-service/
├── submission/
│   ├── deployments/          # Kubernetes Deployments
│   ├── ingress/              # Ingress rules (if applicable)
│   ├── screenshots/          # Screenshots for verification
│   └── services/             # Kubernetes Service YAMLs
├── LICENSE
└── README.md
```

---

## 🚀 Services Overview

| Service         | Port | Localhost URL               | Description           |
|-----------------|------|-----------------------------|------------------------|
| User Service     | 3000 | `http://localhost:3000`     | Manages user data      |
| Product Service  | 3001 | `http://localhost:3001`     | Handles product info   |
| Order Service    | 3002 | `http://localhost:3002`     | Manages order records  |
| Gateway Service  | 3003 | `http://localhost:3003`     | API gateway for all services |

---

## 🐳 Docker Build & Push Instructions

1. **Navigate to each service directory** (e.g. `gateway-service`, `user-service`, etc.)

2. **Build Docker image**:
   ```bash
   docker build -t xxradeonxfx/<service-name>:latest .
   ```

3. **Verify the image locally**:
   ```bash
   docker images
   ```

4. **Push to DockerHub** (ensure you're logged in):
   ```bash
   docker push xxradeonxfx/<service-name>:latest
   ```

> Replace `<service-name>` with one of:
> - `gateway-service`
> - `user-service`
> - `product-service`
> - `order-service`

---

## ☸️ Kubernetes Deployment Steps

> Ensure you're connected to your AKS or other Kubernetes cluster.

1. **Apply Deployments**:
   ```bash
   kubectl apply -f submission/deployments/
   ```

2. **Apply Services**:
   ```bash
   kubectl apply -f submission/services/
   ```

3. **Check pods & services**:
   ```bash
   kubectl get pods
   kubectl get svc
   ```

4. **Port-forward services** (open separate terminals for each):
   ```bash
   kubectl port-forward svc/user-service 3000:3000
   kubectl port-forward svc/product-service 3001:3001
   kubectl port-forward svc/order-service 3002:3002
   kubectl port-forward svc/gateway-service 3003:80
   ```

---

## 🌐 Gateway & Microservices Testing

Once port-forwarded, test all services via these endpoints:

| Endpoint                             | Function                |
| ------------------------------------ | ----------------------- |
| `http://localhost:3000/users`        | User service users list |
| `http://localhost:3001/products`     | Product service items   |
| `http://localhost:3002/orders`       | Order service list      |
| `http://localhost:3003/health`       | Gateway health check    |
| `http://localhost:3003/api/users`    | Users from gateway      |
| `http://localhost:3003/api/products` | Products from gateway   |
| `http://localhost:3003/api/orders`   | Orders from gateway     |

### Sample curl tests:

```bash
curl http://localhost:3003/health
curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders
```

---

## 🖼️ Screenshots

> Located in: `submission/screenshots/`

Contains proof of:
- Running pods
- Services
- Port-forwarding
- Successful curl/API outputs

---

## 🧹 Clean Up Resources

To remove all deployed Kubernetes resources:

```bash
kubectl delete -f submission/services/
kubectl delete -f submission/deployments/
kubectl delete -f submission/ingress/
```

---

## 👤 Author

- **👨‍💻 Name:** Prince Thakur
- **💼 Role:** DevOps / Data Engineer
- **📧 Contact:** [LinkedIn](https://www.linkedin.com/in/prince-thakur-9b6ba3274/)

---

## 📄 License

This project is licensed under the **MIT License**. See `LICENSE` file for details.
