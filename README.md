<img src="https://img.shields.io/badge/istio-learning-brightgreen?sanitize=true"> <img src="https://img.shields.io/badge/zero--to-one-blue?sanitize=true">

# Istio Zero to One

Istio intro to setup and enabling diff features

## Istio Architecture

- istiod is now a single process in the control plane (Runs as a deployment)
  - Pilot
  - Citadel
  - Galley

Main Functions of istiod:
  - Handle configurations
  - TLS certificate distributions at run-time
  - sidecar injection

- Data Plane
  - Sidecar Envoy Proxy
  - Any incoming or outgoing request from a pod will pass through these sidecars
  - These proxies control all the network communications between microservices

- Control Plane
  - Brain of the service-mesh
  - Istio Main Process, Master Componenet

* [Performance and Scalability](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#latency-for-istio-hahahugoshortcode-s3-hbhb)
  - For 70,000 all over requests/second in the cluster, istio adds ~2ms latency
  - Each dataplane requires ~100m CPU and ~40MB Memory
  - Control Place requires ~1CPU and ~1.5GB Memory (Example of - 1000 Microservices, 2000 sidecars)

## Istio Components

- istiod is a single control-plane process 
- istiod - distribute configuration, receive recorded network traffic, telemetry data, manage certificates
  - Pilot
  - Citadel
  - Galley
  - sidecar injector

- Istio Envoy Proxies implement below features:
  - Service Discovery
  - Routing, Load Balancing (Canary, Dark releases)
  - TLS Termination
  - Resilience: Timeout, Retries & Circuit Breaker
  - Health Checks
  - Fault Injections (Chaos Engineering)
  - Rich Metrics
  - mTLS certificates

### Pilot

- Uses Envoy's API to communicate and Configure them

### Citadel

- Local CA autority
- user authentication
- issues and rotates the certificate to each Envoy
- credenticals management
- manages mTLS

### Galley

- Configuration validations, parsing and ingestion of the yaml configurations -> istio service-mesh
- For every new configuration changes, galley ingest -> validate -> route to Next istio component

### Sidecar Injector

- Injects the envoy sidecar container into pods for enabled namespaces
- ```$ kubectl label namespace default istio-injection=enabled```

## Istio Installation

## Microservices Demo with Istio

## Enabling Distributed tracing

- Kiali Dasboard
- Jaeger UI
- Propogating headers

## Enabling Traffic Management

- Canary Deployments
- Virtual Services
- Destination Rules
- Gateways & Routes

## Load Balancing

- Automatic load balancing for Http, gRPC, WebSocket, and TCP traffic
- Fault injections & Delayed Requests (Chaos Engineering)
- Timeouts & Circuit Breakers

## Security

- Secure TLS communication between microservices
- mTLS PeerAuthentications Modes
- Automatic certificate rotation at proxy level

## Monitoring

- Prometheus & Grafana
