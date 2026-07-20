# Contributing

Profiles are executable descriptions of real devices. Changes should preserve wire
semantics and be reviewable against a protocol document, capture, or tested device.

## Profile changes

- Name files and identifiers consistently with nearby profiles.
- Include manufacturer, model, firmware, and protocol documentation where known.
- Use the current native type descriptor grammar, not backward-compatibility aliases.
- Keep access in the column following the type. Omitted access means read-only.
- Use protocol-default byte order unless the device explicitly differs.
- Use standard units and scaling. If a unit is not representable, document it rather
  than silently substituting a dimensionally different unit.
- Explain device quirks and non-obvious transforms with short comments.
- Do not include credentials, serial numbers, site addresses, or other deployment data.

## Testing

Test against hardware when possible and state what was exercised, including reads,
writes, dynamic values, enum or bitfield formatting, and unusual byte order. Profile
parser and runtime tests currently live in the parent OpenWatt repository.

When a profile requires a new grammar feature, land and test that feature in OpenWatt
before depending on it here.

## Pull requests

Keep unrelated devices in separate changes. Describe the device and protocol, cite the
source of register or field definitions, and call out any behaviour that could not be
verified on hardware.
