# JIRA Issue Creation Prompts for CES AI First Training Project

This document provides sample prompts for creating JIRA issues in the 'CES AI First Training' project. These examples demonstrate how to create an Epic, link Stories to it, and create Subtasks for implementation and testing with acceptance criteria.

## Prerequisites

- JIRA instance with appropriate permissions for project 'CES AI First Training' (project key: CES)
- MCP server configured for JIRA integration
- Issue types configured (Epic, Story, Subtask)

## Epic Creation

### Prompt: Create Product CRUD Operations Epic

```
Create a JIRA Epic in project CES with the following details:
- Summary: Product CRUD Operations
- Description: Implement core Create, Read, Update, Delete operations for products with proper validation and error handling.
- Priority: High
- Story Points: 50
- Acceptance Criteria:
  - All CRUD operations work correctly with proper validation and error handling
  - GET operations return products with pagination (default 20 items)
  - POST/PUT operations validate input and return appropriate HTTP status codes
  - DELETE operations remove products and handle not found cases
- Labels: backend, api, crud, ces-training
```

**Expected Result**: Creates Epic CES-100 with key "CES-100"

## Story Creation and Linking

### Prompt: Create Create Product Story

```
Create a JIRA Story in project CES linked to Epic CES-100 with the following details:
- Summary: As a user, I want to create new products so that I can add items to the catalog
- Description: Implement POST /products endpoint with validation for product creation
- Priority: High
- Story Points: 8
- Acceptance Criteria:
  - Given valid product data, when POST /products is called, then a new product is created with HTTP 201
  - Given invalid data (empty name), when POST /products is called, then HTTP 400 is returned with validation errors
  - Given duplicate ID attempt, when POST /products is called, then HTTP 409 is returned
- Labels: backend, api, validation, ces-training
```

**Expected Result**: Creates Story CES-101 linked to Epic CES-100

### Prompt: Create Retrieve Products Story

```
Create a JIRA Story in project CES linked to Epic CES-100 with the following details:
- Summary: As a user, I want to view product information so that I can browse the catalog
- Description: Implement GET /products and GET /products/{id} endpoints with pagination support
- Priority: High
- Story Points: 13
- Acceptance Criteria:
  - Given existing products, when GET /products is called, then all products are returned with HTTP 200
  - Given valid product ID, when GET /products/{id} is called, then product details are returned with HTTP 200
  - Given invalid product ID, when GET /products/{id} is called, then HTTP 404 is returned
  - Pagination works with default 20 items per page
- Labels: backend, api, pagination, ces-training
```

**Expected Result**: Creates Story CES-102 linked to Epic CES-100

### Prompt: Create Update Product Story

```
Create a JIRA Story in project CES linked to Epic CES-100 with the following details:
- Summary: As a user, I want to modify product information so that I can keep the catalog current
- Description: Implement PUT /products/{id} and PATCH /products/{id} endpoints for product updates
- Priority: High
- Story Points: 10
- Acceptance Criteria:
  - Given valid product data, when PUT /products/{id} is called, then product is updated with HTTP 200
  - Given partial data, when PATCH /products/{id} is called, then only specified fields are updated
  - Given invalid product ID, when PUT /products/{id} is called, then HTTP 404 is returned
- Labels: backend, api, partial-update, ces-training
```

**Expected Result**: Creates Story CES-103 linked to Epic CES-100

### Prompt: Create Delete Product Story

```
Create a JIRA Story in project CES linked to Epic CES-100 with the following details:
- Summary: As a user, I want to remove products so that I can manage the catalog
- Description: Implement DELETE /products/{id} endpoint with soft delete functionality
- Priority: Medium
- Story Points: 5
- Acceptance Criteria:
  - Given valid product ID, when DELETE /products/{id} is called, then product is deleted with HTTP 204
  - Given invalid product ID, when DELETE /products/{id} is called, then HTTP 404 is returned
- Labels: backend, api, soft-delete, ces-training
```

**Expected Result**: Creates Story CES-104 linked to Epic CES-100

## Subtask Creation with Acceptance Criteria

### Prompt: Create Implementation Subtasks for Create Product Story

```
Create the following Subtasks for Story CES-101:
1. Define Product Data Model - Story Points: 2
   - Description: Implement Product entity with ID, name, price, description, category, stock quantity
   - Acceptance Criteria:
     - Product class/record created with all required fields
     - Fields have appropriate data types and constraints
   - Assignee: backend-developer
   - Labels: model, entity, ces-training

2. Implement Validation Logic - Story Points: 3
   - Description: Add server-side validation for all fields with appropriate error messages
   - Acceptance Criteria:
     - Name validation: required, 1-100 chars, not whitespace
     - Price validation: positive decimal
     - Stock validation: non-negative integer
     - Clear error messages returned for each validation failure
   - Assignee: backend-developer
   - Labels: validation, error-handling, ces-training

3. Create POST /products Endpoint - Story Points: 3
   - Description: Implement endpoint in all backend services (Java, .NET, Python) with validation and storage
   - Acceptance Criteria:
     - Endpoint accepts POST /products
     - Validates input data before storage
     - Returns 201 on success with created product
     - Returns 400 on validation errors
     - Product stored in memory/database
   - Assignee: backend-developer
   - Labels: endpoint, multi-service, ces-training
```

**Expected Result**: Creates Subtasks CES-105, CES-106, CES-107 linked to Story CES-101

### Prompt: Create Testing Subtasks for Create Product Story

```
Create the following testing Subtasks for Story CES-101:
1. Unit Tests for Product Creation - Story Points: 2
   - Description: Write unit tests for POST /products endpoint covering success and validation failure scenarios
   - Acceptance Criteria:
     - Test for successful product creation
     - Test for validation errors (empty name, negative price)
     - Test for duplicate ID handling
     - All tests pass
   - Assignee: qa-engineer
   - Labels: unit-test, validation, ces-training

2. Integration Tests for Product Creation - Story Points: 3
   - Description: Write integration tests for product creation with database/storage layer
   - Acceptance Criteria:
     - Test end-to-end product creation flow
     - Verify data persistence
     - Test error scenarios with storage layer
     - All integration tests pass
   - Assignee: qa-engineer
   - Labels: integration-test, database, ces-training

3. API Contract Tests for Product Creation - Story Points: 2
   - Description: Write API contract tests ensuring request/response format compliance
   - Acceptance Criteria:
     - Request/response schemas match OpenAPI spec
     - HTTP status codes correct
     - Error response format consistent
     - Contract tests pass against all services
   - Assignee: qa-engineer
   - Labels: contract-test, api, ces-training
```

**Expected Result**: Creates Subtasks CES-108, CES-109, CES-110 linked to Story CES-101

### Prompt: Create Implementation Subtasks for Retrieve Products Story

```
Create the following Subtasks for Story CES-102:
1. Implement GET /products Endpoint - Story Points: 5
   - Description: Return all products with pagination and include total count in response
   - Acceptance Criteria:
     - Returns list of products with HTTP 200
     - Supports pagination parameters (page, size)
     - Includes total count in response
     - Default page size 20, max 100
   - Assignee: backend-developer
   - Labels: endpoint, pagination, ces-training

2. Implement GET /products/{id} Endpoint - Story Points: 3
   - Description: Retrieve single product by ID with proper not found handling
   - Acceptance Criteria:
     - Returns product details with HTTP 200 for valid ID
     - Returns HTTP 404 for invalid/non-existent ID
     - Response format matches product schema
   - Assignee: backend-developer
   - Labels: endpoint, single-item, ces-training

3. Add Pagination Support - Story Points: 5
   - Description: Implement page size and page number parameters with custom page sizes (10-100)
   - Acceptance Criteria:
     - Query parameters page and size supported
     - Page size between 10-100
     - Proper pagination metadata returned
     - Handles edge cases (empty pages, invalid params)
   - Assignee: backend-developer
   - Labels: pagination, query-params, ces-training
```

**Expected Result**: Creates Subtasks CES-111, CES-112, CES-113 linked to Story CES-102

### Prompt: Create Testing Subtasks for Retrieve Products Story

```
Create the following testing Subtasks for Story CES-102:
1. Unit Tests for Product Retrieval - Story Points: 3
   - Description: Write unit tests for GET endpoints covering success, not found, and pagination scenarios
   - Acceptance Criteria:
     - Test successful product list retrieval
     - Test single product retrieval (found/not found)
     - Test pagination logic
     - Test invalid parameter handling
   - Assignee: qa-engineer
   - Labels: unit-test, pagination, ces-training

2. Performance Tests for Product Retrieval - Story Points: 2
   - Description: Write performance tests ensuring response times under 200ms for GET operations
   - Acceptance Criteria:
     - GET /products responds in <200ms (95th percentile)
     - GET /products/{id} responds in <200ms
     - Tests pass under simulated load
   - Assignee: qa-engineer
   - Labels: performance-test, load-testing, ces-training

3. API Contract Tests for Product Retrieval - Story Points: 2
   - Description: Write API contract tests for GET endpoints ensuring proper response formats
   - Acceptance Criteria:
     - Response schemas match OpenAPI specification
     - Pagination metadata format correct
     - Error responses properly formatted
   - Assignee: qa-engineer
   - Labels: contract-test, api, ces-training
```

**Expected Result**: Creates Subtasks CES-114, CES-115, CES-116 linked to Story CES-102

## Bulk Creation Example

### Prompt: Create All CRUD Stories at Once

```
Create the following JIRA Stories in project CES, all linked to Epic CES-100:

1. Update Product Story:
   - Summary: As a user, I want to modify product information so that I can keep the catalog current
   - Description: Implement PUT /products/{id} and PATCH /products/{id} endpoints
   - Priority: High
   - Story Points: 10
   - Acceptance Criteria: [list criteria]
   - Labels: backend, api, partial-update, ces-training

2. Delete Product Story:
   - Summary: As a user, I want to remove products so that I can manage the catalog
   - Description: Implement DELETE /products/{id} endpoint
   - Priority: Medium
   - Story Points: 5
   - Acceptance Criteria: [list criteria]
   - Labels: backend, api, soft-delete, ces-training
```

**Expected Result**: Creates Stories CES-117, CES-118 linked to Epic CES-100

## Automation Script Example

For bulk operations, you can create a script that chains these prompts:

```bash
# Create Epic
mcp jira create-epic --project CES --summary "Product CRUD Operations" --description "..." --priority High --story-points 50

# Create Stories
mcp jira create-story --project CES --epic CES-100 --summary "Create Product" --description "..." --priority High --story-points 8

mcp jira create-story --project CES --epic CES-100 --summary "Retrieve Products" --description "..." --priority High --story-points 13

# Create Subtasks
mcp jira create-subtask --parent CES-101 --summary "Define Product Data Model" --story-points 2 --assignee backend-developer

mcp jira create-subtask --parent CES-101 --summary "Implement Validation Logic" --story-points 3 --assignee backend-developer
```

## Notes

- Project key is CES for 'CES AI First Training' project
- Adjust issue numbers based on your JIRA instance's numbering
- Ensure MCP server has proper JIRA API credentials configured
- Use bulk creation for efficiency when creating multiple related issues
- Always verify issue links and relationships after creation
- Acceptance criteria are included for all subtasks to ensure quality and completeness
