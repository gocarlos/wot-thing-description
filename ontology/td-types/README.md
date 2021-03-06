# TD Data Schema Definition

The following terms are defined in an RDFS vocabulary that conceptually aligns with JSON Schema.
See [td-types.ttl](./td-types.ttl).

Schema definitions can also be derived as OWL classes. An experimental JS script is available
[here](https://github.com/vcharpenay/wot/tree/master/proposals/type-system/schema2owl.js).

| RDF Term | JSON Schema | Comment |
| --- | --- | --- |
| rdf:type | type | |
| td:DataSchema | - | schema definition |
| td:DataField | - | object key/value pair |
| td:Object | object | |
| td:Array | array | |
| td:Number | number | ~ union of xsd:decimal, xsd:float, xsd:double |
| td:Integer | integer | ~ xsd:decimal |
| td:String | string | ~ xsd:string |
| td:Boolean | boolean | ~ xsd:boolean |
| td:items | items | |
| td:minItems | minItems | |
| td:maxItems | maxItems | |
| td:enum |enum | |
| td:field | properties | |
| td:name | - | |
| td:value | - | |
| td:required | required | |
| td:anyOf | anyOf | |
| td:someOf | someOf | |
| td:oneOf | oneOf | |
| xsd:minInclusive | minimum | |
| xsd:maxInclusive | maximum | |

## Examples

The following examples were first presented in issue #13 (as JSON schema definitions).

Door state (see also [Turtle](./ex-door.ttl)):
```json
{
    "@type": "Object",
    "description": "Whether a door is open or closed",
    "field": [
        {
            "name": "door",
            "value": {
                "enum": ["Open", "Closed"]
            }
        }
    ]
}
```

Humidity value (see also [Turtle](./ex-humidity.ttl)):
```json
{
    "@type": "Object",
    "description": "Humidity as a percentage",
    "field": [
        {
            "name": "humidity",
            "value": {
                "@type": "Number",
                "minimum": 0,
                "maximum": 100
            }
        }
    ]
}
```

Supported device modes (see also [Turtle](./ex-modes.ttl)):
```json
{
    "@type": "Object",
    "description": "Collection of modes supported by a device",
    "field": [
        {
            "name": "supportedModes",
            "items": { "@type": "String" }
        }
    ]
}
```

Sensor reading (see also [Turtle](./ex-reading.ttl)):
```json
{
    "@type": "Object",
    "description": "Generic sensor reading",
    "field": [
        {
            "name": "reading",
            "value": {
                "anyOf": [
                    { "@type": "Number" },
                    { "@type": "String" }
                ]
            }
        }
    ]
}
```

Binary switch (see also [Turtle](./ex-switch.ttl)):
```json
{
    "@type": "Object",
    "description": "An on/off power switch",
    "field": [
        {
            "name": "on",
            "value": {
                "@type": "Integer"
            }
        }
    ]
}
```

Weather station (see also [Turtle](./ex-weather.ttl)):
```json
{
    "@type": "Object",
    "description": "Weather station",
    "field": [
        {
            "name": "wind",
            "value": {
                "@type": "Object",
                "field": [
                    {
                        "name": "speed",
                        "value": { "@type": "Number" }
                    },
                    {
                        "name": "direction",
                        "value": { "@type": "Integer" }
                    }
                ]
            }
        },
        {
            "name": "temperature",
            "value": { "@type": "Number" }
        },
        {
            "name": "humidity",
            "value": { "@type": "Integer" }
        }
    ]
}
```