# General Technical Review - Microcks / Incubation

- **Project:** Microcks
- **Project Version:** v1.x (current stable release)
- **Website:** https://microcks.io
- **Date Updated:** 2026-01-30
- **Template Version:** v1.0
- **Description:**  
  Microcks is an open source cloud-native tool for mocking and testing APIs and event-driven applications. It supports REST, gRPC, GraphQL, SOAP, and AsyncAPI-based services, enabling teams to shift API and contract testing left while supporting Kubernetes-native deployments.

---

## Day 0 - Planning Phase

### Scope

* **Roadmap process:**  
  The Microcks roadmap is driven by community input, maintainer discussions, GitHub issues, and user feedback. Scope for mid- and long-term features is discussed openly in the project repository and community channels, with prioritization based on user impact, maintainability, and alignment with cloud-native API lifecycle needs. Contributions map directly back to roadmap items through issues and pull requests.

* **Target personas:**  
  * API developers  
  * Platform and DevOps engineers  
  * QA and test engineers  
  * Platform engineering teams supporting API governance

* **Primary use case:**  
  Mocking, simulating, and testing APIs and asynchronous services based on contract definitions (OpenAPI, AsyncAPI, gRPC, GraphQL, SOAP).

* **Additional use cases:**  
  * Shift-left testing in CI/CD pipelines  
  * Consumer-driven contract testing  
  * Async and event-driven application simulation  
  * API prototyping and documentation validation

* **Unsupported use cases:**  
  * Acting as a production API gateway  
  * Long-term production traffic handling  
  * Stateful business logic execution

* **Intended adopters:**  
  Organizations building or operating API-driven or event-driven systems, including software vendors, financial services, telecoms, and platform engineering teams.

* **End user research:**  
  Feedback is primarily gathered through GitHub issues, community discussions, conference talks, and workshops. No formal published research reports are currently available.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation

---

### Usability

* **User interaction:**  
  Users interact with Microcks through:
  * A web-based UI
  * REST APIs
  * CI/CD integrations (e.g., Jenkins, GitHub Actions)

* **UX/UI:**  
  Microcks provides a web UI for managing API definitions, mocks, tests, and results. The UI is designed for ease of use by developers and testers, with visual feedback for test execution and service simulation.

* **Integration with other projects:**  
  Microcks integrates with Kubernetes, OpenShift, Keycloak (IAM), Kafka (async APIs), and CI/CD tools, enabling it to fit naturally into cloud-native delivery pipelines.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/usage

---

### Design

* **Design principles:**  
  * Cloud-native and Kubernetes-first  
  * Contract-first API design  
  * Secure by default  
  * Pluggable and extensible architecture

* **Architecture requirements:**  
  Microcks supports:
  * Local development (Docker Compose)
  * Kubernetes/OpenShift for test and production-like environments  
  Architecture remains consistent, with scaling and HA primarily applied in Kubernetes deployments.

* **Service dependencies:**  
  * MongoDB (persistent storage)  
  * Keycloak (authentication and authorization)  
  * Kafka (optional, for async APIs)

* **Identity and Access Management:**  
  Microcks integrates with Keycloak and supports OAuth2/OpenID Connect for user authentication and role-based access control.

* **Sovereignty:**  
  Data residency and sovereignty are managed by deploying Microcks within the adopter’s own infrastructure and cluster.

* **Compliance requirements:**  
  Microcks supports compliance indirectly by enabling contract testing, traceability, and controlled access via IAM integration.

* **High Availability:**  
  HA is achieved by deploying multiple replicas of Microcks services in Kubernetes, backed by highly available MongoDB and Kafka deployments.

* **Resource requirements:**  
  Resource usage depends on scale and usage patterns. Typical deployments require moderate CPU and memory, with increased needs when running large numbers of tests or simulations.

* **Storage requirements:**  
  * Persistent storage for MongoDB  
  * Ephemeral storage for pods and runtime data

* **API Design:**  
  * REST-based APIs with well-defined contracts  
  * Sensible defaults for quick setup  
  * Configurable via environment variables and Helm values  
  * Versioned APIs with documented breaking changes

* **Release process:**  
  Microcks follows semantic versioning with documented major, minor, and patch releases, accompanied by release notes.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/architecture

---

### Installation

* **Installation approach:**  
  Microcks can be installed via:
  * Helm charts (recommended for Kubernetes)
  * OpenShift Operator
  * Docker Compose (development/testing)

* **Testing and validation:**  
  Installation is validated by accessing the Microcks UI, deploying sample APIs, and running built-in tests.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/installation

---

### Security

* **Security self assessment:**  
  A formal CNCF security self-assessment is planned but not yet published.

* **Cloud native security tenets:**  
  * Secure by default configurations  
  * Explicit opt-in for advanced or experimental features  
  * Clear documentation for loosening security controls when needed

* **Security hygiene:**  
  * Regular dependency updates  
  * Community review of contributions  
  * CI pipelines for validation and testing

* **Threat modeling:**  
  * Least-privilege access via Kubernetes RBAC  
  * TLS and certificate management handled by the platform  
  * Secure software supply chain practices via container image builds and dependency management

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/security

---

## Day 1 - Installation and Deployment Phase

### Project Installation and Configuration

Microcks is installed primarily on Kubernetes or OpenShift using Helm charts or Operators. Configuration is provided through Helm values, Custom Resources (for Operators), and environment variables. Optional components such as Kafka integration are enabled explicitly.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/installation

---

### Project Enablement and Rollback

* Microcks is enabled by deploying its Kubernetes resources into a namespace.
* No control plane or node downtime is required.
* Disabling is achieved by uninstalling the Helm release or deleting the Operator-managed resource.
* Microcks does not alter cluster defaults or mutate workloads.
* Cleanup is handled automatically by Helm or the Operator.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/operations

---

### Rollout, Upgrade and Rollback Planning

* Compatibility with Kubernetes and OpenShift is maintained through continuous testing and dependency updates.
* Upgrades are performed via Helm upgrade or Operator reconciliation.
* Rollbacks are supported using Helm rollback or redeploying a previous Operator configuration.
* Failures impact only Microcks services, not existing workloads.
* Metrics such as pod health, API error rates, and connectivity issues inform rollback decisions.
* Deprecations and breaking changes are communicated via release notes and documentation.
* Alpha and beta features are explicitly gated and opt-in.

Documentation reference:  
https://github.com/yada/microcks.io/tree/master/content/documentation/release-notes
