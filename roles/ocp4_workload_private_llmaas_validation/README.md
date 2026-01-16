# ocp4_workload_private_llmaas_validation

Ansible role to validate Private LLM as a Service workshop deployments on AWS.

## Description

This role performs comprehensive health checks on all components deployed in the Private LLMaaS workshop environment, including both shared infrastructure and per-user resources.

## Components Validated

### Shared Components

- **Keycloak** - Authentication service (keycloak namespace)
- **OpenShift GitOps** - Argo CD (openshift-gitops namespace)
- **DevSpaces Operator** - Development environment operator (openshift-devspaces namespace)
- **MaaS API** - LiteLLM models-as-a-service (maas-api namespace)
- **Models/vLLM** - Model serving (llm namespace)
- **MCP Servers** - Slack and Kubernetes MCP servers (lls-demo namespace)
- **Grafana** - Monitoring and observability (grafana namespace)
- **Argo CD Applications** - All GitOps-deployed applications

### Per-User Components

- **Showroom** - Workshop content and labs (showroom-{guid}-user{N} namespaces)
- **DevWorkspaces** - User development workspaces (wksp-user{N} namespaces)
- **Llama Stack** - Per-user Llama Stack instances (Argo CD Applications)

## Requirements

- Ansible 2.15+
- kubernetes.core collection
- OpenShift cluster access

## Role Variables

### User Configuration

```yaml
ocp4_workload_private_llmaas_validation_num_users: 1
ocp4_workload_private_llmaas_validation_user_prefix: "user"
```

### Component Toggle Variables

All components are checked by default. You can disable specific checks:

```yaml
ocp4_workload_private_llmaas_validation_check_keycloak: true
ocp4_workload_private_llmaas_validation_check_gitops: true
ocp4_workload_private_llmaas_validation_check_devspaces_operator: true
ocp4_workload_private_llmaas_validation_check_maas_api: true
ocp4_workload_private_llmaas_validation_check_models: true
ocp4_workload_private_llmaas_validation_check_mcp_servers: true
ocp4_workload_private_llmaas_validation_check_grafana: true
ocp4_workload_private_llmaas_validation_check_showroom: true
ocp4_workload_private_llmaas_validation_check_workspaces: true
ocp4_workload_private_llmaas_validation_check_llama_stack: true
ocp4_workload_private_llmaas_validation_check_argocd_apps: true
```

### HTTP Check Configuration

```yaml
ocp4_workload_private_llmaas_validation_http_validate_certs: false
ocp4_workload_private_llmaas_validation_http_timeout: 10
ocp4_workload_private_llmaas_validation_http_success_codes: [200, 301, 302]
```

## Dependencies

None

## Example Playbook

```yaml
- name: Validate Private LLMaaS Workshop
  hosts: localhost
  connection: local
  gather_facts: false

  tasks:
    - name: Run validation
      ansible.builtin.include_role:
        name: rhpds.private_llmaas_validation.ocp4_workload_private_llmaas_validation
      vars:
        ocp4_workload_private_llmaas_validation_num_users: 5
```

## Validation Report

The role generates a comprehensive validation report with:

- Overall status (HEALTHY/DEGRADED/FAILED)
- Component-level health status
- Detailed metrics for each component
- List of detected issues

Results are saved to `agnosticd_user_info` for display in the AgnosticV catalog.

## License

Apache-2.0

## Author

Prakhar Srivastava <psrivast@redhat.com>
