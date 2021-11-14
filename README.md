# Istio Zero to One

Istio intro to setup and enabling diff features

## Istio Architecture

- istiod is now a single process in the control plane
  - Pilot
  - Citadel
  - Galley

Main Functions of istiod:
  - Handle configurations
  - certificate distributions
  - sidecar injection

- Data Plane - Sidecar Proxy
- Control Plane - Istio Main Process, Master Componenets

* [Performance and Scalability](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#latency-for-istio-hahahugoshortcode-s3-hbhb)


## Istio Components

- istiod is a single control-plane process 
- istiod - distribute configuration, receive recorded network traffic, telemetry data, manage certificates
  - Pilot
  - Citadel
  - Galley

- Istio Envoy Proxies implement below features:
  - Service Discovery
  - Load Balancing
  - TLS Termination
  - Circuit Breaker
  - Health Checks
  - Canary Rollouts
  - Fault Injections (Chaos Engineering)
  - Rich Metrics 

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
