# net.clbarnes.connector

- Extension version: 0.1
- Neurarrow version: >=0.2

Point annotations associated with one or more connections.
Connections have a many-to-one relationship with connectors.

## New schema: `net.clbarnes.connectors`

### Parent schemas

- [Spatial](https://neurarrow.readthedocs.io/en/stable/schemas/spatial.html)

### Schema metadata

#### `com.example.my_extension:version`

- encoding: string
- required: yes

The version of this extension used when writing the table.

### Fields

#### `connector_id`

- type: `uint64`
- required: yes
- nullable: no

ID of the connector, unique within this context.

#### `net.clbarnes.connector:x`

- type: `float64`
- required: yes
- nullable: no

Coordinate of the connector point.

#### `net.clbarnes.connector:y`

See above.

#### `net.clbarnes.connector:z`

See above.

#### `net.clbarnes.connector:src_sample_ids`

- type: list of `uint64`
- required: no (derived)
- nullable: yes

IDs of samples from a point cloud or skeleton which are in the `src_sample_id` column of the connectors table.
`null` means "not yet calculated"; empty list means no associated samples.

#### `net.clbarnes.connector:tgt_sample_ids`

See above, for the `tgt_sample_id` column of the connectors table.

#### `net.clbarnes.connector:src_fragment_ids`

See above, for the derived `src_fragment_id` column of the connectors table.

#### `net.clbarnes.connector:tgt_fragment_ids`

See above, for the derived `tgt_fragment_id` column of the connectors table.

## [`connections`](https://neurarrow.readthedocs.io/en/stable/schemas/connections.html) extension

### Fields

#### `net.clbarnes.connector:connector_id`

- type: `uint64`
- required: yes
- nullable: yes

The ID of the entry in the `net.clbarnes.connectors` table to which this connection belongs.

## Changelog

### v0.1

Initial implementation
