# 1.8.0

+ Add GHC 8.4 support (thanks @4e6 !).
+ Drop GHC 7.10 support.
+ Fix JSON Pointer resolution error.

# 1.8.0

+ Allow HTTPS references (thanks @creichert!).
+ Use `safe-exceptions` to eliminate the risk of catching asynchronous exceptions.

# 1.7.2

+ Remove upper bounds.

# 1.7.1

+ Bump http-types.

# 1.7.0

+ Test with GHC 8.2. Drop GHC 7.8.
+ Rework `allUniqueValues` related utility functions.

# 1.6.3

+ Bump hjsonpointer and QuickCheck.

# 1.6.2

+ Bump aeson.

# 1.6.1

+ Fix Haddocks.

# 1.6.0

+ Fix defect where validators alongside "$ref" weren't ignored.

+ Fix defect where local references would fail if an "id" key had set resolution scope to start from a different document.

+ Vendor latest tests.

+ Remove `ReferencedSchemas`.

+ Create `Scope` to hold information that changes during validation.

+ Use a sum type for "type" values. Thanks to Philip Weaver (GitHub @pheaver).

# 1.5.0.1

+ Raise test dep upper bounds.

# 1.5.0.0

+ Report details of `"required"` validator failure.
+ Bump `directory`.

# 1.4.0.0

+ Rename `Data.JsonSchema.*` modules to `JSONSchema.*`.
+ Rename `Data.Validator.*` modules to `JSONSchema.Validator.*`.

# 1.3.0.1

+ Bump `vector`.

# 1.3.0.0

+ Rewrite failure messages.

We used to return a list of every failed validator, no matter how far it was buried within subschemas of the original schema.

Now we return a tree of failure messages, so that if the first schema had only three validators, then no more than three top level failures will be returned.

+ Move the code to parse each validator from JSON from `Data.Validator.Draft4` into the validators' modules themselves.

+ Switch from Prelude to Protolude.

+ Switch `Data.JsonSchema.Fetch` from lazy to strict bytestrings.

# 1.2.0.2

+ Bump hspec.

# 1.2.0.1

+ Switch to hspec for tests.

# 1.2.0.0

+ Return `AdditionalPropertiesObject` error correctly (was mistakenly returning `AdditionalItemsObject` instead.
+ Don't silence errors resulting from subschemas of "anyOf" or "oneOf".

# 1.1.0.1

+ Bump `aeson` and `hjsonpointer`.

# 1.1.0.0

+ Rename `schemaForSchemas` to `metaSchema` and `schemaForSchemasBytes` to `metaSchemaBytes`.

# 1.0.0.0

## Bug fixes:

+ Fix JSON Pointer bug. Pointers were being built in reverse order and so were totally invalid.
+ Use `.:!` instead of `.:?` to parse the draft 4 schema. The only way to omit optional fields in JSON Schema Draft 4 is to omit them entirely, `"null"` can't be used for this.

## API Changes:

+ Add referenced schema loop detection.
+ Add a new `referencesValidity` function.
+ `checkSchema` now checks referenced schema's validity in addition to the starting schema's validity. This change bubbles up to the one-step validation functions as well.
+ Switch most of the fetching code to use `URISchemaMap` instead of `ReferencedSchemas`. It didn't need to know about the more complicated data type.
+ Rething failure related names. Change `Invalid` to `Failure`, add a new `Invalid` type alias which is only used for final results.
+ Failures now include the failing part of the data as well as a JSON Pointer to it, so you don't have to worry about resolving the pointer.

## Fundamental Changes:

+ Make `Fail` (previously `Failure`) an instance of `Functor`.
+ Add a `Validator` data type which is an instance of `Profunctor`.
+ Add a `Spec` data type for collections of `Validators`.

## General:

+ Switch from 2 to 4 space indentation.
+ Update the vendored JSON Schema Test Suite.

# 0.10.0.3

+ Bump http-client.

# 0.10.0.2

+ Enable GHC 8.

# 0.10.0.1

+ Fix .cabal file.

# 0.10

+ Rewrite fetching internals.
+ Fix reference resolution defects, add more tests.
+ Switch to a Perl style regex library, which is closer to ECMAScript regexes than the previous Posix style one.
+ Add one-step validation functions ('fetchFilesystemAndValidate' and 'fetchHTTPAndValidate').
+ Alias the validation failure type exported by 'Data.JsonSchema.Draft4' to
'Invalid', change its field names.

# 0.9

+ Partial rewrite. The API of the library has changed, see the examples
folder for how to use the new one.

+ Users of the library can now write schemas in Haskell as well as JSON.

# 0.8

+ Improve scope updating and resolving.
+ Rename RawSchema's _rsObject field to _rsData.
+ Make RawSchema's _rsURI field a Maybe. This way schemas without a starting URI can say so explicitly with Nothing instead of with "".
+ Rename Graph to SchemaGraph. Declare it with data instead of type. Give it a field referencing the starting schema. This field is used to find the curent schema if no URI is in scope and a self-referencing $ref is found (e.g. "#").
+ Change the order of the last two arguments to fetchReferencedSchemas.

# 0.7.1

+ Support GHC 7.8 again.

# 0.7

Change error type from Text to ValidationFailure.

Revert the 0.6 changes to validate. Also switch from Vector to list. Validate is now:
  Schema err -> Value -> [ValidationFailure err]

Add fetchReferencedSchemas', which lets the user provide their own MonadIO function to be used when fetching schemas. This lets them do things like only fetch schemas from particular domains.

# 0.6

Break the API so the library doesn't induce boolean blindness.

Change validate
  was: Schema -> Value -> Vector ValErr
  now: Schema -> Value -> Either (Vector ValErr) Value

Change Schema
  was: type Schema = Vector Validator
  now: newtype Schema = Schema { _unSchema :: [Validator] }

# 0.5.3

+ Switch from http-conduit to http-client.

# 0.5.2

+ Add convenience function for validating and compiling draft 4 schemas simultaneously.

# 0.5.1

+ Switch from wreq to http-conduit; drop lens dependency.

# 0.5

+ Start changelog.
+ Rename Utils.hs to Helpers.hs.
+ Move all non-ValidatorGen functions in Validators.hs to Helpers.hs.
+ Various touchups.
