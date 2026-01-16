# RHPDS Private LLMaaS Validation Collection

Ansible collection for validating Private LLM as a Service workshop deployments on AWS.

## Description

This collection provides validation roles to verify the health and readiness of all components deployed in the Private LLMaaS workshop environment.

## Components Validated

### Shared Components

- **Keycloak** - Authentication service (keycloak namespace)
- **OpenShift GitOps** - Argo CD (openshift-gitops namespace)
- **DevSpaces Operator** - Development environment operator (openshift-devspaces namespace)
- **OpenShift AI** - AI platform operator
- **MaaS API** - LiteLLM models-as-a-service (maas-api namespace)
- **Models/vLLM** - Model serving (llm namespace)
- **Grafana** - Monitoring and observability
- **Slack MCP** - Slack integration
- **Llama Stack** - LlamaStack instances
- **Kubernetes MCP** - Kubernetes MCP server

### Per-User Components

- **Showroom** - Workshop content and labs
- **Llama Stack** - Per-user Llama Stack instances

**Note:** DevWorkspaces are created on-demand when users log in. The validation only checks that the DevSpaces operator is healthy.

## Roles

### rhpds.private_llmaas_validation.ocp4_workload_private_llmaas_validation

Validates all deployed workshop components and generates a comprehensive health report.

## Installation

```bash
ansible-galaxy collection install rhpds.private_llmaas_validation
```

## Usage

```yaml
- name: Validate Private LLMaaS Workshop
  hosts: localhost
  tasks:
    - name: Run validation
      ansible.builtin.include_role:
        name: rhpds.private_llmaas_validation.ocp4_workload_private_llmaas_validation
```

## License

Apache-2.0

## Author

Prakhar Srivastava <psrivast@redhat.com>
