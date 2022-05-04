# TTS
> Small spring project for TTS.

## Environment
- OS: macOS 12.1
- Frontend
  - IDE: VS Code
  - NodeJS: v17.5.0
  - Vue.js: 3
  - Chrome: Version 98.0.4758.109 (Official Build) (arm64)
  - Postman: 9.14.8
- Backend
  - IDE: IntelliJ
  - Java: 11.0.12
  - Maven: 3.8.4
  - Spring Boot: 2.6.4
  - Postgres: 14
- Deploy
  - Docker Desktop: 4.5.0
  - Kubernetes: v1.22.5
  - Istio: 1.13.1
    - The istio would be failed on the arm processor, so test by using the intel processor instead.
- Design diagram
  - diagrams.net
  
## Run
The project is running in the Docker Desktop and needs to enable the Kubernetes. Also the project uses `Istio` as service mesh framework.

### Install and Enable Istio
```
$ istioctl install --set profile=demo -y
$ kubectl label namespace default istio-injection=enabled
```

### Deploy micorservices with Istio
1. Deploy the database
```
$ cd ./k8s/db
$ kubectl apply -f .
```
2. Deploy the backend services
```
$ cd ./k8s/be
$ kubectl apply -f .
```
3. Deploy the frontend services with Istio load balancing
```
$ cd ./k8s/load_balancing
$ kubectl apply -f .
```

4. Deploy the frontend services with Istio traffic shifting
```
$ cd ./k8s/traffic_shifting
$ kubectl apply -f .
```