---
name: "jsonparse"
displayName: "JSON Parse"
description: "Parse, validate, transform, and query JSON data with advanced schema validation, path extraction, and format conversion capabilities"
keywords: ["json", "parsing", "validation", "schema", "data-transformation", "query"]
author: "JSON Parse"
---

# Onboarding

Before proceeding, validate that the user has completed the following steps before using this power.

## Step 1

No authentication required. The JSON Parse power works locally without external dependencies or API keys.

## Step 2

Create a hook that runs anytime JSON files are modified. Save the hook in .kiro/hooks/hookname.kiro.hook. Example hook format:

```json
{
  "enabled": true,
  "name": "JSON Validation",
  "description": "Monitors JSON file changes and automatically validates syntax and schema compliance",
  "version": "1",
  "when": {
    "type": "fileEdited",
    "patterns": [
      "*.json",
      "*.jsonc",
      "*.json5",
      "config/**/*.json",
      "data/**/*.json"
    ]
  },
  "then": {
    "type": "askAgent",
    "prompt": "A JSON file has been modified. Please validate the JSON syntax and structure. If there are any errors, report them and suggest fixes."
  }
}
```

# Overview

Parse, validate, and transform JSON data with comprehensive schema validation, path-based querying, and format conversion. Perfect for working with configuration files, API responses, and data processing workflows.

**No Authentication Required**: Works entirely locally with no external dependencies.

## Available MCP Servers

### json-parse
**Package:** `json-parse-mcp-server`
**Connection:** Local MCP server
**Authentication:** None required
**Mode:** Full (25 essential tools)
**Endpoint:** Local process

**Available Tools (25):**

**Parsing & Validation:**
- `parseJson` - Parse JSON string with error reporting
- `validateJson` - Validate JSON against schema
- `validateJsonSchema` - Validate JSON schema itself
- `detectJsonFormat` - Detect JSON format (minified, pretty-printed, etc.)

**Schema Operations:**
- `generateSchema` - Generate JSON schema from data
- `inferSchema` - Infer schema from multiple JSON samples
- `validateAgainstSchema` - Validate JSON against provided schema
- `getSchemaErrors` - Get detailed schema validation errors

**Querying & Extraction:**
- `queryJson` - Query JSON using JSONPath
- `extractPaths` - Extract all paths from JSON
- `getValueAtPath` - Get value at specific path
- `setValueAtPath` - Set value at specific path
- `deleteValueAtPath` - Delete value at specific path
- `flattenJson` - Flatten nested JSON structure
- `unflattenJson` - Unflatten flattened JSON

**Transformation:**
- `transformJson` - Transform JSON using mapping rules
- `mergeJson` - Merge multiple JSON objects
- `diffJson` - Compare two JSON objects
- `sortJson` - Sort JSON keys recursively
- `minifyJson` - Minify JSON string
- `prettifyJson` - Pretty-print JSON with formatting

**Format Conversion:**
- `jsonToYaml` - Convert JSON to YAML
- `jsonToCsv` - Convert JSON array to CSV
- `jsonToXml` - Convert JSON to XML

## Tool Usage Examples

```javascript
// Parse JSON string
mcp_json_parse_parseJson({
  "jsonString": "{\"name\": \"John\", \"age\": 30}"
})

// Validate against schema
mcp_json_parse_validateAgainstSchema({
  "json": { "name": "John", "age": 30 },
  "schema": {
    "type": "object",
    "properties": {
      "name": { "type": "string" },
      "age": { "type": "number" }
    },
    "required": ["name", "age"]
  }
})

// Query JSON with JSONPath
mcp_json_parse_queryJson({
  "json": { "users": [{ "name": "John", "age": 30 }, { "name": "Jane", "age": 25 }] },
  "path": "$.users[*].name"
})

// Transform JSON
mcp_json_parse_transformJson({
  "json": { "firstName": "John", "lastName": "Doe" },
  "mapping": { "firstName": "first", "lastName": "last" }
})

// Merge JSON objects
mcp_json_parse_mergeJson({
  "objects": [
    { "name": "John", "age": 30 },
    { "city": "New York" }
  ]
})
```

## Workflows

**Validate Configuration Files:**
```javascript
const { isValid, errors } = await mcp_json_parse_validateJson({ "jsonString": configContent })
if (!isValid) {
  console.log("Config errors:", errors)
}
```

**Extract Data from API Response:**
```javascript
const { result } = await mcp_json_parse_queryJson({
  "json": apiResponse,
  "path": "$.data[*].id"
})
```

**Generate Schema from Sample Data:**
```javascript
const { schema } = await mcp_json_parse_generateSchema({
  "json": sampleData
})
```

**Transform and Merge Multiple Sources:**
```javascript
const { result: transformed } = await mcp_json_parse_transformJson({
  "json": sourceData,
  "mapping": fieldMapping
})
const { result: merged } = await mcp_json_parse_mergeJson({
  "objects": [transformed, additionalData]
})
```

**Compare Configuration Versions:**
```javascript
const { differences } = await mcp_json_parse_diffJson({
  "json1": oldConfig,
  "json2": newConfig
})
```

## Best Practices

- Always validate JSON before processing
- Use JSONPath for efficient data extraction
- Generate schemas from sample data for consistency
- Pretty-print JSON for readability during development
- Use schema validation for configuration files
- Keep minified versions for production
- Document custom transformation mappings

## Troubleshooting

**"Invalid JSON"**: Use `parseJson` to get detailed error location and message

**"Schema validation failed"**: Call `getSchemaErrors` for specific field violations

**"JSONPath query returned empty"**: Verify path syntax and use `extractPaths` to explore structure

**"Merge conflicts"**: Use `diffJson` to identify conflicting keys before merging

**"Encoding issues"**: Ensure JSON is UTF-8 encoded before parsing

## Configuration

**MCP Configuration:**
```json
{
  "mcpServers": {
    "json-parse": {
      "command": "node",
      "args": ["json-parse-server.js"]
    }
  }
}
```

**No API keys or authentication required** - works entirely locally with no external dependencies.