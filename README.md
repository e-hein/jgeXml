# jgeXml - The Just-Good-Enough XML Parser

[![Build status](https://travis-ci.org/MikeRalphson/jgeXml.svg?branch=master)](https://travis-ci.org/MikeRalphson/jgeXml)
[![Join the chat at https://gitter.im/MikeRalphson/jgeXml](https://badges.gitter.im/MikeRalphson/jgeXml.svg)](https://gitter.im/MikeRalphson/jgeXml?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Share on Twitter][twitter-image]][twitter-link]
[![Follow on Twitter][twitterFollow-image]][twitterFollow-link]

jgeXml provides event-driven routines to parse XML 1.0 (both pull and push modes are supported), to write XML (documents or fragments) and to convert between XML and JSON (one way JSON to YAML conversion is also supported).

The code has no dependencies on other modules or native libraries.

## Events (stateCodes)

```
sDeclaration
sElement
sAttribute
sValue
sEndElement
sContent
sComment
sProcessingInstruction
sCData
sDocType
sError
sEndDocument
```

No event is generated for ignoreable whitespace, unlike SAX. Empty elements are normalised into sElement/sEndElement pairs.

## Notes

jgeXml is a non-validating parser. It attempts to report if the XML is well-formed or not.

Both when reading and writing, attributes follow after the element event, and in the order they are given in the source.

When converting to JSON, the attributePrefix (to avoid name clashes with child elements) is configurable per parse.

Child elements can be represented as properties or objects in JSON.

The parser by default treats all content as strings when converting to JSON, optionally data can be coerced
to primitive numbers or null values.

Experimental JSONPath and JSONT utilities are under development.

## Limitations

XML/YAML *generation* is probably not thread safe.

jgeXml is currently schema agnostic and staunchly atheist when it comes to DTDs. It can parse XML documents with schema information, but it is up to the
consumer to interpret the namespace portions of element names. It can parse internal DTDs, but does nothing with them.
xmlWrite minimally supports DTDs but you must build them and the DOCTYPE yourself.

It can parse and transform XSD files as XML, conversion to JSON schema is planned.

The parser is string-based; to process streams, read the data into a string first. It may be memory intensive on large documents.

## Examples

See testx2x for parsing XML to XML, testx2j for parsing XML to JSON, testj2x for converting JSON to XML, testj2y for converting JSON to YAML, testfrag for writing XML fragments, testjpath for JSONPath examples, testjsont for JSONT examples and pullparser / pushparser for how to set up and run the parser.

[twitter-image]: https://img.shields.io/twitter/url/http/PermittedSoc.svg?style=social
[twitter-link]: https://twitter.com/share?source=tweetbutton&text=jgeXml%20parser%20Via%20%40PermittedSoc&url=https%3A%2F%2Fgithub.com%2FMikeRalphson%2FjgeXml
[twitterFollow-image]: https://img.shields.io/twitter/follow/PermittedSoc.svg?style=social
[twitterFollow-link]: https://twitter.com/intent/follow?screen_name=PermittedSoc
