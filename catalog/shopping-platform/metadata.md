# Shopping Platform Metadata Extraction Guide

## 1. System-Level Metadata

- **System Name**: `shopping-platform`
- **Description**: Example e-commerce platform composed of frontend, backend, database and external APIs
- **Tags**: `example`, `ecommerce`
- **Owner**: `oz-hubs`
- **TechDocs Reference**: `dir:./system`

## 2. Entity Inventory (by Kind)

From [shopping-platform.yaml](catalog/shopping-platform/shopping-platform.yaml):

- **1 System**: `shopping-platform`
- **10 Components**:
  - Internal: `shop-web`, `shop-admin-web`, `shop-orders-service`, `shop-catalog-service`, `shop-catalog-graphql-service`, `shop-inventory-service`, `shop-notification-service`, `shop-shared-lib`
  - External: `payment-gateway`, `email-provider`
- **6 APIs**: `shop-orders-rest-api`, `shop-catalog-rest-api`, `shop-catalog-graphql-api`, `shop-inventory-rest-api`, `payment-gateway-api`, `smtp-api`
- **3 Resources**: `shop-orders-db`, `shop-catalog-db`, `shop-events-bus`

## 3. Per-Entity Metadata

For each entity, the following metadata is captured:

- `metadata.name`: Unique identifier
- `metadata.description`: Human-readable description
- `metadata.tags`: Classification and technology markers
- `metadata.annotations`: Extended attributes (e.g., `backstage.io/techdocs-ref`, `github.com/project-slug`)
- `metadata.links`: External URLs (for vendor components)
- `spec.type`: Component type (website, service, library, openapi, database, message-broker)
- `spec.lifecycle`: Status indicator (`experimental` or `production`)
- `spec.owner`: Responsible team/group
- `spec.system`: System this entity belongs to

## 4. Relationship & Dependency Graph

- **`providesApis`**: Which APIs a Component exposes
- **`consumesApis`**: Which APIs a Component uses
- **`dependsOn`**: Runtime dependencies on other Components or Resources
- Component ↔ System mapping
- API provider/consumer topology

## 5. Technology Stack & Tags

- **Languages/Frameworks**: `dotnet`, `python`, `react`
- **Component roles**: `frontend`, `backend`, `library`
- **Infrastructure**: `postgres`, `kafka`, `messaging`, `database`
- **API categories**: `rest`, `openapi`, `graphql`, `external`

## 6. External Integrations

- **External Components** (vendors): `payment-gateway` (Stripe), `email-provider` (SendGrid)
- **External APIs** consumed: `payment-gateway-api`, `smtp-api`
- **Vendor Links**: URLs defined in component `links` section

## 7. GitHub Integration

- `github.com/project-slug`: Repository reference for internal components
  - Format: `HylandSandbox/{repository-name}`
  - 8 internal repositories tracked (all others are external or utilities)

## 8. TechDocs Integration

- **Coverage**: 100% of entities have `backstage.io/techdocs-ref` configured
- **Structure**: Each component has its own subfolder containing:
  - `mkdocs.yml`: MkDocs configuration
  - `docs/index.md`: Documentation entry point
- **External Specs**:
  - OpenAPI spec file: [openapi.yaml](catalog/shopping-platform/shop-catalog-rest-api/openapi.yaml)
  - GraphQL schema file: [schema.graphql](catalog/shopping-platform/shop-catalog-graphql-api/schema.graphql)
  - 4 APIs include inline OpenAPI definitions
  - 1 API references external OpenAPI spec via `$text:`
  - 1 API references external GraphQL schema via `$text:`

## 9. Derived Metrics & Analytics

Metadata that can be aggregated:

- **Components by type**: Count of services, websites, libraries
- **APIs by lifecycle**: Distribution across experimental vs. production
- **Resources by type**: Databases, message brokers, etc.
- **API topology**: Fan-in/fan-out (consumer/provider count per API)
- **TechDocs coverage**: Percentage of entities with documentation configured
- **GitHub integration**: Repositories tracked in catalog
- **Entry points**: Components without outgoing `dependsOn` relationships
- **External dependencies**: APIs and components marked as `external`

## 10. Ownership & Governance

- **Single Owner**: All entities owned by `oz-hubs` (group defined in [org.yaml](catalog/org.yaml))
- **Governance Opportunity**:
  - Low diversity: 100% ownership by one group
  - Potential for team assignment and RACI matrix expansion
  - Track missing owners across the organization

## 11. Key Relationships Summary

### Data Flow

```text
shop-web → shop-orders-rest-api → shop-orders-service
shop-web → shop-catalog-graphql-api → shop-catalog-graphql-service
shop-admin-web → shop-orders-rest-api, shop-catalog-rest-api, shop-catalog-graphql-api
shop-catalog-graphql-service → shop-catalog-rest-api, shop-inventory-rest-api
shop-orders-service → payment-gateway-api (external)
shop-notification-service → smtp-api (external)
shop-inventory-service → shop-orders-rest-api
```

### Resource Dependencies

```text
shop-orders-service → shop-orders-db, shop-events-bus, shop-shared-lib
shop-catalog-service → shop-catalog-db, shop-shared-lib
shop-inventory-service → shop-events-bus
shop-notification-service → shop-events-bus
```

### API Providers

```text
shop-orders-service → shop-orders-rest-api
shop-catalog-service → shop-catalog-rest-api
shop-catalog-graphql-service → shop-catalog-graphql-api
shop-inventory-service → shop-inventory-rest-api
payment-gateway → payment-gateway-api
email-provider → smtp-api
```

## 12. Extensibility

Additional metadata that could be extracted:

- **Cost allocation**: Cost tagging per component/resource
- **Security posture**: Vulnerability scanning, security gates per component
- **Performance metrics**: Response times, throughput from monitoring systems
- **Compliance**: Data classification, GDPR/regulatory mappings
- **SLO/SLA**: Service level objectives per API
- **Deployment targets**: Kubernetes namespaces, cloud regions
- **Incident history**: MTTR, incident count per component
- **Code quality**: Test coverage, SonarQube metrics, linting status
