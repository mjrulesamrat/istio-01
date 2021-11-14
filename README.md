# Istio Zero to One

Istio intro to setup and enabling diff features

## Istio Architecture

- Uses envoy proxies as sidecar containers in each pod
- Does service discovery with envoy and retires the kubernetes internal kube-proxy component
- Provides Ingress & Engress

- Data Plane - Sidecar Proxy
- Control Plane - Istio Main Process, Master Componenets

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

## HTTP

- Fault injections & Delayed Requests
- Timeouts & Circuit Breakers

## Security

- mTLS PeerAuthentications

## Monitoring

- Prometheus & Grafana
