# STAC API - Filter Extension Specification

- [STAC API - Filter Extension Specification](#stac-api---filter-extension-specification)
  - [Overview](#overview)
  - [Limitations of Item Search](#limitations-of-item-search)
  - [Filter Expressiveness](#filter-expressiveness)
  - [Conformance Classes](#conformance-classes)
  - [Getting Started with Implementation](#getting-started-with-implementation)
  - [Queryables](#queryables)
  - [GET Query Parameters and POST JSON fields](#get-query-parameters-and-post-json-fields)
  - [Interaction with Endpoints](#interaction-with-endpoints)
  - [Examples](#examples)
    - [Example 1](#example-1)
      - [Example 1: GET with cql2-text](#example-1-get-with-cql2-text)
      - [Example 1: POST with cql2-json](#example-1-post-with-cql2-json)
    - [Example 2](#example-2)
      - [Example 2: GET with cql2-text](#example-2-get-with-cql2-text)
      - [Example 2: POST with cql2-json](#example-2-post-with-cql2-json)
    - [Example 3: Conjunction with AND](#example-3-conjunction-with-and)
      - [Example 3: AND cql2-text (GET)](#example-3-and-cql2-text-get)
      - [Example 3: AND cql2-json (POST)](#example-3-and-cql2-json-post)
    - [Example 4: Disjunction with OR](#example-4-disjunction-with-or)
      - [Example 4: OR cql2-text (GET)](#example-4-or-cql2-text-get)
      - [Example 4: OR cql2-json (POST)](#example-4-or-cql2-json-post)
    - [Example 5: Property-Property Comparisons](#example-5-property-property-comparisons)
      - [Example 5: GET with cql2-text](#example-5-get-with-cql2-text)
      - [Example 5: POST with cql2-json](#example-5-post-with-cql2-json)
    - [Example 6: Temporal Intersection](#example-6-temporal-intersection)
      - [Example 6: T\_INTERSECTS cql2-text (GET)](#example-6-t_intersects-cql2-text-get)
      - [Example 6: T\_INTERSECTS cql2-json (POST)](#example-6-t_intersects-cql2-json-post)
    - [Example 7: Spatial Intersection in Basic Spatial Operators](#example-7-spatial-intersection-in-basic-spatial-operators)
      - [Example 7: S\_INTERSECTS cql2-text (GET)](#example-7-s_intersects-cql2-text-get)
      - [Example 7: S\_INTERSECTS cql2-json (POST)](#example-7-s_intersects-cql2-json-post)
    - [Example 8: Spatial Intersection in Spatial Operators](#example-8-spatial-intersection-in-spatial-operators)
      - [Example 8: S\_INTERSECTS cql2-text (GET)](#example-8-s_intersects-cql2-text-get)
      - [Example 8: S\_INTERSECTS cql2-json (POST)](#example-8-s_intersects-cql2-json-post)
    - [Example 9: Spatial Intersection Disjunction](#example-9-spatial-intersection-disjunction)
      - [Example 9: S\_INTERSECTS cql2-text (GET)](#example-9-s_intersects-cql2-text-get)
      - [Example 9: S\_INTERSECTS cql2-json (POST)](#example-9-s_intersects-cql2-json-post)
    - [Example 10: Using IS NULL](#example-10-using-is-null)
      - [Example 10: cql2-text (GET)](#example-10-cql2-text-get)
      - [Example 10: cql2-json (POST)](#example-10-cql2-json-post)
    - [Example 11: Using BETWEEN](#example-11-using-between)
      - [Example 11: cql2-text (GET)](#example-11-cql2-text-get)
      - [Example 11: cql2-json (POST)](#example-11-cql2-json-post)
    - [Example 12: Using LIKE](#example-12-using-like)
      - [Example 12: cql2-text (GET)](#example-12-cql2-text-get)
      - [Example 12: cql2-json (POST)](#example-12-cql2-json-post)
    - [Example 13: Using the CASEI Case-insensitive Comparison Function](#example-13-using-the-casei-case-insensitive-comparison-function)
      - [Example 13: cql2-text (GET)](#example-13-cql2-text-get)
      - [Example 13: cql2-json (POST)](#example-13-cql2-json-post)
    - [Example 14: Using the ACCENTI Accent-insensitive Comparison Function](#example-14-using-the-accenti-accent-insensitive-comparison-function)
      - [Example 14: cql2-text (GET)](#example-14-cql2-text-get)
      - [Example 14: cql2-json (POST)](#example-14-cql2-json-post)

## Overview

- **Title:** Filter
- **OpenAPI specification:** [openapi.yaml](openapi.yaml)
- **Conformance Classes:**
  - Filter: `http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/filter`
  - Features Filter: `http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/features-filter`
  - Item Search Filter: `https://api.stacspec.org/v1.0.0-rc.3/item-search#filter`
  - CQL2 Text: `http://www.opengis.net/spec/cql2/1.0/conf/cql2-text`
  - CQL2 JSON: `http://www.opengis.net/spec/cql2/1.0/conf/cql2-json`
  - Basic CQL2: `http://www.opengis.net/spec/cql2/1.0/conf/basic-cql2`
  - Advanced Comparison Operators: `http://www.opengis.net/spec/cql2/1.0/conf/advanced-comparison-operators`
  - Basic Spatial Operators: `http://www.opengis.net/spec/cql2/1.0/conf/basic-spatial-operators`
  - Spatial Operators: `http://www.opengis.net/spec/cql2/1.0/conf/spatial-operators`
  - Temporal Operators: `http://www.opengis.net/spec/cql2/1.0/conf/temporal-operators`
  - Custom Functions: `http://www.opengis.net/spec/cql2/1.0/conf/functions`
  - Arithmetic Expressions: `http://www.opengis.net/spec/cql2/1.0/conf/arithmetic`
  - Array Operators: `http://www.opengis.net/spec/cql2/1.0/conf/array-operators`
  - Property-Property Comparisons: `http://www.opengis.net/spec/cql2/1.0/conf/property-property`
  - Accent and Case-insensitive Comparison: `http://www.opengis.net/spec/cql2/1.0/conf/accent-case-insensitive-comparison`
  - Queryables Transactions: `https://api.stacspec.org/v1.0.0/queryables/extensions/transaction`
- **Scope:** STAC API - Features, STAC API - Item Search
- **[Extension Maturity Classification](https://github.com/radiantearth/stac-api-spec/tree/main/README.md#maturity-classification):** Pilot
- **Dependencies:**
  - [STAC API - Item Search](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/item-search)
  - [STAC API - Features](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/ogcapi-features)
- **Owner**: @philvarner

The Filter extension provides an expressive mechanism for searching based on Item attributes.

This extension references behavior defined in the
[OGC API - Features - Part 3: Filtering and the Common Query Language (CQL2)](https://github.com/opengeospatial/ogcapi-features/tree/master/extensions/filtering) and [Common Query Language (CQL2)
](https://github.com/opengeospatial/ogcapi-features/blob/master/cql2/README.md)
specifications. As of November 2021, these specifications are still in draft status, but rapidly converging on
finalized behavior. Several behaviors have changed since the
last published [draft](https://portal.ogc.org/files/96288), so this spec references the latest revision in the
[OAFeat Part 3 spec's GitHub repo](https://github.com/opengeospatial/ogcapi-features/tree/master/extensions/cql)
and [Common Query Language (CQL2)](https://github.com/opengeospatial/ogcapi-features/blob/master/cql2/README.md)).
Implementers should proceed with implementation, but must be aware that minor changes may be made
before these specs are final.

OAFeat Part 3 CQL2 formally defines the syntax of "CQL2" as both a text format (cql2-text) as an ABNF grammar
(largely similar to the BNF grammar in the General Model for CQL) and a JSON format (cql2-json) as a JSON Schema and
OpenAPI schema. Additionally, it defines a natural
language description of the declarative semantics, which were never well-defined for the original CQL language.
The CQL2 Text format has had long-standing use within
geospatial software (e.g., GeoServer), is not expected to change before final.
OGC CQL2 Text has been previously described in [OGC Filter Encoding](https://www.ogc.org/standards/filter) and
[OGC Catalogue Services 3.0 - General Model](http://docs.opengeospatial.org/is/12-168r6/12-168r6.html#62)
(including a BNF grammar in Annex B). The CQL2 JSON format is newly-defined and has changed significantly during
the draft process, but is believed to be stable now.

It should be noted that the "CQL" referred to here is "CQL2" defined in OGC API - Features - Part 3. This is a related, but
different language to the "classic" OGC CQL defined in the General Model. Relatedly, CQL is **not**
referencing or related two other "CQL" languages,
the [SRU (Search/Retrieve via URL) Contextual Query Language](https://www.loc.gov/standards/sru/cql/index.html) (formerly
known as Common Query Language) or the [Cassandra Query Language](https://cassandra.apache.org/doc/latest/cql/) used by the
Cassandra database.

## Limitations of Item Search

OAFeat defines a limited set of filtering capabilities. Filtering can only be done over a single collection and
with only a single `bbox` (rectangular spatial filter) parameter and a single datetime (instant or interval) parameter.

The STAC Item Search specification extends the functionality of OAFeat in a few key ways:

- It allows cross-collection filtering, whereas OAFeat only allows filtering within a single collection.
  (`collections` parameter, accepting 0 or more collections)
- It allows filtering by Item ID (`ids` parameter)
- It allows filtering based on a single GeoJSON Geometry, rather than only a bbox (`intersects` parameter)

However, it does not contain a formalized way to filter based on arbitrary fields in an Item. For example, there is
no way to express the filter "item.properties.eo:cloud_cover is less than 10". It also does not have a way to logically combine
multiple spatial or temporal filters.

## Filter Expressiveness

This extension expands the capabilities of Item Search and the OAFeat Items resource with
[OAFeat Part 3 CQL2](https://portal.ogc.org/files/96288)
by providing an expressive query language to construct more complex filter predicates using operators that are similar to
those provided by SQL. This extension also supports the Queryables mechanism that allows discovery of what Item fields can be used in
predicates.

CQL2 enables more expressive queries than supported by STAC API Item Search. These include:

- Use of Item Property values in predicates (e.g., `item.properties.eo:cloud_cover`), using comparison operators
- Items whose `datetime` values are in the month of August of the years 2017-2021, using OR and datetime comparisons
- Items whose `geometry` values intersect any one of several Polygons, using `OR` and `S_INTERSECTS`
- Items whose `geometry` values intersect one Polygon, but do not intersect another one, using AND, NOT, and
  S_INTERSECTS

## Conformance Classes

OAFeat Part 3 CQL2 defines several conformance classes that allow implementers to create compositions of
functionality that support whatever expressiveness they need. This allows implementers to incrementally support CQL
syntax, without needing to implement a huge spec all at once.  Some implementers choose not to incur the cost of
implementing functionality they do not need or may not be able to implement functionality that is not supported by
their underlying datastore, e.g., Elasticsearch does not support the spatial predicates required by the
Spatial Operators conformance class, only the `S_INTERSECTS` operator in the Basic Spatial Operators class.

The STAC API Filter Extension reuses the definitions and conformance classes in OAFeat CQL,
adding only the *Item Search Filter* conformance class
(`https://api.stacspec.org/v1.0.0-rc.3/item-search#filter`) to bind
the Filter behavior to the Item Search endpoint.

The implementation **must** support these conformance classes:

- Filter (`http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/filter`) defines the Queryables mechanism and
  parameters `filter-lang`, `filter-crs`, and `filter`.
- Basic CQL2 (`http://www.opengis.net/spec/cql2/1.0/conf/basic-cql2`) defines the basic operations allowed in
  the query language used for the `filter` parameter defined by Filter. This includes logical operators (`AND`, `OR`, `NOT`),
  comparison operators (`=`, `<>`, `<`, `<=`, `>`, `>=`), and `IS NULL`. The comparison operators are allowed against
  string, numeric, boolean, date, and datetime types.
- Item Search Filter (`https://api.stacspec.org/v1.0.0-rc.3/item-search#filter`) binds the Filter and
  Basic CQL2 conformance classes to apply to the Item Search endpoint (`/search`).  This class is the correlate of the OAFeat CQL2 Features
  Filter class that binds Filter and Basic CQL2 to the Features resource (`/collections/{cid}/items`).

The implementation **must** support at least one of the "CQL2 Text" or "CQL2 JSON" conformance classes that
define the CQL2 format used in the filter parameter:

- CQL2 Text (`http://www.opengis.net/spec/cql2/1.0/conf/cql2-text`) defines that the CQL2 Text format is supported by Item Search
- CQL2 JSON (`http://www.opengis.net/spec/cql2/1.0/conf/cql2-json`) defines that the CQL2 JSON format is supported by Item Search

If both are advertised as being supported, it is only required that both be supported for GET query parameters, and that
only that CQL2 JSON be supported for POST JSON requests.  It is recommended that clients use CQL2 Text in GET requests and
CQL2 JSON in POST requests.

The implementation **may** support the OAFeat Part 3 *Features Filter* conformance classes:

- Features Filter (`http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/features-filter`) binds the Filter and
  CQL2 conformance classes to the Features resource(`/collections/{cid}/items`).

For additional capabilities, the following classes may be implemented:

- Advanced Comparison Operators
  (`http://www.opengis.net/spec/cql2/1.0/conf/advanced-comparison-operators`) defines the `LIKE`,
  `BETWEEN`, and `IN` operators. **Note**: this conformance class no longer requires implementing the
  `lower` and `upper` functions.
- Basic Spatial Operators (`http://www.opengis.net/spec/cql2/1.0/conf/basic-spatial-operators`) defines the intersects operator (`S_INTERSECTS`)
  that accepts only a BBOX or POINT parameter.
- Spatial Operators
  (`http://www.opengis.net/spec/cql2/1.0/conf/spatial-operators`) defines a set of operators that
  are part of the Dimensionally Extended Nine-intersection Model (DE-9IM) relation operators
  (`S_CONTAINS`, `S_CROSSES`, `S_DISJOINT`, `S_EQUALS`, `S_INTERSECTS`, `S_OVERLAPS`, `S_TOUCHES`, and `S_WITHIN`),
  and additionally defines the intersects operator (`S_INTERSECTS`) to accept LINESTRING,
  POLYGON, MULTIPOINT, MULTILINESTRING, and MULTIPOLYGON,
  in addition to BBOX and POINT as supported in Basic Spatial Operators.
- Temporal Operators
  (`http://www.opengis.net/spec/cql2/1.0/conf/temporal-operators`) defines several temporal
  operators that provide more expressivity with datetime types than the relative comparison
  operators
  in the Basic CQL2 class.
- Custom Functions (`http://www.opengis.net/spec/cql2/1.0/conf/functions`) defines support
  for function definition and usage.
- Arithmetic Expressions: (`http://www.opengis.net/spec/cql2/1.0/conf/arithmetic`) defines
  support for arithmetic expressions.
- Array Operators: (`http://www.opengis.net/spec/cql2/1.0/conf/array-operators`)
  defines array operators (`A_EQUALS`, `A_CONTAINS`, `A_CONTAINED_BY`, and `A_OVERLAPS`).
- Property-Property Comparisons: (`http://www.opengis.net/spec/cql2/1.0/conf/property-property`)
  allows the use of queryables (e.g., properties) in both positions of a clause, not just in the
  first position. This allows predicates like `property1 = property2` be expressed, whereas the
  Basic CQL2 conformance class only requires comparisons against right-hand-side literals.
- Accent and Case-insensitive Comparison: (`http://www.opengis.net/spec/cql2/1.0/conf/accent-case-insensitive-comparison`)
  defines the UPPER and LOWER functions that can be used for case-insensitive comparison.
- Queryables Transactions: (`https://api.stacspec.org/v1.0.0/queryables/extensions/transaction`)
  allow to update queryables properties on a per catalog and/or per collection basis.

Additionally, if an API implements the OGC API Features endpoint, it is **recommended** that the OAFeat Part 3 Filter,
Features Filter, and Basic CQL2 conformance classes be implemented, which allow use of CQL2 filters against the
OAFeat Part 1 Features endpoint (`/collections/{collectionId}/items`). Note that POST with a JSON body
to the Features resource is not supported, as POST is used by the
[Transaction Extension](https://github.com/stac-api-extensions/transaction) for creating items.

## Getting Started with Implementation

It recommended that implementers start with fully implementing only a subset of functionality. A good place to start is
implementing only the Basic CQL2 conformance class of logical and comparison operators, defining a static Queryables
schema with no queryables advertised and the `additionalProperties` field set to `true`, and
only implementing CQL2 JSON. Following from that can be support for
S_INTERSECTS, defining a static Queryables schema with only the basic Item properties, and
implementing CQL2 Text. From there, other comparison operators can be implemented and a more
dynamic Queryables schema.

Formal definitions and grammars for CQL2 can be found in the
[OAFeat CQL spec](https://github.com/opengeospatial/ogcapi-features/tree/master/cql2) includes
a BNF grammar for CQL2 Text and both a JSON Schema and an OpenAPI specification for CQL2 JSON.
The standalone files are:
  
- [cql2.bnf](https://github.com/opengeospatial/ogcapi-features/blob/master/cql2/standard/schema/cql2.bnf)
- [cql2.json](https://github.com/opengeospatial/ogcapi-features/blob/master/cql2/standard/schema/cql2.json)
- [cql2.yml](https://github.com/opengeospatial/ogcapi-features/blob/master/cql2/standard/schema/cql2.yml)

These projects have or are developing CQL2 support:

- [stac-fastapi-pgstac](https://github.com/stac-utils/stac-fastapi-pgstac) has support for
  CQL2 Text and CQL2 JSON, via using [pygeofilter](https://github.com/geopython/pygeofilter)
  to translate CQL2 Text to CQL2 JSON and processing the CQL2 JSON with
  [pgstac](https://github.com/stac-utils/pgstac)
- [pygeofilter](https://github.com/geopython/pygeofilter) handles both CQL2 Text and CQL2 JSON,
  including the ability to convert from CQL2 Text to CQL2 JSON
- [xtraplatform-spatial](https://github.com/interactive-instruments/xtraplatform-spatial) has support for CQL2 Text and provides an [ANTLR 4 grammer](https://github.com/interactive-instruments/xtraplatform-spatial/tree/master/xtraplatform-cql/src/main/antlr/de/ii/xtraplatform/cql/infra)
- [Geotools](https://github.com/geotools/geotools) has support for [CQL2 text](https://github.com/geotools/geotools/tree/main/modules/library/cql/src/main/java/org/geotools/filter/text/cql2)
- [DotNetStac.Api](https://github.com/Terradue/DotNetStac.Api) has support for [CQL2 JSON](https://github.com/Terradue/DotNetStac.Api/blob/5e7334e95da92ca19f9e9b75c476f362ae24a6da/src/Stac.Api/Models/Cql2/CQL2.cs)
  and implements [Linq extensions](https://github.com/Terradue/DotNetStac.Api/blob/6916507eaf21554872f5c03102d6c144e565e8f5/src/Stac.Api/Models/Cql2/Cql2Linq.cs)
  to build [expressions trees](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/expression-trees) from CQL2.
  It also includes a [default query provider](https://github.com/Terradue/DotNetStac.Api/blob/ea93d783e024e7a8e64dacf06ccb62b94779bd2d/src/Stac.Api/Services/Queryable/StacQueryProvider.cs)
  for STAC object enumerables implemented in [DotNetStac](https://github.com/Terradue/DotNetStac).

Note that the xbib CQL library (JVM) is the OASIS Contextual Query Language, not
OGC CQL, and should not be used to implement this extension, as they are significantly different query languages.
[Stacatto](https://github.com/planetlabs/staccato) uses this for their query language implementation, but it is
not compliant with this extension.

## Queryables

The Queryables mechanism allows a client to discover what terms are available for use when
writing filter expressions. These terms are defined both over the entire catalog
(at `/queryables`) and per collection (at `/collections/{collectionId}/queryables`).
The decision as to which queryables to define for the entire catalog is at the discretion
of the implementer, and can be anywhere between none and the union of all
queryables across all collections.

By default, the queryables are the only terms that may be used
in filter expressions, and if any term is used in expression that is not defined as a queryable an error must be
returned according to OAFeat Part 3. It is recognized that this is a severe restriction in STAC APIs that have highly variable
and dynamic content, so this behavior may be modified by setting the `additionalProperties` attribute in the
queryables definition to `true`.  As such, any syntactically-valid term for a property will be accepted, and the
matching semantics are such that, if an Item does not have an attribute by that name, the value is assumed to be
`null`.  It is recommended to use fully-qualified property names (e.g., `properties.eo:cloud_cover`).

Queryables are advertised via a JSON Schema document retrieved from the `/queryables` endpoint. This endpoint at the root
retrieves queryables that apply to all collections. When used as a subresource of the collection resource
(e.g. /collections/collection1/queryables), it returns queryables pertaining only to that single collection.

It is required to implement both of these endpoints, but for a STAC API, this may simply be a static document of the
STAC-specific fields.  A basic Queryables
definitions for STAC Items should include at least the fields id, collection, geometry, and datetime.

```json
{
  "$schema" : "https://json-schema.org/draft/2019-09/schema",
  "$id" : "https://stac-api.example.com/queryables",
  "type" : "object",
  "title" : "Queryables for Example STAC API",
  "description" : "Queryable names for the example STAC API Item Search filter.",
  "properties" : {
    "id" : {
      "description" : "ID",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/id"
    },
    "collection" : {
      "description" : "Collection",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/collection"
    },
    "geometry" : {
      "description" : "Geometry",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/geometry"
    },
    "datetime" : {
      "description" : "Datetime",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/datetime.json#/properties/datetime"
    }
  },
  "additionalProperties": true
}
```

Fields in Item Properties should be exposed with their un-prefixed names, and not require expressions to prefix them
with `properties`, e.g., `eo:cloud_cover` instead of `properties.eo:cloud_cover`.

There may also be support for finding what queryables are available for a subset of collections, e.g.,
`/queryables?collections=c1,c3`) as described in [this issue](https://github.com/opengeospatial/ogcapi-features/issues/576).

The Landing Page endpoint (`/`) will have a Link with rel `http://www.opengis.net/def/rel/ogc/1.0/queryables` with an href to
the endpoint `/queryables`. Additionally, each Collection resource will have a Link to the queryables resource for that
collection, e.g., `/collections/collection1/queryables`.

The queryables endpoint returns a JSON Schema describing the names and types of terms that may be used in filter expressions.
This response is defined in JSON Schema because it is a well-specified typed schema, but it is not used for validating a JSON
document derived from it. This schema defines the terms that may be used in a CQL2 filter.

These queryable terms are mapped by the service to filter Items. For example, the service may define a queryable with the
name "eo:cloud_cover" that can be used in a CQL2 expression like `eo:cloud_cover <= 10`, with the semantics that only Items where the
`properties.eo:cloud_cover` value was <= 10 would match the filter. The server would then translate this into an appropriate
query for the data within its datastore.

Queryables can be static or dynamically derived. For example, `cloud_cover` might be specified to have a value 0 to 100 or a field
may have a set of enumerated values dynamically determined by an aggregation at runtime.  This schema can be used by a UI or
interactive client to dynamically expose to the user the fields that are available for filtering, and provide a precise group
of options for the values of these terms.

Queryables can also be used to advertise "synthesized" property values. The only requirement in CQL2 is that the property have a type
and evaluate to literal value of that type or NULL. For example, a filter like "Items must have an Asset with an eo:band with
the common_name of 'nir'" can be expressed. A Queryable `assets_bands` could be defined to have a type of array of string and
have the semantics that it contains all of `common_name` values across all assets and bands for an Item. This could then be
filtered with the CQL2 expression `'nir' in assets_bands`. Implementations would then expand this expression into the
appropriate query against its datastore. (TBD if this will actually work or not. This is also related to the upcoming
restriction on property/literal comparisons)

An implementation may also choose not to advertise any queryables, and provide the user with out-of-band information or
simply let them try querying against fields. While this is not allowed according to the OGC CQL2 Queryable spec, it is allowed
in STAC API by the Filter Extension. In this case, the queryables endpoint (`/queryables`) would return this document:

```json
{
  "$schema" : "https://json-schema.org/draft/2019-09/schema",
  "$id" : "https://stac-api.example.com/queryables",
  "type" : "object",
  "title" : "Queryables for Example STAC API",
  "description" : "Queryable names for the example STAC API Item Search filter.",
  "properties" : {
  },
  "additionalProperties": true
}
```

### Updating Queryables

Implementers can choose to allow users to update default queryables on a per Catalog and/ or per Collection basis.
In that case, the `/queryables` endpoints should be callable using the `PUT` method with a payload containing the new queryables object. After updating the endpoint, a server-side process will have to ensure that the newly exposed fields can be queried for the Catalog or Collection or otherwise reject the request.

In addition to adding the PUT method to the queryables endpoint, implementers will also need to add the conformance class `https://api.stacspec.org/v1.0.0/queryables/extensions/transaction` to their API to advertise the added capabilities.

## GET Query Parameters and POST JSON fields

This extension adds three GET query parameters or POST JSON fields to an Item Search request:

- filter-lang:`cql2-text` or `cql2-json`. If undefined, defaults to `cql2-text` for a GET request and `cql2-json` for a POST request.
- filter-crs: recommended to not be passed, but server must only accept `http://www.opengis.net/def/crs/OGC/1.3/CRS84` as
  a valid value, may reject any others
- filter: CQL2 filter expression

API implementations advertise which `filter-lang` values are supported via conformance classes in the Landing Page.
At least one must be implemented, but it is recommended to implement both. If both are advertised as conformance classes, the
server should process either for a GET request, but may only process cql2-json for a POST request. If POST of cql2-text is not
supported, the server must return a 400 error if `filter-lang=cql2-text`.

## Interaction with Endpoints

In an implementation that supports several operator classes, the Landing Page (`/`) must return a document including
at least these values:

```json
{
  "id": "example_stacapi",
  "conformsTo": [
    "http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/core",
    "http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/oas30",
    "http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/geojson",

    "http://www.opengis.net/spec/ogcapi_common-2/1.0/conf/collections",

    "http://api.stacspec.org/v1.0.0/core",
    "http://api.stacspec.org/v1.0.0/item-search",

    "https://api.stacspec.org/v1.0.0-rc.3/item-search#filter"
    "http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/filter",
    "http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/features-filter",
    "http://www.opengis.net/spec/cql2/1.0/conf/cql2-text",
    "http://www.opengis.net/spec/cql2/1.0/conf/cql2-json",
    "http://www.opengis.net/spec/cql2/1.0/conf/basic-cql2",
    "http://www.opengis.net/spec/cql2/1.0/conf/basic-spatial-operators",
    "http://www.opengis.net/spec/cql2/1.0/conf/advanced-comparison-operators"

  ],
  "links": [
    {
      "title": "Search",
      "href": "https://stac-api.example.com/search",
      "rel": "search",
      "type": "application/geo+json"
    },
    {
      "title": "Queryables",
      "href": "https://stac-api.example.com/queryables",
      "rel": "http://www.opengis.net/def/rel/ogc/1.0/queryables",
      "type": "application/schema+json"
    }
  ],
  "stac_extensions": [],
  "stac_version": "1.0.0",
  "type": "Catalog",
}
```

A client can use the link with `"rel": "http://www.opengis.net/def/rel/ogc/1.0/queryables"` to retrieve the queryables.

The Queryables endpoint (`/queryables`) returns something like the following:

```json
{
  "$schema" : "https://json-schema.org/draft/2019-09/schema",
  "$id" : "https://stac-api.example.com/queryables",
  "type" : "object",
  "title" : "Queryables for Example STAC API",
  "description" : "Queryable names for the example STAC API Item Search filter.",
  "properties" : {
    "id" : {
      "description" : "ID",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/id"
    },
    "collection" : {
      "description" : "Collection",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/collection"
    },
    "geometry" : {
      "description" : "Geometry",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/geometry"
    },
    "datetime" : {
      "description" : "Datetime",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/datetime.json#/properties/datetime"
    },
    "eo:cloud_cover" : {
      "description" : "Cloud Cover",
      "$ref": "https://stac-extensions.github.io/eo/v1.0.0/schema.json#/properties/eo:cloud_cover"
    },
    "gsd" : {
      "description" : "Ground Sample Distance",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/instrument.json#/properties/gsd"
    },
    "assets_bands" : {
      "description" : "Asset eo:bands common names",
      "$ref": "https://stac-extensions.github.io/eo/v1.0.0/schema.json#/properties/eo:bands/common_name"
    }
  },
  "additionalProperties": true
}
```

Alternately, the client could retrieve the queryables for a single collection with
`/collections/collections1/queryables`, which may have more queryables than available for the entire catalog, since
there may be queryables that are only relevant to that collection.

Notice in this schema that instead of directly defining the type information about each field, we have instead used the JSON
Schema `$ref` mechanism to refer to a STAC schema definition. This not only allows the reuse of these JSON Schema definitions,
but also binds an arbitrarily-named Queryable to a specific STAC field. For example, in the above we know that the
`eo:cloud_cover` field is referring to the field of the same name in the EO Extension not because they happen to have the same
name, but rather because the `$ref` indicates it. The field could just as well be named "cloud_cover", "CloudCover", or "cc",
and we would still know it filtered on the EO extension `eo:cloud_cover` field. For example, if the queryable was named
"CloudCover", a CQL2 expression using that queryable would look like `CloudCover <= 10`.

While these do seem quite complex to write and understand, keep in mind that query construction will likely be done with a
more ergonomic SDK, and query parsing will be done with the help of a ABNF grammar and OpenAPI schema.

These parameters/fields must be supported by the STAC Item Search endpoint and OAFeat Features resource (`/collections/$collectionId/items`).

## Examples

Note: the GET examples with query parameters are unescaped to make them easier to read.

The GET examples are assuming a call to `GET /search` and the POST examples are assuming a
call to `POST /search`.

The parameter `filter-crs` always defaults to `http://www.opengis.net/def/crs/OGC/1.3/CRS84` for a STAC API, so is not shown
in any of these examples.

### Example 1

This example uses the queryables definition in (Interaction with Endpoints)(#interaction-with-endpoints).

#### Example 1: GET with cql2-text

Note that `filter-lang` defaults to `cql2-text` in this case. The parameter `filter-crs` defaults
to `http://www.opengis.net/def/crs/OGC/1.3/CRS84` for a STAC API.

```text
filter=id='LC08_L1TP_060247_20180905_20180912_01_T1_L1TP' AND collection='landsat8_l1tp'
```

#### Example 1: POST with cql2-json

Note that `filter-lang` defaults to `cql2-json` in this case. The parameter `filter-crs` defaults
to `http://www.opengis.net/def/crs/OGC/1.3/CRS84` for a STAC API.

```json
{
  "filter": {
    "op" : "and",
    "args": [
      {
        "op": "=",
        "args": [ { "property": "id" }, "LC08_L1TP_060247_20180905_20180912_01_T1_L1TP" ]
      },
      {
        "op": "=",
        "args" : [ { "property": "collection" }, "landsat8_l1tp" ]
      }
    ]
  }
}
```

### Example 2

This example uses the queryables definition in [Interaction with Endpoints](#interaction-with-endpoints).

Note that filtering on the `collection` field is relevant in Item Search, since the queries are cross-collection, whereas
OGC API Features filters only operate against a single collection already.

#### Example 2: GET with cql2-text

```text
filter=collection = 'landsat8_l1tp'
  AND eo:cloud_cover <= 10
  AND datetime >= TIMESTAMP('2021-04-08T04:39:23Z')
  AND S_INTERSECTS(geometry, POLYGON((43.5845 -79.5442, 43.6079 -79.4893, 43.5677 -79.4632, 43.6129 -79.3925, 43.6223 -79.3238, 43.6576 -79.3163, 43.7945 -79.1178, 43.8144 -79.1542, 43.8555 -79.1714, 43.7509 -79.6390, 43.5845 -79.5442)))
```

#### Example 2: POST with cql2-json

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "and",
    "args": [
      {
        "op": "=",
        "args": [ { "property": "collection" }, "landsat8_l1tp" ]
      },
      {
        "op": "<=",
        "args": [ { "property": "eo:cloud_cover" }, 10 ]
      },
      {
        "op": ">=",
        "args": [ { "property": "datetime" }, { "timestamp": "2021-04-08T04:39:23Z" } ]
      },
      {
        "op": "s_intersects",
        "args": [
          {
            "property": "geometry"
          },
          {
            "type": "Polygon",
            "coordinates": [
              [
                [43.5845, -79.5442],
                [43.6079, -79.4893],
                [43.5677, -79.4632],
                [43.6129, -79.3925],
                [43.6223, -79.3238],
                [43.6576, -79.3163],
                [43.7945, -79.1178],
                [43.8144, -79.1542],
                [43.8555, -79.1714],
                [43.7509, -79.6390],
                [43.5845, -79.5442]
              ]
            ]
          }
        ]
      }
    ]
  }
}
```

### Example 3: Conjunction with AND

We'll be imagining these as queries against [EarthSearch Sentinel 2
COG](https://stacindex.org/catalogs/earth-search#/Cnz1sryATwWudkxyZekxWx6356v9RmvvCcLLw79uHWJUDvt2?t=items) data.

The queryables defined are as follows:

```json
{
  "$schema" : "https://json-schema.org/draft/2019-09/schema",
  "$id" : "https://stac-api.example.com/queryables",
  "type" : "object",
  "title" : "Queryables for Example STAC API",
  "description" : "Queryable names for the example STAC API Item Search filter.",
  "properties" : {
    "geometry" : {
      "description" : "Geometry",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/item.json#/geometry"
    },
    "datetime" : {
      "description" : "Datetime",
      "$ref": "https://schemas.stacspec.org/v1.0.0/item-spec/json-schema/datetime.json#/properties/datetime"
    },
    "eo:cloud_cover" : {
      "description" : "Cloud Cover",
      "$ref": "https://stac-extensions.github.io/eo/v1.0.0/schema.json#/properties/eo:cloud_cover"
    },
    "sentinel:data_coverage" : {
      "description" : "Sentinel Sat Data Coverage",
      "type": "integer",
      "minimum": 0,
      "maximum": 100
    },
    "sentinel:grid_id" : {
      "description" : "Sentinel Sat Grid ID",
      "type": "string"
    }
  }
}
```

Note that `sentinel:data_coverage` and `sentinel:grid_id` are properties that are not defined in an extension schema, and are intended to
represent vendor-specific properties. Because of this, they are fully specified directly in the JSON Schema. However, it is
recommended that vendor-specific properties be published as part of a well-defined extension schema, so these only represent ones
that have not followed that recommendation.

A sample STAC Item (excluding `assets`) is:

```json
{
  "type": "Feature",
  "stac_version": "1.0.0",
  "stac_extensions": [
    "https://stac-extensions.github.io/eo/v1.0.0/schema.json",
    "https://stac-extensions.github.io/view/v1.0.0/schema.json",
    "https://stac-extensions.github.io/projection/v1.0.0/schema.json"
  ],
  "id": "S2A_60HWB_20201111_0_L2A",
  "bbox": [ 176.9997779369264, -39.83783732066656, 178.14624317719924, -38.842842449352425],
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[176.9997779369264, -39.83783732066656],[176.99978104582647,-38.84846679951431],
            [178.14624317719924, -38.842842449352425],[177.8514661209684,-39.83471270154608],
            [176.9997779369264, -39.83783732066656]]]
  },
  "properties": {
    "datetime": "2020-11-11T22:16:58Z",
    "platform": "sentinel-2a",
    "constellation": "sentinel-2",
    "instruments": ["msi"],
    "gsd": 10,
    "view:off_nadir": 0,
    "proj:epsg": 32760,
    "sentinel:utm_zone": 60,
    "sentinel:latitude_band": "H",
    "sentinel:grid_square": "WB",
    "sentinel:sequence": "0",
    "sentinel:product_id": "S2A_MSIL2A_20201111T221611_N0214_R129_T60HWB_20201111T235959",
    "sentinel:data_coverage": 78.49,
    "eo:cloud_cover": 0.85,
    "sentinel:valid_cloud_cover": true,
    "created": "2020-11-12T02:08:31.563Z",
    "updated": "2020-11-12T02:08:31.563Z"
  }
}
```

One problem in working with Sentinel-2 data is that many scenes only contain a tiny "sliver" of data, where the satellite's
recording path intersection only a corner of a grid square. This examples shows
Show me all imagery that has low cloud cover (less than 10), and high data coverage (50), as I'd like a cloud free image that is not just
a tiny sliver of data.

#### Example 3: AND cql2-text (GET)

```text
filter=sentinel:data_coverage > 50 AND eo:cloud_cover < 10
```

#### Example 3: AND cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "and",
    "args": [
      {
        "op": ">",
        "args": [ { "property": "sentinel:data_coverage" }, 50 ]
      },
      {
        "op": "<",
        "args": [ { "property": "eo:cloud_cover" }, 10 ]
      }
    ]
  }
}
```

An 'or' is also supported, matching if either condition is true. Though it's not a sensible query you could get images that have full data
coverage or low cloud cover.

### Example 4: Disjunction with OR

This uses the same queryables as Example 3.

#### Example 4: OR cql2-text (GET)

```text
filter=sentinel:data_coverage > 50 OR eo:cloud_cover < 10
```

#### Example 4: OR cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "or",
    "args": [
      {
        "op": ">",
        "args": [ { "property": "sentinel:data_coverage" }, 50 ]
      },
      {
        "op": "<",
        "args": [ { "property": "eo:cloud_cover" }, 10 ]
      }
    ]
  }
}
```

### Example 5: Property-Property Comparisons

The Property-Property Comparisons conformance class permits queryable properties to be used on either side
of an operator. This is a generic example, as there are few STAC properties
that are comparable in a meaningful way. This example uses a contrived example of two proprietary properties,
`prop1` and `prop2` that are of the same type.

This queryables JSON Schema is used in these examples:

```json
{
  "$schema" : "https://json-schema.org/draft/2019-09/schema",
  "$id" : "https://stac-api.example.com/queryables",
  "type" : "object",
  "title" : "Queryables for Example STAC API",
  "description" : "Queryable names for the example STAC API Item Search filter.",
  "properties" : {
    "prop1" : {
      "description" : "Property 1",
      "type": "integer"
    },
    "prop2" : {
      "description" : "Property 2",
      "type": "integer"
    }
  }
}
```

#### Example 5: GET with cql2-text

```text
filter=prop1 = prop2
```

#### Example 5: POST with cql2-json

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "=",
    "args": [
      { "property": "prop1" },
      { "property": "prop2" }
    ]
  }
}
```

### Example 6: Temporal Intersection

This uses the same queryables as Example 3.

The only temporal operator required is `T_INTERSECTS`. This is effectively that the datetime or interval operands
have any overlap between them.

#### Example 6: T_INTERSECTS cql2-text (GET)

```text
filter=T_INTERSECTS(datetime, INTERVAL('2020-11-11T00:00:00Z', '2020-11-12T00:00:00Z'))
```

#### Example 6: T_INTERSECTS cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "t_intersects",
    "args": [
      { "property": "datetime" },
      { "interval" : [ "2020-11-11T00:00:00Z", "2020-11-12T00:00:00Z"] }
    ]
  }
}
```

### Example 7: Spatial Intersection in Basic Spatial Operators

The only spatial operator that must be implemented for Basic Spatial Operators
is `S_INTERSECTS` supporting BBOX and POINT. This has the same semantics as provided
by the Item Search `intersects` parameter.  The `cql2-text` format uses WKT geometries and the `cql2-json`
format uses GeoJSON geometries.

#### Example 7: S_INTERSECTS cql2-text (GET)

```text
filter=S_INTERSECTS(geometry,POINT(-77.0824 38.7886))
```

#### Example 7: S_INTERSECTS cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "s_intersects",
    "args": [
      { "property": "geometry" } ,
      {
        "type": "Point",
        "coordinates": [-77.0824, 38.7886]
      }
    ]
  }
}
```

### Example 8: Spatial Intersection in Spatial Operators

The Spatial Operators extends the Basic Spatial Operators by adding support for additional
geometries to the `S_INTERSECTS` parameter. This has the same semantics as provided
by the Item Search `intersects` parameter.  The `cql2-text` format uses WKT geometries and the `cql2-json`
format uses GeoJSON geometries.

#### Example 8: S_INTERSECTS cql2-text (GET)

```text
filter=S_INTERSECTS(geometry,POLYGON((-77.0824 38.7886,-77.0189 38.7886,-77.0189 38.8351,-77.0824 38.8351,-77.0824 38.7886)))
```

#### Example 8: S_INTERSECTS cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "s_intersects",
    "args": [
      { "property": "geometry" } ,
      {
        "type": "Polygon",
        "coordinates": [[
            [-77.0824, 38.7886], [-77.0189, 38.7886],
            [-77.0189, 38.8351], [-77.0824, 38.8351],
            [-77.0824, 38.7886]
        ]]
      }
    ]
  }
}
```

### Example 9: Spatial Intersection Disjunction

One limitation of the `intersects` parameter is that only a single geometry may be provided. While most
GeoJSON geometries can be combined to form a composite (e.g., multiple Polygons can be combined to form a
MultiPolygon), this is much easier to do in the query by combining `S_INTERSECTS` predicates with the `OR`
logical operator.

#### Example 9: S_INTERSECTS cql2-text (GET)

```text
filter=S_INTERSECTS(geometry,POLYGON((-77.0824 38.7886,-77.0189 38.7886,-77.0189 38.8351,-77.0824 38.8351,-77.0824 38.7886))) OR S_INTERSECTS(geometry,POLYGON((-79.0935 38.7886,-79.0290 38.7886,-79.0290 38.8351,-79.0935 38.8351,-79.0935 38.7886)))
```

#### Example 9: S_INTERSECTS cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "or" ,
    "args": [
      {
        "op": "s_intersects",
        "args": [
          { "property": "geometry" } ,
          {
            "type": "Polygon",
            "coordinates": [[
              [-77.0824, 38.7886], [-77.0189, 38.7886],
              [-77.0189, 38.8351], [-77.0824, 38.8351],
              [-77.0824, 38.7886]
            ]]
          }
        ]
      },
      {
        "op": "s_intersects",
        "args": [
          { "property": "geometry" } ,
          {
            "type": "Polygon",
            "coordinates": [[
              [-79.0935, 38.7886], [-79.0290, 38.7886],
              [-79.0290, 38.8351], [-79.0935, 38.8351],
              [-79.0935, 38.7886]
            ]]
          }
        ]
      }
    ]
  }
}
```

### Example 10: Using IS NULL

One of the main use cases for STAC API is doing cross-collection query. Commonly, this means that items have
different sets of properties. For example, a collection of Sentinel 2 data may have a property
`sentinel:data_coverage` and a collection of Landsat 8 data may have a corresponding property
`landsat:coverage_percent`, both representing what percentage of a given gridded scene actually contains
data.  However, we many also want to also include in our result items that do not have a value defined for
either of those properties.

#### Example 10: cql2-text (GET)

```text
filter=sentinel:data_coverage > 50 OR landsat:coverage_percent < 10 OR (sentinel:data_coverage IS NULL AND landsat:coverage_percent IS NULL)
```

#### Example 10: cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "or",
    "args": [
      {
        "op": ">",
        "args": [ { "property": "sentinel:data_coverage" }, 50 ]
      },
      {
        "op": "<",
        "args": [ { "property": "landsat:coverage_percent" }, 10 ]
      },
      {
        "op": "and",
        "args": [
          {
            "op": "isNull",
            "args": [ { "property": "sentinel:data_coverage" } ]
          },
          {
            "op": "isNull",
            "args": [ { "property": "landsat:coverage_percent" } ]
          }
        ]
      }
    ]
  }
}
```

### Example 11: Using BETWEEN

The BETWEEN operator allows for checking if a numeric value is within a specified inclusive range.

#### Example 11: cql2-text (GET)

```text
filter=eo:cloud_cover BETWEEN 0 AND 50
```

#### Example 11: cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "between",
    "args": [
      { "property": "eo:cloud_cover" },
      0, 50
    ]
  }
}
```

### Example 12: Using LIKE

The LIKE operator allows for pattern-based string matching.

#### Example 12: cql2-text (GET)

```text
filter=mission LIKE 'sentinel%'
```

#### Example 12: cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "like",
    "args": [
      { "property": "mission" },
      "sentinel%"
    ]
  }
}
```

### Example 13: Using the CASEI Case-insensitive Comparison Function

The predefined function `CASEI` allows for case-insensitive comparisons. This function is
defined in the Accent and Case-insensitive Comparison conformance class.

In the example using 'Straße', both the capitalized 'S' and Eszett ('ß') are converted to an
insensitive representation whereby the expressions `CASEI('Straße')`, `CASEI('straße')`,
`CASEI('Strasse')`, and `CASEI('strasse')` are all equal.

#### Example 13: cql2-text (GET)

```text
filter=CASEI(provider) = CASEI('coolsat')
```

```text
filter=CASEI(provider) = CASEI('Straße')
```

#### Example 13: cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "=",
    "args": [
      { 
        "function" : "casei", 
        "args" : [ { "property": "provider" } ]
      },
      { 
        "function" : "casei", 
        "args" : [ "coolsat" ]
      }
    ]
  }
}
```

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "=",
    "args": [
      { 
        "function" : "casei", 
        "args" : [ { "property": "provider" } ]
      },
      { 
        "function" : "casei", 
        "args" : [ "Straße" ]
      }
    ]
  }
}
```

### Example 14: Using the ACCENTI Accent-insensitive Comparison Function

The predefined function `ACCENTI` allows for accent-insensitive comparisons. This function is
defined in the Accent and Case-insensitive Comparison conformance class. In the example below,
`ACCENTI('tiburon')` and `ACCENTI('tiburón')` evaluate to be equal.

#### Example 14: cql2-text (GET)

```text
filter=ACCENTI(provider) = ACCENTI('tiburón')
```

#### Example 14: cql2-json (POST)

```json
{
  "filter-lang": "cql2-json",
  "filter": {
    "op": "=",
    "args": [
      { 
        "function" : "accenti", 
        "args" : [ { "property": "provider" } ]
      },
      { 
        "function" : "accenti", 
        "args" : [ "tiburón" ]
      }
    ]
  }
}
```

### Example 15: Using the IN List predicate

The predefined function `IN` allows for checking if a value is in a list of values.

#### Example 15: cql2-text (GET)

```text
filter=keywords IN ('fire', 'forest', 'wildfire')
```

#### Example 15: cql2-json (POST)

```json
{
    "filter-lang": "cql2-json",
    "filter": {
        "op": "in",
        "args": [
            {
                "property": "keywords"
            },
            [
                "fire",
                "forest",
                "wildfire"
            ]
        ]
    }
}
```
