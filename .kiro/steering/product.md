# Product Overview

cert-manager-sync is a Kubernetes operator that enables automatic synchronization of TLS certificates from cert-manager to external certificate stores.

## Purpose

The operator solves the challenge of securely distributing TLS certificates managed by cert-manager to external services like AWS ACM, Cloudflare, HashiCorp Vault, and other certificate stores without manual intervention.

## Key Features

- **Multi-store support**: Syncs to 9+ certificate stores (AWS ACM, Cloudflare, DigitalOcean, GCP, Vault, Heroku, Incapsula, ThreatX, Filepath)
- **Annotation-driven configuration**: Uses Kubernetes annotations on TLS secrets to define sync destinations
- **Exponential backoff**: Implements retry logic with binary exponential backoff for failed syncs
- **Multiple destinations**: Can sync a single certificate to multiple stores simultaneously
- **Prometheus metrics**: Exposes sync status and metrics for monitoring
- **Event recording**: Creates Kubernetes events for sync operations

## Target Users

- DevOps engineers managing Kubernetes clusters with cert-manager
- Platform teams needing to distribute certificates to external services
- Organizations using hybrid cloud architectures requiring certificate synchronization
