# OpenAPI Specifications (optional)

Drop your OpenAPI spec files here (`.yaml` or `.json`).

- If this directory contains at least one spec file, the sandbox pipeline will create a **contracts library** and make it searchable via `search_contracts` in your sandbox MCP server.
- If this directory is empty (contains only this README), the contracts library step is skipped.

## Naming

Spec files should follow the existing convention in `platform-services-kb`:
```
openapi/
  <service-id>-api.yaml
```
