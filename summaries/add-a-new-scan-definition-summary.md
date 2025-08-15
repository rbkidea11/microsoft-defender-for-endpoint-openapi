# Endpoints: Authenticated Scan Definition Management

**Source:** add-a-new-scan-definition.md  
**Tags:** AuthenticatedScan  
**Summary:** Create, update, and batch delete scan definitions  

## Endpoint 1: POST /api/DeviceAuthenticatedScanDefinitions

**OperationId:** createScanDefinition

### Description
Creates a new authenticated scan definition for Windows or Network device vulnerability scanning.

### Request Body
```json
{
  "scanName": "string",
  "scanType": "Windows|Network",
  "targets": ["string"],
  "authenticationParameters": {
    "username": "string",
    "password": "string",
    "domain": "string"
  },
  "scheduleSettings": {
    "frequency": "string",
    "startTime": "datetime"
  }
}
```
**Required:** scanName, scanType, targets, authenticationParameters

### Responses
### 201 Created
```json
{
  "id": "string",
  "scanName": "string",
  "scanType": "string",
  "status": "Active",
  "createdDateTime": "datetime"
}
```

---

## Endpoint 2: PATCH /api/DeviceAuthenticatedScanDefinitions/{id}

**OperationId:** updateScanDefinition

### Description
Updates an existing authenticated scan definition.

### Parameters
### Path Parameters
- `id` (string, required): Scan definition ID

### Request Body
```json
{
  "scanName": "string",
  "targets": ["string"],
  "scheduleSettings": {
    "frequency": "string",
    "startTime": "datetime"
  }
}
```

### Responses
### 200 Success
```json
{
  "id": "string",
  "scanName": "string",
  "scanType": "string",
  "status": "Active",
  "lastModifiedDateTime": "datetime"
}
```

---

## Endpoint 3: POST /api/DeviceAuthenticatedScanDefinitions/BatchDelete

**OperationId:** batchDeleteScanDefinitions

### Description
Deletes multiple scan definitions in a single batch operation.

### Request Body
```json
{
  "scanDefinitionIds": ["string", "string"]
}
```
**Required:** scanDefinitionIds

### Responses
### 200 Success
```json
{
  "deletedIds": ["string"],
  "failedIds": ["string"]
}
```

---

## Common Properties

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Scan management permissions required

### Rate Limits
- Standard API rate limits apply

### OData Support
- ❌ Not applicable for POST/PATCH operations

## Example
```http
POST /api/DeviceAuthenticatedScanDefinitions
Authorization: Bearer {token}
Content-Type: application/json

{
  "scanName": "Weekly Windows Scan",
  "scanType": "Windows",
  "targets": ["192.168.1.0/24"],
  "authenticationParameters": {
    "username": "scanuser",
    "password": "password",
    "domain": "contoso.com"
  }
}
```

## Notes
- Supports both Windows and Network scan types
- Authentication parameters are required for all scan definitions
- Batch delete supports multiple scan definitions in single operation

---
