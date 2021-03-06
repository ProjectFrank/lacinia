## 0.19.0 -- UNRELEASED

Lacinia now includes support for GraphQL subscriptions.

Lacinia no longer catches and reports exceptions inside field resolvers.

The :decorator option to `com.walmartlabs.lacinia.schema/compile` has been
removed. This is a feature, added in 0.17.0, that can be better implemented
in application code.

## 0.18.0 -- 19 June 2017

`com.walmartlabs.lacinia.schema/tag-with-type` now uses metadata in the majority of cases
(as it did in 0.16.0), resorting to a wrapper type only when
the value is a Java object that doesn't support metadata.

Queries with repeated identical fields (same alias and arguments) will now be merged together
along with their subselections.

Fixed Selections API functions throwing a NullPointerException on Introspective meta fields.

Upgraded to `clojure-future-spec` 1.9.0-alpha17.

[Closed Issues](https://github.com/walmartlabs/lacinia/milestone/5?closed=1)

## 0.17.0 -- 22 May 2017

Lacinia now better implements the specification, in terms of parsing
and serializing scalars.

The default mapping from field name to field resolver has simplified;
it is now a direct mapping, without converting underscores to dashes.
The old behavior is still available via an option to
`com.walmartlabs.lacinia.schema/compile`.

The function `com.walmartlabs.lacinia.schema/tag-with-type` has changed; it
now returns a special wrapper value (rather than the same value with
different metadata). This is to allow resolved values that do not
support metadata, such as Java objects.

The related function `com.walmartlabs.lacinia.schema/type-tag` has been removed.

Please update your applications carefully.

`compile` now has a new option, `:decorator`.
The decorator is a callback applied to all non-default field resolvers.
The primary use case is to adapt the return value of a field resolver,
for example, from a core.async channel to a Lacinia ResolverResult.

New function: `com.walmartlabs.lacinia.parser/operations`: extracts
from a parsed query the type (mutation or query) and the set of
operations.

Several new *experimental* functions were added to `com.walmartlabs.lacinia.executor` to
expose details about the selections tree; these functions can be invoked
from a field resolver to preview what fields will be selected below
the field.

[Closed Issues](https://github.com/walmartlabs/lacinia/milestone/4)

## 0.16.0 -- 3 May 2017

The function `com.walmartlabs.lacinia.schema/as-conformer` is now public.

New function `com.walmartlabs.lacinia/execute-parsed-query-async`.

Lacinia can now, optionally, collect timing information about
field resolver functions. This information is returned in the
`:extensions :timings` key of the response.

[Closed Issues](https://github.com/walmartlabs/lacinia/milestone/3?closed=1)

## 0.15.0 -- 19 Apr 2017

Field resolvers can now operate synchronously or asynchronously.

This release fleshes out the Lacinia type system to be fully compliant with the
GraphQL type system.
Previously, there were significant limitations when combining `list` and `non-null` modifiers on types.

The internal representation of enum values has changed from String to Keyword.
You will now see a Keyword, not a String, supplied as the value of an enum-typed argument
or variable.
You may need to make small changes to your field resolvers.

[Closed Issues](https://github.com/walmartlabs/lacinia/milestone/2?closed=1)


## 0.14.0 -- 29 Mar 2017

This release adds some very small performance improvements.

Field resolver functions may now return sets (where the schema type is a list).
Previously this generated a runtime error.

There is a change to the signature of the
`com.walmartlabs.lacinia.executor/execute-query` function
that will not affect the majority of users.

We have removed an unused dependency on `org.clojure/tools.macro`.

And, of course, smaller fixes and improvements to the documentation.

[Closed Issues](https://github.com/walmartlabs/lacinia/milestone/1?closed=1)


## 0.13.0 -- 15 Mar 2017

Lucky 13 is our first publicly available version of Lacinia.
It is still alpha and still subject to change, however.
