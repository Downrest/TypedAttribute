# TypedAttribute
[![Wally](https://img.shields.io/badge/Wally-Package-orange?style=for-the-badge)](https://wally.run/package/downrest/typedattribute)

A typed attribute wrapper with an object-oriented API.

Used for cases where attributes are shared between client/server to replicate gamestate. TypedAttribute exposes equivalent API for both sides.

Constructing a typed attribute is done thru:
* `new<type>(attributeName: string, defaultValue: type)`

The getter is:
* `Get(): type`

The setter (internally typechecked at runtime) is:
* `Set(setValue: type)`

There is also a signal for attribute value changes:
* `Changed:Connect(function(previousValue: type, newValue: type))`

Example usage:
```luau
local Attribute = TypedAttribute.new("Attribute", false)

-- getter
Attribute:Get()

-- setter
Attribute:Set(true)
Attribute:Set("hi") -- TypeError: Expected this to be `boolean`, but got `string`

-- changed signal
Attribute.Changed:Connect(function(previousValue: boolean, newValue: boolean)
    ...
end)
```