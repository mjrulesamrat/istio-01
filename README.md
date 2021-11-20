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

```bash
$ kubectl label namespace default istio-injection=enabled
```

## Istio Installation

1. istioctl install/istio operator

- Complete [Ref](https://istio.io/latest/docs/setup/getting-started/)
  ```bash
  $ curl -L https://istio.io/downloadIstio | sh -
  # Set path from the downloaded instructions
  $ export PATH=$PWD/bin:$PATH
  $ istioctl x precheck
  $ istioctl install --set profile=demo -y
  $ istioctl -h
  # Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later
  $ kubectl label namespace namespace_name istio-injection=enabled

  # check if istio is configured or not
  $ istioctl analyze

  # inject the istio by setting a namespace
  $ kubectl label namespace default istio-injection=enabled

  # explicitly disable for given namespace
  $ kubectl label namespace default istio-injection=disabled
  ```

3. istioctl manifest generate (optional)
4. Install using Helm (optional)

## Microservices Demo with Istio

Bookstore Demo provided by the Istio community is best example to get understanding of the functionality.
```bash
# use default demo application provided by the istio to test the setup
$ kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

Below command will enable all the addons mentioned here
```bash
$ ls samples/addons  # checkout the addons
$ kubectl apply -f samples/addons
```

## Enabling Distributed tracing

- Kiali Dasboard

```bash
$ kubectl rollout status deploy/kiali -n istio-system

# access kiali
$ istioctl dashboard kiali
```

- Jaeger UI
- Propogating headers

## Traffic Management

Istio Ingress(Gateway) bookinfo-gateway -> virtual-service -> product-page service -> review virtual-service -> review service -> rating service

### Load Balancing
- Gateways
  - Replaces the Ingress & Engress of kubernetes
- Virtual Services
  - http routes
  - To define & match the routes of the services
  - has routes and matches conditions for different label given to deployments
  - Gives more granular control for specific feature release to target audience
- Destination Rules
  - Add subset for given host/virtual-service
  - Adds one more layer of identification for the routing
  - Can add different deployments under one rule
  - Automatic load balancing for Http, gRPC, WebSocket, and TCP traffic
- Canary Deployments
  - destination rules injunction with the virtuals services can make this happen, even complex routing policies.

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
