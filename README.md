# OpenWatt Profiles

This repository is the canonical catalogue of device profiles for
[OpenWatt](https://github.com/open-watt/openwatt). Profiles describe protocol data,
its native type and unit, and how that data is mounted into the OpenWatt device model.

It is intended to be checked out by OpenWatt at `conf/profiles` as a Git submodule.

## Status

The profile format is being centralised and normalised. Existing protocol-specific
profile directories are moving here as their loaders adopt the shared profile model.
During that migration, the authoritative type descriptor grammar is documented in the
header of [`src/manager/spec.d`](https://github.com/open-watt/openwatt/blob/main/src/manager/spec.d),
and the wider model is described in
[`docs/DATA_MODEL.draft.md`](https://github.com/open-watt/openwatt/blob/main/docs/DATA_MODEL.draft.md).

New and migrated profiles should use the native descriptor language. In particular:

- include scaling and units in the type descriptor where supported;
- use `s8`, `s16`, `s32`, and `s64` for signed integers;
- place optional `R`, `W`, or `RW` access in the column after the type;
- rely on the protocol's byte-order context and specify layout modifiers only when the
  device differs from that default;
- avoid legacy aliases in new profiles.

## Using the catalogue

From an OpenWatt checkout:

```sh
git submodule update --init conf/profiles
```

OpenWatt loads profiles at runtime. A profile change therefore needs to be deployed
alongside the compatible OpenWatt build; updating only the executable can leave the
runtime profile grammar out of sync.

The runtime searches its configured profile path recursively by profile basename. The
path defaults to this repository at `conf/profiles`, can be set with
`/system/profile-path`, and can be overridden with the process `--profile-path` option.
Directories are only organisational, so every `.conf` basename must be globally unique.
A duplicate is an error rather than an implicit protocol or filesystem-order preference.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Device documentation links, exact model
identifiers, protocol captures, and hardware test results are especially valuable.

## License

OpenWatt Profiles uses the same dual-license terms as the parent OpenWatt project. See
[LICENSE.md](LICENSE.md) and [LICENSE-MPL-2.0.md](LICENSE-MPL-2.0.md).
