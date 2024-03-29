## GPX Extensions

### gpx_ico/0/2

Links to the illustrative schema (XSD), plus examples of usage (GPX + GPZ):

- [gpx_ico.xsd](gpx_ico.xsd)
- [icon-example-1.gpx](icon-example-1.gpx) or [icon-example-1.gpz](icon-example-1.gpz)
- [icon-example-2.gpx](icon-example-2.gpx) or [icon-example-2.gpz](icon-example-2.gpz)
- [icon-example-3.gpx](icon-example-3.gpx) or [icon-example-3.gpz](icon-example-3.gpz)
- [icon-example-4.gpx](icon-example-4.gpx) or [icon-example-4.gpz](icon-example-4.gpz)

All of the examples are GPX 1.1 compliant and can be validated against the strict [schema](https://www.topografix.com/GPX/1/1/gpx-strict.xsd).



### Change History

#### 0.2

- Switch concept from `<sym>` and `<type>` to dedicated `<icon>` element.
- Rename `<path href="...">` to `<folder url="...">`.
- Support `<folder>` elements within `<icon>` elements.

#### 0.1

- Initial draft.
