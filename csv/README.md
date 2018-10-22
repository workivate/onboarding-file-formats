# Comma-separated Values (CSV)

A comma-separated values file is a text file that contains one record per line. A record contains a constant number of fields that are separated by the comma character (`,`). The first row of the file may contain the headers for the appropriate fields.

[RFC 4180](https://tools.ietf.org/html/rfc4180) proposes a specification for the CSV format. The expected details of the format in our case is:
  * Fields delimited by `,`
  * Fields enclosed by `"` for fields where the value contains whitespace or commas.

## CSV File format:

* [Schema definition](schema/full_import.csvs)
* [Example of full import file](examples/full_import.csv)

**Please read general notes about file format in main [README](../README.md) file.**

## Notes about schema definition

Our CSV schema has been defined with an unofficial CSV Schema draft specification as defined here: http://digital-preservation.github.io/csv-schema/csv-schema-1.0.html

There is also open source validation tool: https://github.com/digital-preservation/csv-validator which can be used to validate generated documents against schema.
