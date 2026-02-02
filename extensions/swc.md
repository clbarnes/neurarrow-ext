# net.clbarnes.swc

- Extension version: 0.1
- Neurarrow version: >=0.2

This extension allows lossless conversion from
[SWC files](https://www.sciencedirect.com/science/article/abs/pii/S0165027098000910?via%3Dihub)
[as documented here](http://www.neuronland.org/NLMorphologyConverter/MorphologyFormats/SWC/Spec.html),
with some ambiguities resolved by the [SWC+ documentation](https://neuroinformatics.nl/swcPlus/).

## `skeletons` extension

### Schema metadata

#### `net.clbarnes.swc:version`

- encoding: string
- required: yes

The version of this extension used when writing the table.

#### `net.clbarnes.swc:header:*`

- encoding: string
- required: no

Text content of all lines prior to the first non-empty, non-commented line for a single SWC file,
with all leading `#` characters and any shared whitespace trimmed.

i.e. a SWC file representing fragment `1234` starting

```swc
# here is a long
# description of

# the nature of this file
1 2 1.0 2.0 3.0 4.0 -1
# here's a comment
```

MUST produce a header like

```text
here is a long
description of
the nature of this file
```

under the key `net.clbarnes.swc:header:1234`.

Note that the original publication and the later SWC+ specification both impose some structure on the header;
here it is treated as raw text.

#### `net.clbarnes.swc:type:*`

- encoding: string
- required: no

Structure/ neuronal compartment type identifier mapping.
The last element in the key name MUST be a signed decimal integer.
The value is a string describing the structure.

For example, a JSON representation of the `type` map used by [neuromorpho.org](https://neuromorpho.org/myfaq.jsp) would look like

```json
{
    "net.clbarnes.swc:type:-1": "root",
    "net.clbarnes.swc:type:0": "undefined",
    "net.clbarnes.swc:type:1": "soma",
    "net.clbarnes.swc:type:2": "axon",
    "net.clbarnes.swc:type:3": "basal dendrite",
    "net.clbarnes.swc:type:4": "apical dendrite",
    "net.clbarnes.swc:type:5": "custom",
    "net.clbarnes.swc:type:6": "unspecified neurite",
    "net.clbarnes.swc:type:7": "glia process"
}
```

Skeletons in the same context SHOULD use the same `type` mapping.

### Fields

#### `net.clbarnes.swc:type_id`

- type: `int64`
- required: yes
- nullable: no

Structure/ neuronal compartment type enumeration.
Refer to the `net.clbarnes.swc:type:*` schema metadata.

### Implementation notes

The `radius` field is optional in neurarrow, but required in SWC.
Missing radii SHOULD be filled in with `-1.0` when converting from neurarrow to SWC.
Negative radii MUST be recorded as `null` when converting from SWC to neurarrow.

SWC files conventionally use micrometer units.
