# CSS JSON Schema Validation Limitations

**TL;DR:** JSON schema is great for basic CSS validation but can't handle complex CSS grammar, dynamic values, or context-dependent rules.

## Why This Matters

When building CSS property types (like our `Border` interface), we need to understand where JSON schema validation breaks down. This helps us make informed decisions about validation strategies and set proper expectations.

## The Big 3 Limitations

### 1. 🔄 **Complex CSS Grammar** 
**Problem:** CSS uses `||` syntax meaning "any order, all optional"
```css
/* These are ALL valid and equivalent */
border: 1px solid red;
border: solid red 1px;
border: red 1px solid;
```
**JSON Schema:** Falls back to `"type": "string"` - too complex to validate properly.

### 2. 🧮 **Dynamic Values**
**Problem:** `calc()` and `var()` need context and mathematical parsing
```css
border-width: calc(var(--base-width) * 2 + 1px);
border-color: var(--brand-color, red);
```
**JSON Schema:** Can only validate syntax patterns, not mathematical validity or variable existence.

### 3. 📏 **Range Validation**
**Problem:** CSS has numeric ranges within string values
```css
rgb(255, 0, 0)    /* 0-255 range */
hsl(360, 100%, 50%)  /* 0-360° hue, 0-100% saturation/lightness */
```
**JSON Schema:** Regex can't enforce numeric ranges - would allow `rgb(999, -50, 500)`.

## What Works Well ✅

| **CSS Feature** | **JSON Schema** | **Why** |
|-----------------|------------------|---------|
| **Enum Values** | ✅ Perfect | `border-style: solid` - fixed value sets |
| **Basic Patterns** | ✅ Good | Simple regex for basic syntax |
| **Type Checking** | ✅ Perfect | String vs number validation |
| **Structure** | ✅ Perfect | Required properties, object shape |

## Practical Recommendations

### 🎯 **Use JSON Schema For**
- **Structure validation** (required properties, object shape)
- **Enum values** (`border-style: solid` works perfectly)
- **Basic patterns** (simple regex validation)
- **Type checking** (string vs number)

### 🚫 **Don't Rely on JSON Schema For**
- **Complex shorthand syntax** (use `"type": "string"` with good docs)
- **Dynamic expressions** (`calc()`, `var()` - validate elsewhere)
- **Numeric ranges in strings** (RGB, HSL values)
- **Context-dependent validation** (inheritance, element types)

### 💡 **Best Practices**
1. **Be permissive** - Use `"type": "string"` for complex properties
2. **Document limitations** - Explain what the schema can't validate
3. **Layer validation** - JSON schema + CSS parsers for full validation
4. **Focus on structure** - Use JSON schema for what it's good at

### 📖 **Example**
```json
{
  "border": {
    "type": "string",
    "description": "CSS border shorthand. Note: JSON schema cannot validate the any-order syntax (1px solid red = red solid 1px)"
  },
  "borderStyle": {
    "enum": ["none", "hidden", "dotted", "dashed", "solid", "double", "groove", "ridge", "inset", "outset"],
    "description": "Border line style - JSON schema handles this perfectly"
  }
}
```

## Summary

**JSON Schema is great for basic CSS validation** but hits limits with CSS's complex grammar and dynamic features. Use it for structure and simple validation, then layer in CSS parsers for full compliance when needed. 