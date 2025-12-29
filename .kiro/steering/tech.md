# Technology Stack

## Language & Runtime

- **Go 1.25.1**: Primary programming language
- **Kubernetes client-go**: For Kubernetes API interactions
- **Logrus**: Structured logging library

## Architecture

- **Kubernetes Operator Pattern**: Uses informers and event handlers
- **Interface-based design**: `RemoteStore` interface for pluggable certificate stores
- **Event-driven**: Responds to Kubernetes secret changes via informers

## Key Dependencies

- `k8s.io/client-go`: Kubernetes client library
- `k8s.io/api`: Kubernetes API types
- `github.com/prometheus/client_golang`: Metrics collection
- Cloud provider SDKs: AWS SDK, GCP client libraries, Cloudflare Go client
- `github.com/hashicorp/vault/api`: HashiCorp Vault integration
- `software.sslmate.com/src/go-pkcs12`: PKCS#12 certificate format support

## Build System

- **Make**: Build automation via `Makefile`
- **Docker**: Multi-stage builds with scratch base image
- **Helm**: Kubernetes deployment packaging

## Common Commands

### Development

```bash
# Run tests
make test

# Build binary
go build -o cert-manager-sync cmd/cert-manager-sync/*.go

# Run locally (requires KUBECONFIG)
./cert-manager-sync
```

### Testing

```bash
# Run all tests with verbose output
go test -v ./...

# Run vulnerability check
govulncheck -show verbose ./...

# Test specific package
go test -v ./pkg/certmanagersync
```

### Docker

```bash
# Build container image
docker build -t cert-manager-sync .

# Run container
docker run cert-manager-sync
```

### Deployment

```bash
# Deploy with Helm
helm upgrade --install -n cert-manager cert-manager-sync ./deploy/cert-manager-sync

# Deploy with custom values
helm upgrade --install -n cert-manager cert-manager-sync ./deploy/cert-manager-sync -f custom-values.yaml
```

## Configuration

- Environment variables for operator configuration
- Kubernetes annotations for certificate sync configuration
- Helm values for deployment customization
