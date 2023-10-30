# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v1.0.0-rc.3] - 2023-10-18

### Changed

- Fixed several issues with OpenAPI specification
- Basic Spatial Operators in CQL2 now only requires BBOX and POINT support, so the text
  and examples were updated to account for this.
- Fixed the CQL2 JSON between operator example to use 3 items array

### Added

- References [DotNetStac.Api](https://github.com/Terradue/DotNetStac.Api) for its support
    for [CQL2 JSON](https://github.com/Terradue/DotNetStac.Api/blob/5e7334e95da92ca19f9e9b75c476f362ae24a6da/src/Stac.Api/Models/Cql2/CQL2.cs)

## [v1.0.0-rc.2] - 2022-11-01

### Changed

- Update language on catalog-level queryables
- Fix several examples

## [v1.0.0-rc.1] - 2022-03-17

### Added

- Filter Extension - the CQL2 Accent and Case-insensitive Comparison 
    (`http://www.opengis.net/spec/cql2/1.0/conf/accent-case-insensitive-comparison`) conformance class
    adds the ACCENTI and CASEI functions for case-insensitive comparison. These replace the UPPER and
    LOWER psuedo-functions that were previously part of the Advanced Comparison Operators class.

### Changed

- Specifications now use the term "must" instead of "shall". The semantics of these words are identical.
- Conformance class for Item Search Filter is now
  `https://api.stacspec.org/v1.0.0-beta.5/item-search#filter`, whereas before it was incorrectly stated as
  `https://api.stacspec.org/v1.0.0-beta.5/item-search#filter:item-search-filter`

## [v1.0.0-beta.5] - 2022-01-14

### Changed

- Filter Extension updates to align with changes to OAFeat CQL2 spec
  - Updated all "CQL" usages to "CQL2"
  - Most conformance class URIs are now prefixed with `http://www.opengis.net/spec/cql2/` instead
    of `http://www.opengis.net/spec/ogcapi-features-3/`
  - Conformance classes `http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/basic-cql`,
    `http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/cql-text`, and
    `http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/cql-json` have had `cql` replaced
    with `cql2` (in addition to the prefix change) to
    become `http://www.opengis.net/spec/cql2/1.0/conf/basic-cql2`,
    `http://www.opengis.net/spec/cql2/1.0/conf/cql2-text`, and
    `http://www.opengis.net/spec/cql2/1.0/conf/cql2-json`
  - Significant changes to CQL2 JSON format, now using `op` and `args` structure
  - Spatial operator `INTERSECTS` is now `S_INTERSECTS`
  - Temporal operator `ANYINTERACTS` is now `T_INTERSECTS`
  - Updated Example 3 (now Example 5) to make it clear that property to property comparisons require the
    Property-Property Comparisons conformance class
  - The CQL2 Case-insensitive Comparison
    (`http://www.opengis.net/spec/cql2/1.0/conf/case-insensitive-comparison`) conformance class
    that adds UPPER/LOWER terms or function CASEI for case-insensitive comparison has not been added
    to this spec yet, since the definition in CQL2 is in flux.

### Fixed

- Filter Extension - examples of using intervals and timestamps in CQL2 were incorrect and have been fixed
- Filter Extension - examples are updated so that text and json examples are equivalent

## [v1.0.0-beta.4] - 2021-10-05

### Changed

- Filter Extension - query language is now referred to as "CQL2" rather than CQL
- Filter Extension now uses OAFeat Part 3 conformance class URIs
- Filter Extension - The following changes have been made to the Filter Extension conformance classes to align with changes to the OAFeat CQL draft. All classes
  whose names have changed also have changed conformance URI strings.
  - "Basic CQL" now includes the "not equal" operator (`<>`)
  - "Basic CQL" has always supported datetime comparisons, but this is now explicitly mentioned
  - "Enhanced Comparison Operators" has been renamed "Advanced Comparison Operators". This is the same as the OAFeat CQL definition, except
    that it does not require the `upper` and `lower` functions.
  - "Enhanced Spatial Operators" has been renamed to just "Spatial Operators" (not to be confused with Basic Spatial Operators)
  - "Basic Temporal Operators" and "Enhanced Temporal Operators" have merged into "Temporal Operators"
  - "Functions" has been renamed "Custom Functions"
  - "Arithmetic" has been renamed "Arithmetic Expressions"
  - "Arrays" has been renamed "Array Operators"
  - "Queryable Second Operand" has been renamed "Property-Property Comparisons"

## [v1.0.0-beta.3] - 2021-08-06

### Changed
- Filter Extension conformance classes refactored to better align with STAC API use cases.
- Renamed conformance class "Queryable First Operand"
  (https://api.stacspec.org/v1.0.0-beta.3/item-search#filter:queryable-first-operand) to
  "Queryable Second Operand"
  (https://api.stacspec.org/v1.0.0-beta.3/item-search#filter:queryable-second-operand)

## [v1.0.0-beta.2] - 2021-06-01

### Added
- Added Filter extension to integrate OAFeat Part 3 CQL

## Older versions

See the [stac-api-spec CHANGELOG](https://github.com/radiantearth/stac-api-spec/blob/v0.9.0/CHANGELOG.md)
for STAC API releases prior to or equal to version v1.0.0-rc.2.

[Unreleased]: <https://github.com/stac-api-extensions/filter/compare/v1.0.0-rc.3..main>
[v1.0.0-rc.3]: <https://github.com/stac-api-extensions/filter/tree/v1.0.0-rc.3>
[v1.0.0-rc.2]: <https://github.com/stac-api-extensions/filter/tree/v1.0.0-rc.2>
[v1.0.0-rc.1]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-rc.1>
[v1.0.0-beta.5]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-beta.5>
[v1.0.0-beta.4]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-beta.4>
[v1.0.0-beta.3]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-beta.3>
