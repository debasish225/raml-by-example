---
publication: 'RAML Playground'
tags: ['RAML', 'ramldt2jsonschema', 'JSON Schema']
license: 'cc-40-by'
---

# `ramldt2jsonschema` v0.2.0 released 🎉

If your workflow involves the use of JSON Schema to describe the payloads of your api, and `ramldt2jsonschema`'s js2dt command to convert them into raml, then you might be glad to know that as of v0.2.0, `ramldt2jsonschema` supports draft-06 of JSON Schema. 

Here are a few of the new features introduced in JSON Schema draft-06:

- `$ref` is now allowed as a property name.

```
{
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "list": {
      "type": "array"
    },
    "$ref": {
      "type": "string"
    }
  },
  "additionalProperties": false
}
```

- Positive schema booleans can now be used outside of `additionalProperties` and `additionalItems` (negative booleans are still not convertible into raml). Here `"list": true`, and `"description": {}` have the same effect.

```
{
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "list": true,
    "description": {},
    "forSale": {
      "type": "boolean",
      "default": true
    }
  },
  "required": ["list", "description"],
  "additionalProperties": false
}
```

- Introducing the new `const` keyword, a more readible form of a one-element `enum`

```
{
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Task",
  "type": "object",
  "properties": {
    "difficulty": {
      "type": "string",
      "enum": ["easy", "hard"]
    },
    "type": {
      "type": "string",
      "const": "list"
    }
  }
}
```

- The `required` jsonschema keyword may now contain an empty array, indicating that no properties are required.

```
{
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Product",
  "type": "object",
  "properties": {
    "list": {
      "type": "array"
    }
  },
  "required": []
}
```

Try-it out:
```sh
$ npm i -g ramldt2jsonschema@0.2.0
```
