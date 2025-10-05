# Polar - Aurelius Federal Platform Resource

## Overview

Polar is a registered resource in the Aurelius Federal Platform Resource Library. This document provides information about how Polar integrates with the platform and its capabilities for federal deployments.

## Resource Information

- **Name:** Polar Knowledge Graph Framework
- **Type:** Infrastructure Observability Service
- **Classification:** Open Source Software (OSS)
- **Maintained by:** Carnegie Mellon University Software Engineering Institute
- **Platform:** Aurelius Federal Platform
- **Distribution Statement:** [DISTRIBUTION STATEMENT A] Approved for public release and unlimited distribution

## Description

Polar is a knowledge graph framework designed to collect infrastructure data and load it into a graph database for comprehensive DevSecOps observability. It provides:

- **Modular Agent Architecture:** Extensible agents for different data sources (GitLab, Kubernetes, Jira, etc.)
- **Message-Oriented Design:** Pub/sub architecture using RabbitMQ with mutual TLS
- **Graph-Based Storage:** Neo4j backend for relationship-rich infrastructure data
- **Security-First:** Mutual TLS authentication and encrypted communications
- **Cloud-Native:** Kubernetes-ready with Helm chart deployments
- **Reproducible Builds:** Nix-based build system for deterministic artifacts

## Key Features for Federal Deployments

### Security & Compliance
- Mutual TLS (mTLS) authentication for all agent communications
- Certificate-based identity management
- Secure credential handling via environment variables
- Compliance-friendly separation of concerns between infrastructure and application operators

### Observability & Monitoring
- Real-time collection of infrastructure state
- Relationship mapping between CI/CD artifacts and infrastructure
- Audit trail capabilities through graph queries
- Integration with existing observability stacks

### Deployment Flexibility
- Kubernetes native with StatefulSets and Services
- Helm chart based deployments
- Support for air-gapped environments
- Nix-based containerization for reproducibility

## Agents Available

### GitLab Agent
- Collects CI/CD pipeline data
- Tracks repository changes and merge requests
- Maps deployment relationships

### Kubernetes Agent
- Observes cluster resources (Pods, Services, Deployments, etc.)
- Tracks resource relationships and ownership
- Monitors cluster state changes

### Jira Agent
- Integrates issue tracking with infrastructure
- Links tickets to deployments and changes
- Provides traceability for compliance

### Provenance Agent
- Tracks software supply chain
- Records artifact lineage
- Supports SLSA compliance

## Integration Points

### Required Infrastructure
- **Graph Database:** Neo4j (version 4.x or later)
- **Message Broker:** RabbitMQ with TLS support
- **Certificate Authority:** For mTLS certificate issuance
- **Container Runtime:** Kubernetes 1.20+ or Docker

### Network Requirements
- Secure connections to target systems (GitLab, Kubernetes APIs, etc.)
- Internal pub/sub broker access
- Graph database connectivity
- Certificate authority access for cert rotation

## Deployment Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                  Aurelius Federal Platform                   │
│                                                               │
│  ┌──────────────┐         ┌──────────────┐                  │
│  │   Observers  │────────▶│   Cassini    │                  │
│  │   (Agents)   │         │   (Broker)   │                  │
│  └──────────────┘         └──────────────┘                  │
│                                  │                            │
│                                  ▼                            │
│  ┌──────────────┐         ┌──────────────┐                  │
│  │  Consumers   │◀────────│   Message    │                  │
│  │              │         │    Queue     │                  │
│  └──────────────┘         └──────────────┘                  │
│         │                                                     │
│         ▼                                                     │
│  ┌──────────────┐                                           │
│  │    Neo4j     │                                           │
│  │  Graph DB    │                                           │
│  └──────────────┘                                           │
└─────────────────────────────────────────────────────────────┘
```

## Usage in Aurelius Federal Platform

### Getting Started
1. Clone the Polar repository
2. Review security and compliance requirements
3. Configure mTLS certificates for your environment
4. Deploy Neo4j and RabbitMQ infrastructure
5. Configure and deploy Polar agents
6. Verify connectivity and data collection

### Configuration
Polar agents are configured through environment variables and YAML configuration files. See the main [README.md](../../README.md) for detailed setup instructions.

### Resource Access
- **Repository:** https://github.com/AureliustechandTalentSolutions/Polar
- **Documentation:** [docs/](../)
- **Agent Configurations:** [src/agents/](../../src/agents/)
- **Deployment Manifests:** [src/deploy/](../../src/deploy/)

## Support and Maintenance

### Project Status
- **License:** MIT-style license (see license.txt)
- **Active Development:** Yes
- **Community Support:** GitHub Issues
- **Commercial Support:** Contact permission@sei.cmu.edu

### Version Information
- **Current Version:** See latest Git tag
- **Stability:** Production-ready
- **Update Frequency:** Active development with regular releases

## Compliance and Licensing

### Copyright
Copyright 2024 Carnegie Mellon University

### Distribution Statement
[DISTRIBUTION STATEMENT A] This material has been approved for public release and unlimited distribution. Please see Copyright notice for non-US Government use and distribution.

### License
Licensed under a MIT-style license. See license.txt or contact permission@sei.cmu.edu for full terms.

### Distribution Management
DM24-0470

### Third-Party Components
This Software includes and/or makes use of Third-Party Software each subject to its own license. See the repository for complete attribution.

## Related Resources

- [Polar Architecture Documentation](../architecture/polar-logical-architecture.md)
- [Polar OAM Model](../polar-oam.md)
- [DevOps Guide](../devops.md)
- [SEI Blog Article](https://insights.sei.cmu.edu/blog/polar-improving-devsecops-observability/)

## Contact Information

For questions about using Polar in the Aurelius Federal Platform:
- **Email:** permission@sei.cmu.edu
- **GitHub:** https://github.com/AureliustechandTalentSolutions/Polar/issues

---

*Last Updated: 2024*
*Resource Library Version: 1.0*
