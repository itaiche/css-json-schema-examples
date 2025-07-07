# CSS Property Schemas

Modular JSON schemas for CSS property validation.

## Core Types
- **`css-data-types.json`** - Basic CSS types (length, percentage, variables, calc)
- **`css-color-types.json`** - Complete color validation (147 named colors, hex, RGB, HSL)

## Property Types
- **`css-border-types.json`** - Border property types
- **`css-border-image-types.json`** - Border image types  
- **`css-margin-types.json`** - Margin property types

## Complete Schemas
- **`border-schema.json`** - All border properties
- **`margin-schema.json`** - All margin properties

## Usage
```bash
# Validate with AJV
ajv validate -s margin-schema.json -d your-data.json
```

Schemas use `$ref` cross-references for modularity and reusability. 