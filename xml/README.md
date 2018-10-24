# XML


## XML File format:

* [Schema definition](schema/full_import.xsd)
* [Example of full import file](examples/full_import.xml)

**Please read general notes about file format in main [README](../README.md) file.**

## Notes on the XML schemas

Due to the limitations of W3C XSD 1.0 it cannot be validated that there is an `email` element if there's no `employee_id` or the `employee_id` is empty. Please read more about the importance of these fields in the [general notes](../README.md).

## Validation tools

Local validation: [Apache Xerces2](http://xerces.apache.org/xerces2-j/)

Online tool: [FreeFormatter.com XML validator](https://www.freeformatter.com/xml-validator-xsd.html)