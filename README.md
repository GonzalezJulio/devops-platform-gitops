# DevOps Platform Cloud Metrics — Etapa 1

## 📌 Descripción

Proyecto práctico enfocado en la construcción de una plataforma cloud-native utilizando Kubernetes, GitOps y automatización de despliegues.

La primera etapa del proyecto se centró en construir una base sólida de infraestructura y despliegue declarativo utilizando Docker, Kubernetes y ArgoCD.

---

# 🚀 Objetivos de la Etapa 1

- Containerizar una aplicación Flask
- Implementar un clúster Kubernetes local con k3d/k3s
- Desplegar aplicaciones mediante Deployments y Services
- Implementar GitOps con ArgoCD
- Automatizar despliegues mediante sincronización con GitHub
- Realizar rolling updates sin downtime
- Comprender Desired State y Self-Healing

---

# 🏗️ Arquitectura

```text
GitHub
   ↓
ArgoCD
   ↓
Kubernetes Cluster (k3d/k3s)
   ↓
Deployment
   ↓
Pods
   ↓
Service (NodePort)
```

---

# 🧰 Tecnologías utilizadas

- Python / Flask
- Docker
- Docker Hub
- Kubernetes
- k3d / k3s
- ArgoCD
- GitHub
- GitOps

---

# 📂 Estructura del proyecto

```text
.
├── app
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── templates
│
├── gitops
│   ├── app
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── kustomization.yaml
│   │
│   └── argocd
│       └── application.yaml
│
├── k8s
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── namespace.yaml
│
├── monitoring
├── logging
├── diagrams
└── screenshots
```

---

# 🐳 Docker

## Construcción de imagen

```bash
docker build -t aresden113/devops-platform:v1 .
```

## Push a Docker Hub

```bash
docker push aresden113/devops-platform:v1
```

---

# ☸️ Kubernetes

## Crear namespace

```bash
kubectl apply -f k8s/namespace.yaml
```

## Deployment

La aplicación fue desplegada utilizando:

- múltiples réplicas
- rolling updates
- variables de entorno
- imágenes versionadas

## Service

Se utilizó un Service tipo NodePort para exponer la aplicación:

```yaml
type: NodePort
```

---

# 🔄 GitOps con ArgoCD

Se configuró ArgoCD para sincronizar automáticamente el estado del clúster con el repositorio GitHub.

## Flujo GitOps

```text
Git Push
   ↓
ArgoCD detecta cambios
   ↓
Kubernetes aplica nuevo estado
   ↓
Rolling Update automático
```

---

# 🔥 Rolling Update — v1 → v2

Durante la etapa se realizó una actualización completa de la aplicación:

- Construcción de nueva imagen Docker (`v2`)
- Push a Docker Hub
- Actualización declarativa del Deployment
- Sincronización automática mediante ArgoCD
- Reemplazo progresivo de Pods sin downtime

---

# ✅ Resultados obtenidos

- Aplicación containerizada y desplegada
- Cluster Kubernetes funcional
- GitOps operativo
- Despliegues automatizados
- Self-Healing habilitado
- Rolling Updates exitosos
- Arquitectura declarativa funcionando

---

# 📌 Próxima etapa

La Etapa 2 incluirá:

- Ingress + Traefik
- Prometheus
- Grafana
- Loki
- Promtail
- Observabilidad completa
- CI/CD con GitHub Actions

---

# 🚀 Etapa 2 — Observabilidad en Kubernetes

En esta etapa del laboratorio DevOps implementé un stack completo de observabilidad sobre Kubernetes utilizando herramientas Cloud Native del ecosistema CNCF.

El objetivo fue centralizar métricas y logs del cluster para comprender cómo funcionan los sistemas de monitoreo y observabilidad utilizados en entornos reales DevOps/SRE.

---

# 🔧 Stack implementado

* Kubernetes (k3d)
* Prometheus
* Grafana
* Loki
* Promtail

---

# 📊 Funcionalidades implementadas

✅ Recolección de métricas del cluster Kubernetes
✅ Dashboards personalizados en Grafana
✅ Monitoreo de CPU y memoria
✅ Estado de pods y reinicios de contenedores
✅ Centralización de logs con Loki
✅ Recolección de logs mediante Promtail
✅ Visualización integrada de métricas y logs

---

# 📈 Métricas monitoreadas

## Prometheus + Grafana

* Uso de CPU
* Uso de memoria
* Estado de Pods
* Reinicios de contenedores
* Métricas del cluster Kubernetes

---

# 📝 Logs centralizados con Loki

Se implementó integración completa entre Grafana y Loki para visualizar logs directamente desde dashboards y Explore.

Ejemplos:

* Logs del namespace monitoring
* Logs de Grafana
* Logs de Prometheus
* Logs de Loki y Promtail

---

# ⚠️ Problemas encontrados

Durante la integración entre Grafana y Loki aparecieron errores relacionados con:

* Conectividad entre servicios
* Resolución DNS interna
* Parsing de consultas LogQL
* Validación de endpoints Loki
* Configuración del datasource en Grafana

Error principal encontrado:

```text
Unable to connect with Loki.
parse error at line 1, col 1: syntax error: unexpected IDENTIFIER
```

---

# 🛠️ Troubleshooting realizado

Para resolver el problema se realizaron múltiples validaciones:

```bash
kubectl get pods -n monitoring
kubectl get svc -n monitoring
kubectl logs -n monitoring deploy/grafana
kubectl exec -it -n monitoring deploy/grafana -- sh
wget -qO- http://loki:3100/ready
```

También se validó:

* comunicación entre pods
* endpoints internos
* datasource Loki
* consultas LogQL
* estado de servicios Kubernetes

---

# ✅ Resultado final

Se logró integrar correctamente:

* Prometheus
* Grafana
* Loki
* Promtail

permitiendo visualizar métricas y logs centralizados desde Grafana en un entorno Kubernetes funcional.

---

# 📚 Aprendizajes obtenidos

* Observabilidad Cloud Native
* Monitoreo en Kubernetes
* Uso de PromQL
* Uso de LogQL
* Troubleshooting en Kubernetes
* Integración de herramientas CNCF
* Centralización de logs
* Dashboards de observabilidad

---

# 📌 Próximas etapas

* Alertas con Grafana/Alertmanager
* Métricas custom de aplicaciones
* GitOps observability
* Dashboards avanzados
* Exporters adicionales
* Tracing distribuido
* Monitoreo production-ready


# 👨‍💻 Autor

Julio González

## 🔗 Repositorio

https://github.com/GonzalezJulio/devops-platform-gitops