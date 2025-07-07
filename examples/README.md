# CSS Property Examples

JSON examples for CSS property validation testing and reference.

## Border Examples (78 total)
- **`basic-borders.json`** - Basic patterns (8 examples)
- **`advanced-values.json`** - Modern CSS features (16 examples)
- **`border-radius.json`** - Rounded corners (12 examples)
- **`border-images.json`** - Decorative borders (12 examples)
- **`real-world-examples.json`** - UI components (30 examples)

## Margin Examples (38 total)
- **`margin-examples.json`** - Complete margin examples (basic, advanced, logical properties, real-world usage)

## Usage

### Validation
```bash
ajv validate -s schemas/margin-schema.json -d examples/margin-examples.json
```

### Reference
```javascript
const cardStyle = {
  border: "1px solid #e1e5e9",
  borderRadius: "8px",
  margin: "1rem"
};
```

All examples pass their respective schema validation. 