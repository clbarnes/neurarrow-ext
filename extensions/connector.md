# net.clbarnes.connector

- Extension version: 0.2
- Neurarrow version: >=0.2

Point annotations associated with one or more connections.
Connections have a many-to-one relationship with connectors.

## New schema: `net.clbarnes.connectors`

### Parent schemas

- [Spatial](https://neurarrow.readthedocs.io/en/stable/schemas/spatial.html)

### Schema metadata

#### `net.clbarnes.connectors:version`

- encoding: string
- required: yes

The version of this extension used when writing the table.

### Fields

#### `connector_id`

- type: `uint64`
- required: yes
- nullable: no

ID of the connector, unique within this context.

#### `x`, `y`, `z`

- type: `float64`
- required: yes
- nullable: no

Coordinate of the connector point.

#### `src_sample_ids`

- type: list of `uint64`
- required: no (derived)
- nullable: yes

IDs of samples from a point cloud or skeleton which are in the `src_sample_id` column of the connectors table.
`null` means "not yet calculated"; empty list means no associated samples.

#### `tgt_sample_ids`

See above, for the `tgt_sample_id` column of the connectors table.

#### `src_fragment_ids`

See above, for the derived `src_fragment_id` column of the connectors table.

#### `tgt_fragment_ids`

See above, for the derived `tgt_fragment_id` column of the connectors table.

## [`connections`](https://neurarrow.readthedocs.io/en/stable/schemas/connections.html) extension

## Changelog

### v0.1

Initial implementation
