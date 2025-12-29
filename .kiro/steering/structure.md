# Project Structure

## Directory Layout

```
cert-manager-sync/
├── cmd/cert-manager-sync/     # Application entry point
├── internal/                  # Private application code
│   ├── metrics/              # Prometheus metrics implementation
│   └── types/                # Internal type definitions
├── pkg/                      # Public library code
│   ├── certmanagersync/      # Core operator logic
│   ├── state/                # Kubernetes client and state management
│   └── tlssecret/            # TLS certificate parsing and configuration
├── stores/                   # Certificate store implementations
│   ├── acm/                  # AWS Certificate Manager
│   ├── cloudflare/           # Cloudflare certificates
│   ├── digitalocean/         # DigitalOcean certificates
│   ├── filepath/             # File system storage
│   ├── gcpcm/                # Google Cloud Certificate Manager
│   ├── heroku/               # Heroku certificates
│   ├── incapsula/            # Incapsula WAF certificates
│   ├── threatx/              # ThreatX certificates
│   └── vault/                # HashiCorp Vault storage
├── deploy/cert-manager-sync/ # Helm chart for deployment
└── devops/docs/              # Documentation and diagrams
```

## Code Organization Patterns

### Package Responsibilities

- **cmd/**: Application entry points and main functions
- **internal/**: Private code not intended for external use
- **pkg/**: Public APIs that could be imported by other projects
- **stores/**: Pluggable certificate store implementations

### Interface Design

- All certificate stores implement the `RemoteStore` interface
- Each store package contains:
  - Main implementation file (e.g., `acm.go`)
  - Test file (e.g., `acm_test.go`)
  - Configuration parsing and validation

### Naming Conventions

- Package names are lowercase, single words when possible
- Store packages named after the service (e.g., `acm`, `vault`)
- Struct names use PascalCase (e.g., `ACMStore`, `VaultStore`)
- Interface names end with descriptive suffix (e.g., `RemoteStore`)

### Configuration Pattern

- Environment variables for operator-level configuration
- Kubernetes annotations for per-secret configuration
- Annotation keys follow pattern: `cert-manager-sync.lestak.sh/{store}-{setting}`

### Error Handling

- Use structured logging with logrus
- Return errors from functions, handle at appropriate level
- Create Kubernetes events for user-visible operations
- Implement exponential backoff for transient failures

### Testing Structure

- Test files alongside implementation files
- Use table-driven tests where appropriate
- Mock external dependencies for unit tests
