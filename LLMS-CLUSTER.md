# /cluster endpoints

## GET /api2/json/cluster

Cluster index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/replication

List replication jobs.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/cluster/replication

Create a new replication job

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // Flag to disable/deactivate the entry.
  disable?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  id: string;
  // Rate limit in mbps (megabytes per second) as floating point number.
  rate?: number;
  // Mark the replication job for removal. The job will remove all local replication snapshots. When set to 'full', it also tries to remove replicated volumes on the target. The job then removes itself from the configuration file.
  remove_job?: "local" | "full";
  // Storage replication schedule. The format is a subset of `systemd` calendar events.
  schedule?: string;
  // For internal use, to detect if the guest was stolen.
  source?: string;
  // Target node.
  target: string;
  // Section type.
  type: "local";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/replication/{id}

Mark replication job for removal.

### Input Parameters

```ts
interface Params {
  // Will remove the jobconfig entry, but will not cleanup.
  force?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  id: string;
  // Keep replicated data at target (do not remove).
  keep?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/replication/{id}

Read replication job configuration.

### Input Parameters

```ts
interface Params {
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/replication/{id}

Update replication job configuration.

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Flag to disable/deactivate the entry.
  disable?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  id: string;
  // Rate limit in mbps (megabytes per second) as floating point number.
  rate?: number;
  // Mark the replication job for removal. The job will remove all local replication snapshots. When set to 'full', it also tries to remove replicated volumes on the target. The job then removes itself from the configuration file.
  remove_job?: "local" | "full";
  // Storage replication schedule. The format is a subset of `systemd` calendar events.
  schedule?: string;
  // For internal use, to detect if the guest was stolen.
  source?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/metrics

Metrics index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/metrics/server

List configured metric servers.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Flag to disable the plugin.
  disable: boolean;
  // The ID of the entry.
  id: string;
  // Server network port
  port: number;
  // Server dns name or IP address
  server: string;
  // Plugin type.
  type: string;
}[];
```

## DELETE /api2/json/cluster/metrics/server/{id}

Remove Metric server.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/metrics/server/{id}

Read metric server configuration.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/metrics/server/{id}

Create a new external metric server config

### Input Parameters

```ts
interface Params {
  // An API path prefix inserted between '<host>:<port>/' and '/api2/'. Can be useful if the InfluxDB service runs behind a reverse proxy.
  "api-path-prefix"?: string;
  // The InfluxDB bucket/db. Only necessary when using the http v2 api.
  bucket?: string;
  // Flag to disable the plugin.
  disable?: boolean;
  // The ID of the entry.
  id: string;
  influxdbproto?: "udp" | "http" | "https";
  // InfluxDB max-body-size in bytes. Requests are batched up to this size.
  "max-body-size"?: number;
  // MTU for metrics transmission over UDP
  mtu?: number;
  // The InfluxDB organization. Only necessary when using the http v2 api. Has no meaning when using v2 compatibility api.
  organization?: string;
  // root graphite path (ex: proxmox.mycluster.mykey)
  path?: string;
  // server network port
  port: number;
  // Protocol to send graphite data. TCP or UDP (default)
  proto?: "udp" | "tcp";
  // server dns name or IP address
  server: string;
  // graphite TCP socket timeout (default=1)
  timeout?: number;
  // The InfluxDB access token. Only necessary when using the http v2 api. If the v2 compatibility api is used, use 'user:password' instead.
  token?: string;
  // Plugin type.
  type: "graphite" | "influxdb";
  // Set to 0 to disable certificate verification for https endpoints.
  "verify-certificate"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/metrics/server/{id}

Update metric server configuration.

### Input Parameters

```ts
interface Params {
  // An API path prefix inserted between '<host>:<port>/' and '/api2/'. Can be useful if the InfluxDB service runs behind a reverse proxy.
  "api-path-prefix"?: string;
  // The InfluxDB bucket/db. Only necessary when using the http v2 api.
  bucket?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Flag to disable the plugin.
  disable?: boolean;
  // The ID of the entry.
  id: string;
  influxdbproto?: "udp" | "http" | "https";
  // InfluxDB max-body-size in bytes. Requests are batched up to this size.
  "max-body-size"?: number;
  // MTU for metrics transmission over UDP
  mtu?: number;
  // The InfluxDB organization. Only necessary when using the http v2 api. Has no meaning when using v2 compatibility api.
  organization?: string;
  // root graphite path (ex: proxmox.mycluster.mykey)
  path?: string;
  // server network port
  port: number;
  // Protocol to send graphite data. TCP or UDP (default)
  proto?: "udp" | "tcp";
  // server dns name or IP address
  server: string;
  // graphite TCP socket timeout (default=1)
  timeout?: number;
  // The InfluxDB access token. Only necessary when using the http v2 api. If the v2 compatibility api is used, use 'user:password' instead.
  token?: string;
  // Set to 0 to disable certificate verification for https endpoints.
  "verify-certificate"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/metrics/export

Retrieve metrics of the cluster.

### Input Parameters

```ts
interface Params {
  // Also return historic values. Returns full available metric history unless `start-time` is also set
  history?: boolean;
  // Only return metrics for the current node instead of the whole cluster
  "local-only"?: boolean;
  // Only include metrics with a timestamp > start-time.
  "start-time"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications

Index for notification-related API endpoints.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/notifications/matcher-fields

Returns known notification metadata fields

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Name of the field.
  name: string;
}[];
```

## GET /api2/json/cluster/notifications/matcher-field-values

Returns known notification metadata fields and their known values

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Additional comment for this value.
  comment?: string;
  // Field this value belongs to.
  field: string;
  // Notification metadata value known by the system.
  value: string;
}[];
```

## GET /api2/json/cluster/notifications/endpoints

Index for all available endpoint types.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/notifications/endpoints/sendmail

Returns a list of all sendmail endpoints

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Author of the mail
  author?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  from-address?: string;
  // List of email recipients
  mailto?: object[];
  // List of users
  mailto-user?: object[];
  // The name of the endpoint.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
}[];
```

## POST /api2/json/cluster/notifications/endpoints/sendmail

Create a new sendmail endpoint

### Input Parameters

```ts
interface Params {
  // Author of the mail
  author?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  mailto?: object[];
  // List of users
  "mailto-user"?: object[];
  // The name of the endpoint.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/notifications/endpoints/sendmail/{name}

Remove sendmail endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/sendmail/{name}

Return a specific sendmail endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/notifications/endpoints/sendmail/{name}

Update existing sendmail endpoint

### Input Parameters

```ts
interface Params {
  // Author of the mail
  author?: string;
  // Comment
  comment?: string;
  // A list of settings you want to delete.
  delete?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  mailto?: object[];
  // List of users
  "mailto-user"?: object[];
  // The name of the endpoint.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/gotify

Returns a list of all gotify endpoints

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // The name of the endpoint.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
  // Server URL
  server: string;
}[];
```

## POST /api2/json/cluster/notifications/endpoints/gotify

Create a new gotify endpoint

### Input Parameters

```ts
interface Params {
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // The name of the endpoint.
  name: string;
  // Server URL
  server: string;
  // Secret token
  token: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/notifications/endpoints/gotify/{name}

Remove gotify endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/gotify/{name}

Return a specific gotify endpoint

### Input Parameters

```ts
interface Params {
  // Name of the endpoint.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/notifications/endpoints/gotify/{name}

Update existing gotify endpoint

### Input Parameters

```ts
interface Params {
  // Comment
  comment?: string;
  // A list of settings you want to delete.
  delete?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable this target
  disable?: boolean;
  // The name of the endpoint.
  name: string;
  // Server URL
  server?: string;
  // Secret token
  token?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/smtp

Returns a list of all smtp endpoints

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Author of the mail. Defaults to 'Proxmox VE'.
  author?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  from-address: string;
  // List of email recipients
  mailto?: object[];
  // List of users
  mailto-user?: object[];
  // Determine which encryption method shall be used for the connection.
  mode?: "insecure" | "starttls" | "tls";
  // The name of the endpoint.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
  // The port to be used. Defaults to 465 for TLS based connections, 587 for STARTTLS based connections and port 25 for insecure plain-text connections.
  port?: number;
  // The address of the SMTP server.
  server: string;
  // Username for SMTP authentication
  username?: string;
}[];
```

## POST /api2/json/cluster/notifications/endpoints/smtp

Create a new smtp endpoint

### Input Parameters

```ts
interface Params {
  // Author of the mail. Defaults to 'Proxmox VE'.
  author?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  "from-address": string;
  // List of email recipients
  mailto?: object[];
  // List of users
  "mailto-user"?: object[];
  // Determine which encryption method shall be used for the connection.
  mode?: "insecure" | "starttls" | "tls";
  // The name of the endpoint.
  name: string;
  // Password for SMTP authentication
  password?: string;
  // The port to be used. Defaults to 465 for TLS based connections, 587 for STARTTLS based connections and port 25 for insecure plain-text connections.
  port?: number;
  // The address of the SMTP server.
  server: string;
  // Username for SMTP authentication
  username?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/notifications/endpoints/smtp/{name}

Remove smtp endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/smtp/{name}

Return a specific smtp endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/notifications/endpoints/smtp/{name}

Update existing smtp endpoint

### Input Parameters

```ts
interface Params {
  // Author of the mail. Defaults to 'Proxmox VE'.
  author?: string;
  // Comment
  comment?: string;
  // A list of settings you want to delete.
  delete?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable this target
  disable?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  mailto?: object[];
  // List of users
  "mailto-user"?: object[];
  // Determine which encryption method shall be used for the connection.
  mode?: "insecure" | "starttls" | "tls";
  // The name of the endpoint.
  name: string;
  // Password for SMTP authentication
  password?: string;
  // The port to be used. Defaults to 465 for TLS based connections, 587 for STARTTLS based connections and port 25 for insecure plain-text connections.
  port?: number;
  // The address of the SMTP server.
  server?: string;
  // Username for SMTP authentication
  username?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/webhook

Returns a list of all webhook endpoints

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // HTTP body, base64 encoded
  body?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // HTTP headers to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  header?: object[];
  // HTTP method
  method: "post" | "put" | "get";
  // The name of the endpoint.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
  // Secrets to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  secret?: object[];
  // Server URL
  url: string;
}[];
```

## POST /api2/json/cluster/notifications/endpoints/webhook

Create a new webhook endpoint

### Input Parameters

```ts
interface Params {
  // HTTP body, base64 encoded
  body?: string;
  // Comment
  comment?: string;
  // Disable this target
  disable?: boolean;
  // HTTP headers to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  header?: object[];
  // HTTP method
  method: "post" | "put" | "get";
  // The name of the endpoint.
  name: string;
  // Secrets to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  secret?: object[];
  // Server URL
  url: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/notifications/endpoints/webhook/{name}

Remove webhook endpoint

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/endpoints/webhook/{name}

Return a specific webhook endpoint

### Input Parameters

```ts
interface Params {
  // Name of the endpoint.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/notifications/endpoints/webhook/{name}

Update existing webhook endpoint

### Input Parameters

```ts
interface Params {
  // HTTP body, base64 encoded
  body?: string;
  // Comment
  comment?: string;
  // A list of settings you want to delete.
  delete?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable this target
  disable?: boolean;
  // HTTP headers to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  header?: object[];
  // HTTP method
  method?: "post" | "put" | "get";
  // The name of the endpoint.
  name: string;
  // Secrets to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  secret?: object[];
  // Server URL
  url?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/targets

Returns a list of all entities that can be used as notification targets.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Comment
  comment?: string;
  // Show if this target is disabled
  disable?: boolean;
  // Name of the target.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
  // Type of the target.
  type: "sendmail" | "gotify" | "smtp" | "webhook";
}[];
```

## POST /api2/json/cluster/notifications/targets/{name}/test

Send a test notification to a provided target.

### Input Parameters

```ts
interface Params {
  // Name of the target.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/matchers

Returns a list of all matchers

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Comment
  comment?: string;
  // Disable this matcher
  disable?: boolean;
  // Invert match of the whole matcher
  invert-match?: boolean;
  // Match notification timestamp
  match-calendar?: object[];
  // Metadata fields to match (regex or exact match). Must be in the form (regex|exact):<field>=<value>
  match-field?: object[];
  // Notification severities to match
  match-severity?: object[];
  // Choose between 'all' and 'any' for when multiple properties are specified
  mode?: "all" | "any";
  // Name of the matcher.
  name: string;
  // Show if this entry was created by a user or was built-in
  origin: "user-created" | "builtin" | "modified-builtin";
  // Targets to notify on match
  target?: object[];
}[];
```

## POST /api2/json/cluster/notifications/matchers

Create a new matcher

### Input Parameters

```ts
interface Params {
  // Comment
  comment?: string;
  // Disable this matcher
  disable?: boolean;
  // Invert match of the whole matcher
  "invert-match"?: boolean;
  // Match notification timestamp
  "match-calendar"?: object[];
  // Metadata fields to match (regex or exact match). Must be in the form (regex|exact):<field>=<value>
  "match-field"?: object[];
  // Notification severities to match
  "match-severity"?: object[];
  // Choose between 'all' and 'any' for when multiple properties are specified
  mode?: "all" | "any";
  // Name of the matcher.
  name: string;
  // Targets to notify on match
  target?: object[];
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/notifications/matchers/{name}

Remove matcher

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/notifications/matchers/{name}

Return a specific matcher

### Input Parameters

```ts
interface Params {
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/notifications/matchers/{name}

Update existing matcher

### Input Parameters

```ts
interface Params {
  // Comment
  comment?: string;
  // A list of settings you want to delete.
  delete?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable this matcher
  disable?: boolean;
  // Invert match of the whole matcher
  "invert-match"?: boolean;
  // Match notification timestamp
  "match-calendar"?: object[];
  // Metadata fields to match (regex or exact match). Must be in the form (regex|exact):<field>=<value>
  "match-field"?: object[];
  // Notification severities to match
  "match-severity"?: object[];
  // Choose between 'all' and 'any' for when multiple properties are specified
  mode?: "all" | "any";
  // Name of the matcher.
  name: string;
  // Targets to notify on match
  target?: object[];
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/config

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/cluster/config

Generate new cluster configuration. If no links given, default to local IP address as link0.

### Input Parameters

```ts
interface Params {
  // The name of the cluster.
  clustername: string;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // Node id for this node.
  nodeid?: number;
  // Number of votes for this node.
  votes?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/config/apiversion

Return the version of the cluster join API available on this node.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = number;
```

## GET /api2/json/cluster/config/nodes

Corosync node list.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  node: string;
}[];
```

## DELETE /api2/json/cluster/config/nodes/{node}

Removes a node from the cluster configuration.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  node: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/config/nodes/{node}

Adds a node to the cluster configuration. This call is for internal use.

### Input Parameters

```ts
interface Params {
  // The JOIN_API_VERSION of the new node.
  apiversion?: number;
  // Do not throw error if node already exists.
  force?: boolean;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // IP Address of node to add. Used as fallback if no links are given.
  new_node_ip?: string;
  // The cluster node name.
  node: string;
  // Node id for this node.
  nodeid?: number;
  // Number of votes for this node
  votes?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/config/join

Get information needed to join this cluster over the connected node.

### Input Parameters

```ts
interface Params {
  // The node for which the joinee gets the nodeinfo.
  node?: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/config/join

Joins this node into an existing cluster. If no links are given, default to IP resolved by node's hostname on single link (fallback fails for clusters with multiple links).

### Input Parameters

```ts
interface Params {
  // Certificate SHA 256 fingerprint.
  fingerprint: string;
  // Do not throw error if node already exists.
  force?: boolean;
  // Hostname (or IP) of an existing cluster member.
  hostname: string;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // Node id for this node.
  nodeid?: number;
  // Superuser (root) password of peer node.
  password: string;
  // Number of votes for this node
  votes?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/config/totem

Get corosync totem protocol settings.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/config/qdevice

Get QDevice status

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/firewall/groups

List security groups.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest: string;
  // Security Group name.
  group: string;
}[];
```

## POST /api2/json/cluster/firewall/groups

Create new security group.

### Input Parameters

```ts
interface Params {
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Security Group name.
  group: string;
  // Rename/update an existing security group. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing group.
  rename?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/groups/{group}

Delete security group.

### Input Parameters

```ts
interface Params {
  // Security Group name.
  group: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/groups/{group}

List rules.

### Input Parameters

```ts
interface Params {
  // Security Group name.
  group: string;
}
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/cluster/firewall/groups/{group}

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action: string;
  // Descriptive comment.
  comment?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Security Group name.
  group: string;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type: "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/groups/{group}/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Security Group name.
  group: string;
  // Update rule at position <pos>.
  pos?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/groups/{group}/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // Security Group name.
  group: string;
  // Update rule at position <pos>.
  pos?: number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/firewall/groups/{group}/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action?: string;
  // Descriptive comment.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Security Group name.
  group: string;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  moveto?: number;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type?: "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/rules

List rules.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/cluster/firewall/rules

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action: string;
  // Descriptive comment.
  comment?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type: "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/rules/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Update rule at position <pos>.
  pos?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/rules/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // Update rule at position <pos>.
  pos?: number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/firewall/rules/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action?: string;
  // Descriptive comment.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  moveto?: number;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type?: "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/ipset

List IPSets

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest: string;
  // IP set name.
  name: string;
}[];
```

## POST /api2/json/cluster/firewall/ipset

Create new IPSet

### Input Parameters

```ts
interface Params {
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // IP set name.
  name: string;
  // Rename an existing IPSet. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing IPSet.
  rename?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/ipset/{name}

Delete IPSet

### Input Parameters

```ts
interface Params {
  // Delete all members of the IPSet, if there are any.
  force?: boolean;
  // IP set name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/ipset/{name}

List IPSet content

### Input Parameters

```ts
interface Params {
  // IP set name.
  name: string;
}
```

### Returns

```ts
type Returns = {
  cidr: string;
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest: string;
  nomatch?: boolean;
}[];
```

## POST /api2/json/cluster/firewall/ipset/{name}

Add IP or Network to IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  comment?: string;
  // IP set name.
  name: string;
  nomatch?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/ipset/{name}/{cidr}

Remove IP or Network from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // IP set name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/ipset/{name}/{cidr}

Read IP or Network settings from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  // IP set name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/firewall/ipset/{name}/{cidr}

Update IP or Network settings

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // IP set name.
  name: string;
  nomatch?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/aliases

List aliases

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  cidr: string;
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest: string;
  name: string;
}[];
```

## POST /api2/json/cluster/firewall/aliases

Create IP or Network Alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  comment?: string;
  // Alias name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/firewall/aliases/{name}

Remove IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Alias name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/aliases/{name}

Read alias.

### Input Parameters

```ts
interface Params {
  // Alias name.
  name: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/firewall/aliases/{name}

Update IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  cidr: string;
  comment?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Alias name.
  name: string;
  // Rename an existing alias.
  rename?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/options

Get Firewall options.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/firewall/options

Set Firewall options.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Enable ebtables rules cluster wide.
  ebtables?: boolean;
  // Enable or disable the firewall cluster wide.
  enable?: number;
  // Log ratelimiting settings
  log_ratelimit?: string;
  // Forward policy.
  policy_forward?: "ACCEPT" | "DROP";
  // Input policy.
  policy_in?: "ACCEPT" | "REJECT" | "DROP";
  // Output policy.
  policy_out?: "ACCEPT" | "REJECT" | "DROP";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/firewall/macros

List available macros

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // More verbose description (if available).
  descr: string;
  // Macro name.
  macro: string;
}[];
```

## GET /api2/json/cluster/firewall/refs

Lists possible IPSet/Alias reference which are allowed in source/dest properties.

### Input Parameters

```ts
interface Params {
  // Only list references of specified type.
  type?: "alias" | "ipset";
}
```

### Returns

```ts
type Returns = {
  comment?: string;
  name: string;
  ref: string;
  scope: string;
  type: "alias" | "ipset";
}[];
```

## GET /api2/json/cluster/backup

List vzdump backup schedule.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // The job ID.
  id: string;
}[];
```

## POST /api2/json/cluster/backup

Create new vzdump backup job.

### Input Parameters

```ts
interface Params {
  // Backup all known guest systems on this host.
  all?: boolean;
  // Limit I/O bandwidth (in KiB/s).
  bwlimit?: number;
  // Description for the Job.
  comment?: string;
  // Compress dump file.
  compress?: "0" | "1" | "gzip" | "lzo" | "zstd";
  // Day of week selection.
  dow?: string;
  // Store resulting files to specified directory.
  dumpdir?: string;
  // Enable or disable the job.
  enabled?: boolean;
  // Exclude specified guest systems (assumes --all)
  exclude?: string;
  // Exclude certain files/directories (shell globs). Paths starting with '/' are anchored to the container's root, other paths match relative to each subdirectory.
  "exclude-path"?: object[];
  // Options for backup fleecing (VM only).
  fleecing?: string;
  // Job ID (will be autogenerated).
  id?: string;
  // Set IO priority when using the BFQ scheduler. For snapshot and suspend mode backups of VMs, this only affects the compressor. A value of 8 means the idle priority is used, otherwise the best-effort priority is used with the specified value.
  ionice?: number;
  // Maximal time to wait for the global lock (minutes).
  lockwait?: number;
  // Deprecated: use notification targets/matchers instead. Specify when to send a notification mail
  mailnotification?: "always" | "failure";
  // Deprecated: Use notification targets/matchers instead. Comma-separated list of email addresses or users that should receive email notifications.
  mailto?: string;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per guest system.
  maxfiles?: number;
  // Backup mode.
  mode?: "snapshot" | "suspend" | "stop";
  // Only run if executed on this node.
  node?: string;
  // Template string for generating notes for the backup(s). It can contain variables which will be replaced by their values. Currently supported are {{cluster}}, {{guestname}}, {{node}}, and {{vmid}}, but more might be added in the future. Needs to be a single line, newline and backslash need to be escaped as '\n' and '\\' respectively.
  "notes-template"?: string;
  // Determine which notification system to use. If set to 'legacy-sendmail', vzdump will consider the mailto/mailnotification parameters and send emails to the specified address(es) via the 'sendmail' command. If set to 'notification-system', a notification will be sent via PVE's notification system, and the mailto and mailnotification will be ignored. If set to 'auto' (default setting), an email will be sent if mailto is set, and the notification system will be used if not.
  "notification-mode"?: "auto" | "legacy-sendmail" | "notification-system";
  // Deprecated: Do not use
  "notification-policy"?: "always" | "failure" | "never";
  // Deprecated: Do not use
  "notification-target"?: string;
  // PBS mode used to detect file changes and switch encoding format for container backups.
  "pbs-change-detection-mode"?: "legacy" | "data" | "metadata";
  // Other performance-related settings.
  performance?: string;
  // Use pigz instead of gzip when N>0. N=1 uses half of cores, N>1 uses N as thread count.
  pigz?: number;
  // Backup all known guest systems included in the specified pool.
  pool?: string;
  // If true, mark backup(s) as protected.
  protected?: boolean;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // Be quiet.
  quiet?: boolean;
  // Prune older backups according to 'prune-backups'.
  remove?: boolean;
  // If true, the job will be run as soon as possible if it was missed while the scheduler was not running.
  "repeat-missed"?: boolean;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  schedule?: string;
  // Use specified hook script.
  script?: string;
  // Job Start time.
  starttime?: string;
  // Exclude temporary files and logs.
  stdexcludes?: boolean;
  // Stop running backup jobs on this host.
  stop?: boolean;
  // Maximal time to wait until a guest system is stopped (minutes).
  stopwait?: number;
  // Store resulting file to this storage.
  storage?: string;
  // Store temporary files to specified directory.
  tmpdir?: string;
  // The ID of the guest system you want to backup.
  vmid?: string;
  // Zstd threads. N=0 uses half of the available cores, if N is set to a value bigger than 0, N is used as thread count.
  zstd?: number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/backup/{id}

Delete vzdump backup job definition.

### Input Parameters

```ts
interface Params {
  // The job ID.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/backup/{id}

Read vzdump backup job definition.

### Input Parameters

```ts
interface Params {
  // The job ID.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/backup/{id}

Update vzdump backup job definition.

### Input Parameters

```ts
interface Params {
  // Backup all known guest systems on this host.
  all?: boolean;
  // Limit I/O bandwidth (in KiB/s).
  bwlimit?: number;
  // Description for the Job.
  comment?: string;
  // Compress dump file.
  compress?: "0" | "1" | "gzip" | "lzo" | "zstd";
  // A list of settings you want to delete.
  delete?: string;
  // Day of week selection.
  dow?: string;
  // Store resulting files to specified directory.
  dumpdir?: string;
  // Enable or disable the job.
  enabled?: boolean;
  // Exclude specified guest systems (assumes --all)
  exclude?: string;
  // Exclude certain files/directories (shell globs). Paths starting with '/' are anchored to the container's root, other paths match relative to each subdirectory.
  "exclude-path"?: object[];
  // Options for backup fleecing (VM only).
  fleecing?: string;
  // The job ID.
  id: string;
  // Set IO priority when using the BFQ scheduler. For snapshot and suspend mode backups of VMs, this only affects the compressor. A value of 8 means the idle priority is used, otherwise the best-effort priority is used with the specified value.
  ionice?: number;
  // Maximal time to wait for the global lock (minutes).
  lockwait?: number;
  // Deprecated: use notification targets/matchers instead. Specify when to send a notification mail
  mailnotification?: "always" | "failure";
  // Deprecated: Use notification targets/matchers instead. Comma-separated list of email addresses or users that should receive email notifications.
  mailto?: string;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per guest system.
  maxfiles?: number;
  // Backup mode.
  mode?: "snapshot" | "suspend" | "stop";
  // Only run if executed on this node.
  node?: string;
  // Template string for generating notes for the backup(s). It can contain variables which will be replaced by their values. Currently supported are {{cluster}}, {{guestname}}, {{node}}, and {{vmid}}, but more might be added in the future. Needs to be a single line, newline and backslash need to be escaped as '\n' and '\\' respectively.
  "notes-template"?: string;
  // Determine which notification system to use. If set to 'legacy-sendmail', vzdump will consider the mailto/mailnotification parameters and send emails to the specified address(es) via the 'sendmail' command. If set to 'notification-system', a notification will be sent via PVE's notification system, and the mailto and mailnotification will be ignored. If set to 'auto' (default setting), an email will be sent if mailto is set, and the notification system will be used if not.
  "notification-mode"?: "auto" | "legacy-sendmail" | "notification-system";
  // Deprecated: Do not use
  "notification-policy"?: "always" | "failure" | "never";
  // Deprecated: Do not use
  "notification-target"?: string;
  // PBS mode used to detect file changes and switch encoding format for container backups.
  "pbs-change-detection-mode"?: "legacy" | "data" | "metadata";
  // Other performance-related settings.
  performance?: string;
  // Use pigz instead of gzip when N>0. N=1 uses half of cores, N>1 uses N as thread count.
  pigz?: number;
  // Backup all known guest systems included in the specified pool.
  pool?: string;
  // If true, mark backup(s) as protected.
  protected?: boolean;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // Be quiet.
  quiet?: boolean;
  // Prune older backups according to 'prune-backups'.
  remove?: boolean;
  // If true, the job will be run as soon as possible if it was missed while the scheduler was not running.
  "repeat-missed"?: boolean;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  schedule?: string;
  // Use specified hook script.
  script?: string;
  // Job Start time.
  starttime?: string;
  // Exclude temporary files and logs.
  stdexcludes?: boolean;
  // Stop running backup jobs on this host.
  stop?: boolean;
  // Maximal time to wait until a guest system is stopped (minutes).
  stopwait?: number;
  // Store resulting file to this storage.
  storage?: string;
  // Store temporary files to specified directory.
  tmpdir?: string;
  // The ID of the guest system you want to backup.
  vmid?: string;
  // Zstd threads. N=0 uses half of the available cores, if N is set to a value bigger than 0, N is used as thread count.
  zstd?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/backup/{id}/included_volumes

Returns included guests and the backup status of their disks. Optimized to be used in ExtJS tree views.

### Input Parameters

```ts
interface Params {
  // The job ID.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/backup-info

Index for backup info related endpoints

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // API sub-directory endpoint
  subdir: string;
}[];
```

## GET /api2/json/cluster/backup-info/not-backed-up

Shows all guests which are not covered by any backup job.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Name of the guest
  name?: string;
  // Type of the guest.
  type: "qemu" | "lxc";
  // VMID of the guest.
  vmid: number;
}[];
```

## GET /api2/json/cluster/ha

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  id: string;
}[];
```

## GET /api2/json/cluster/ha/resources

List HA resources.

### Input Parameters

```ts
interface Params {
  // Only list resources of specific type
  type?: "ct" | "vm";
}
```

### Returns

```ts
type Returns = {
  sid: string;
}[];
```

## POST /api2/json/cluster/ha/resources

Create a new HA resource.

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // The HA group identifier.
  group?: string;
  // Maximal number of service relocate tries when a service failes to start.
  max_relocate?: number;
  // Maximal number of tries to restart the service on a node after its start failed.
  max_restart?: number;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
  // Requested resource state.
  state?: "started" | "stopped" | "enabled" | "disabled" | "ignored";
  // Resource type.
  type?: "ct" | "vm";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/ha/resources/{sid}

Delete resource configuration.

### Input Parameters

```ts
interface Params {
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ha/resources/{sid}

Read resource configuration.

### Input Parameters

```ts
interface Params {
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/ha/resources/{sid}

Update resource configuration.

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The HA group identifier.
  group?: string;
  // Maximal number of service relocate tries when a service failes to start.
  max_relocate?: number;
  // Maximal number of tries to restart the service on a node after its start failed.
  max_restart?: number;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
  // Requested resource state.
  state?: "started" | "stopped" | "enabled" | "disabled" | "ignored";
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/ha/resources/{sid}/migrate

Request resource migration (online) to another node.

### Input Parameters

```ts
interface Params {
  // Target node.
  node: string;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/ha/resources/{sid}/relocate

Request resource relocatzion to another node. This stops the service on the old node, and restarts it on the target node.

### Input Parameters

```ts
interface Params {
  // Target node.
  node: string;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  sid: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ha/groups

Get HA groups.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  group: string;
}[];
```

## POST /api2/json/cluster/ha/groups

Create a new HA group.

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // The HA group identifier.
  group: string;
  // List of cluster node names with optional priority.
  nodes: string;
  // The CRM tries to run services on the node with the highest priority. If a node with higher priority comes online, the CRM migrates the service to that node. Enabling nofailback prevents that behavior.
  nofailback?: boolean;
  // Resources bound to restricted groups may only run on nodes defined by the group.
  restricted?: boolean;
  // Group type.
  type?: "group";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/ha/groups/{group}

Delete ha group configuration.

### Input Parameters

```ts
interface Params {
  // The HA group identifier.
  group: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ha/groups/{group}

Read ha group configuration.

### Input Parameters

```ts
interface Params {
  // The HA group identifier.
  group: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/ha/groups/{group}

Update ha group configuration.

### Input Parameters

```ts
interface Params {
  // Description.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The HA group identifier.
  group: string;
  // List of cluster node names with optional priority.
  nodes?: string;
  // The CRM tries to run services on the node with the highest priority. If a node with higher priority comes online, the CRM migrates the service to that node. Enabling nofailback prevents that behavior.
  nofailback?: boolean;
  // Resources bound to restricted groups may only run on nodes defined by the group.
  restricted?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ha/status

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/ha/status/current

Get HA manger status.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // For type 'service'. Service state as seen by the CRM.
  crm_state?: string;
  // Status entry ID (quorum, master, lrm:<node>, service:<sid>).
  id: string;
  // For type 'service'.
  max_relocate?: number;
  // For type 'service'.
  max_restart?: number;
  // Node associated to status entry.
  node: string;
  // For type 'quorum'. Whether the cluster is quorate or not.
  quorate?: boolean;
  // For type 'service'. Requested service state.
  request_state?: string;
  // For type 'service'. Service ID.
  sid?: string;
  // For type 'service'. Verbose service state.
  state?: string;
  // Status of the entry (value depends on type).
  status: string;
  // For type 'lrm','master'. Timestamp of the status information.
  timestamp?: number;
  // Type of status entry.
  type: "quorum" | "master" | "lrm" | "service";
}[];
```

## GET /api2/json/cluster/ha/status/manager_status

Get full HA manger status, including LRM status.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/acme

ACMEAccount index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/acme/plugins

ACME plugin index.

### Input Parameters

```ts
interface Params {
  // Only list ACME plugins of a specific type
  type?: "dns" | "standalone";
}
```

### Returns

```ts
type Returns = {
  // Unique identifier for ACME plugin instance.
  plugin: string;
}[];
```

## POST /api2/json/cluster/acme/plugins

Add ACME plugin configuration.

### Input Parameters

```ts
interface Params {
  // API plugin name
  api?:
    | "1984hosting"
    | "acmedns"
    | "acmeproxy"
    | "active24"
    | "ad"
    | "ali"
    | "alviy"
    | "anx"
    | "artfiles"
    | "arvan"
    | "aurora"
    | "autodns"
    | "aws"
    | "azion"
    | "azure"
    | "bookmyname"
    | "bunny"
    | "cf"
    | "clouddns"
    | "cloudns"
    | "cn"
    | "conoha"
    | "constellix"
    | "cpanel"
    | "curanet"
    | "cyon"
    | "da"
    | "ddnss"
    | "desec"
    | "df"
    | "dgon"
    | "dnsexit"
    | "dnshome"
    | "dnsimple"
    | "dnsservices"
    | "doapi"
    | "domeneshop"
    | "dp"
    | "dpi"
    | "dreamhost"
    | "duckdns"
    | "durabledns"
    | "dyn"
    | "dynu"
    | "dynv6"
    | "easydns"
    | "edgedns"
    | "euserv"
    | "exoscale"
    | "fornex"
    | "freedns"
    | "gandi_livedns"
    | "gcloud"
    | "gcore"
    | "gd"
    | "geoscaling"
    | "googledomains"
    | "he"
    | "hetzner"
    | "hexonet"
    | "hostingde"
    | "huaweicloud"
    | "infoblox"
    | "infomaniak"
    | "internetbs"
    | "inwx"
    | "ionos"
    | "ionos_cloud"
    | "ipv64"
    | "ispconfig"
    | "jd"
    | "joker"
    | "kappernet"
    | "kas"
    | "kinghost"
    | "knot"
    | "la"
    | "leaseweb"
    | "lexicon"
    | "limacity"
    | "linode"
    | "linode_v4"
    | "loopia"
    | "lua"
    | "maradns"
    | "me"
    | "miab"
    | "misaka"
    | "myapi"
    | "mydevil"
    | "mydnsjp"
    | "mythic_beasts"
    | "namecheap"
    | "namecom"
    | "namesilo"
    | "nanelo"
    | "nederhost"
    | "neodigit"
    | "netcup"
    | "netlify"
    | "nic"
    | "njalla"
    | "nm"
    | "nsd"
    | "nsone"
    | "nsupdate"
    | "nw"
    | "oci"
    | "omglol"
    | "one"
    | "online"
    | "openprovider"
    | "openstack"
    | "opnsense"
    | "ovh"
    | "pdns"
    | "pleskxml"
    | "pointhq"
    | "porkbun"
    | "rackcorp"
    | "rackspace"
    | "rage4"
    | "rcode0"
    | "regru"
    | "scaleway"
    | "schlundtech"
    | "selectel"
    | "selfhost"
    | "servercow"
    | "simply"
    | "technitium"
    | "tele3"
    | "tencent"
    | "timeweb"
    | "transip"
    | "udr"
    | "ultra"
    | "unoeuro"
    | "variomedia"
    | "veesp"
    | "vercel"
    | "vscale"
    | "vultr"
    | "websupport"
    | "west_cn"
    | "world4you"
    | "yandex360"
    | "yc"
    | "zilore"
    | "zone"
    | "zoneedit"
    | "zonomi";
  // DNS plugin data. (base64 encoded)
  data?: string;
  // Flag to disable the config.
  disable?: boolean;
  // ACME Plugin ID name
  id: string;
  // List of cluster node names.
  nodes?: string;
  // ACME challenge type.
  type: "dns" | "standalone";
  // Extra delay in seconds to wait before requesting validation. Allows to cope with a long TTL of DNS records.
  "validation-delay"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/acme/plugins/{id}

Delete ACME plugin configuration.

### Input Parameters

```ts
interface Params {
  // Unique identifier for ACME plugin instance.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/acme/plugins/{id}

Get ACME plugin configuration.

### Input Parameters

```ts
interface Params {
  // Unique identifier for ACME plugin instance.
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/acme/plugins/{id}

Update ACME plugin configuration.

### Input Parameters

```ts
interface Params {
  // API plugin name
  api?:
    | "1984hosting"
    | "acmedns"
    | "acmeproxy"
    | "active24"
    | "ad"
    | "ali"
    | "alviy"
    | "anx"
    | "artfiles"
    | "arvan"
    | "aurora"
    | "autodns"
    | "aws"
    | "azion"
    | "azure"
    | "bookmyname"
    | "bunny"
    | "cf"
    | "clouddns"
    | "cloudns"
    | "cn"
    | "conoha"
    | "constellix"
    | "cpanel"
    | "curanet"
    | "cyon"
    | "da"
    | "ddnss"
    | "desec"
    | "df"
    | "dgon"
    | "dnsexit"
    | "dnshome"
    | "dnsimple"
    | "dnsservices"
    | "doapi"
    | "domeneshop"
    | "dp"
    | "dpi"
    | "dreamhost"
    | "duckdns"
    | "durabledns"
    | "dyn"
    | "dynu"
    | "dynv6"
    | "easydns"
    | "edgedns"
    | "euserv"
    | "exoscale"
    | "fornex"
    | "freedns"
    | "gandi_livedns"
    | "gcloud"
    | "gcore"
    | "gd"
    | "geoscaling"
    | "googledomains"
    | "he"
    | "hetzner"
    | "hexonet"
    | "hostingde"
    | "huaweicloud"
    | "infoblox"
    | "infomaniak"
    | "internetbs"
    | "inwx"
    | "ionos"
    | "ionos_cloud"
    | "ipv64"
    | "ispconfig"
    | "jd"
    | "joker"
    | "kappernet"
    | "kas"
    | "kinghost"
    | "knot"
    | "la"
    | "leaseweb"
    | "lexicon"
    | "limacity"
    | "linode"
    | "linode_v4"
    | "loopia"
    | "lua"
    | "maradns"
    | "me"
    | "miab"
    | "misaka"
    | "myapi"
    | "mydevil"
    | "mydnsjp"
    | "mythic_beasts"
    | "namecheap"
    | "namecom"
    | "namesilo"
    | "nanelo"
    | "nederhost"
    | "neodigit"
    | "netcup"
    | "netlify"
    | "nic"
    | "njalla"
    | "nm"
    | "nsd"
    | "nsone"
    | "nsupdate"
    | "nw"
    | "oci"
    | "omglol"
    | "one"
    | "online"
    | "openprovider"
    | "openstack"
    | "opnsense"
    | "ovh"
    | "pdns"
    | "pleskxml"
    | "pointhq"
    | "porkbun"
    | "rackcorp"
    | "rackspace"
    | "rage4"
    | "rcode0"
    | "regru"
    | "scaleway"
    | "schlundtech"
    | "selectel"
    | "selfhost"
    | "servercow"
    | "simply"
    | "technitium"
    | "tele3"
    | "tencent"
    | "timeweb"
    | "transip"
    | "udr"
    | "ultra"
    | "unoeuro"
    | "variomedia"
    | "veesp"
    | "vercel"
    | "vscale"
    | "vultr"
    | "websupport"
    | "west_cn"
    | "world4you"
    | "yandex360"
    | "yc"
    | "zilore"
    | "zone"
    | "zoneedit"
    | "zonomi";
  // DNS plugin data. (base64 encoded)
  data?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Flag to disable the config.
  disable?: boolean;
  // ACME Plugin ID name
  id: string;
  // List of cluster node names.
  nodes?: string;
  // Extra delay in seconds to wait before requesting validation. Allows to cope with a long TTL of DNS records.
  "validation-delay"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/acme/account

ACMEAccount index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/cluster/acme/account

Register a new ACME account with CA.

### Input Parameters

```ts
interface Params {
  // Contact email addresses.
  contact: string;
  // URL of ACME CA directory endpoint.
  directory?: string;
  // HMAC key for External Account Binding.
  "eab-hmac-key"?: string;
  // Key Identifier for External Account Binding.
  "eab-kid"?: string;
  // ACME account config file name.
  name?: string;
  // URL of CA TermsOfService - setting this indicates agreement.
  tos_url?: string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/cluster/acme/account/{name}

Deactivate existing ACME account at CA.

### Input Parameters

```ts
interface Params {
  // ACME account config file name.
  name?: string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/acme/account/{name}

Return existing ACME account information.

### Input Parameters

```ts
interface Params {
  // ACME account config file name.
  name?: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/acme/account/{name}

Update existing ACME account information with CA. Note: not specifying any new account information triggers a refresh.

### Input Parameters

```ts
interface Params {
  // Contact email addresses.
  contact?: string;
  // ACME account config file name.
  name?: string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/acme/tos

Retrieve ACME TermsOfService URL from CA. Deprecated, please use /cluster/acme/meta.

### Input Parameters

```ts
interface Params {
  // URL of ACME CA directory endpoint.
  directory?: string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/acme/meta

Retrieve ACME Directory Meta Information

### Input Parameters

```ts
interface Params {
  // URL of ACME CA directory endpoint.
  directory?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/acme/directories

Get named known ACME directory endpoints.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  name: string;
  // URL of ACME CA directory endpoint.
  url: string;
}[];
```

## GET /api2/json/cluster/acme/challenge-schema

Get schema of ACME challenge types.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  id: string;
  // Human readable name, falls back to id
  name: string;
  schema: any;
  type: string;
}[];
```

## GET /api2/json/cluster/ceph

Cluster ceph index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/ceph/metadata

Get ceph metadata.

### Input Parameters

```ts
interface Params {
  scope?: "all" | "versions";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ceph/status

Get ceph status.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/ceph/flags

get the status of all ceph flags

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Flag description.
  description: string;
  // Flag name.
  name:
    | "nobackfill"
    | "nodeep-scrub"
    | "nodown"
    | "noin"
    | "noout"
    | "norebalance"
    | "norecover"
    | "noscrub"
    | "notieragent"
    | "noup"
    | "pause";
  // Flag value.
  value: boolean;
}[];
```

## PUT /api2/json/cluster/ceph/flags

Set/Unset multiple ceph flags at once.

### Input Parameters

```ts
interface Params {
  // Backfilling of PGs is suspended.
  nobackfill?: boolean;
  // Deep Scrubbing is disabled.
  "nodeep-scrub"?: boolean;
  // OSD failure reports are being ignored, such that the monitors will not mark OSDs down.
  nodown?: boolean;
  // OSDs that were previously marked out will not be marked back in when they start.
  noin?: boolean;
  // OSDs will not automatically be marked out after the configured interval.
  noout?: boolean;
  // Rebalancing of PGs is suspended.
  norebalance?: boolean;
  // Recovery of PGs is suspended.
  norecover?: boolean;
  // Scrubbing is disabled.
  noscrub?: boolean;
  // Cache tiering activity is suspended.
  notieragent?: boolean;
  // OSDs are not allowed to start.
  noup?: boolean;
  // Pauses read and writes.
  pause?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/ceph/flags/{flag}

Get the status of a specific ceph flag.

### Input Parameters

```ts
interface Params {
  // The name of the flag name to get.
  flag:
    | "nobackfill"
    | "nodeep-scrub"
    | "nodown"
    | "noin"
    | "noout"
    | "norebalance"
    | "norecover"
    | "noscrub"
    | "notieragent"
    | "noup"
    | "pause";
}
```

### Returns

```ts
type Returns = boolean;
```

## PUT /api2/json/cluster/ceph/flags/{flag}

Set or clear (unset) a specific ceph flag

### Input Parameters

```ts
interface Params {
  // The ceph flag to update
  flag:
    | "nobackfill"
    | "nodeep-scrub"
    | "nodown"
    | "noin"
    | "noout"
    | "norebalance"
    | "norecover"
    | "noscrub"
    | "notieragent"
    | "noup"
    | "pause";
  // The new value of the flag
  value: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/jobs

Index for jobs related endpoints.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // API sub-directory endpoint
  subdir: string;
}[];
```

## GET /api2/json/cluster/jobs/realm-sync

List configured realm-sync-jobs.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // A comment for the job.
  comment?: string;
  // If the job is enabled or not.
  enabled: boolean;
  // The ID of the entry.
  id: string;
  // Last execution time of the job in seconds since the beginning of the UNIX epoch
  last-run?: number;
  // Next planned execution time of the job in seconds since the beginning of the UNIX epoch.
  next-run?: number;
  // Authentication domain ID
  realm: string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  remove-vanished?: string;
  // The configured sync schedule.
  schedule: string;
  // Select what to sync.
  scope?: "users" | "groups" | "both";
}[];
```

## DELETE /api2/json/cluster/jobs/realm-sync/{id}

Delete realm-sync job definition.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/jobs/realm-sync/{id}

Read realm-sync job definition.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/jobs/realm-sync/{id}

Create new realm-sync job.

### Input Parameters

```ts
interface Params {
  // Description for the Job.
  comment?: string;
  // Enable newly synced users immediately.
  "enable-new"?: boolean;
  // Determines if the job is enabled.
  enabled?: boolean;
  // The ID of the job.
  id: string;
  // Authentication domain ID
  realm?: string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  schedule: string;
  // Select what to sync.
  scope?: "users" | "groups" | "both";
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/jobs/realm-sync/{id}

Update realm-sync job definition.

### Input Parameters

```ts
interface Params {
  // Description for the Job.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Enable newly synced users immediately.
  "enable-new"?: boolean;
  // Determines if the job is enabled.
  enabled?: boolean;
  // The ID of the job.
  id: string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  schedule: string;
  // Select what to sync.
  scope?: "users" | "groups" | "both";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/jobs/schedule-analyze

Returns a list of future schedule runtimes.

### Input Parameters

```ts
interface Params {
  // Number of event-iteration to simulate and return.
  iterations?: number;
  // Job schedule. The format is a subset of `systemd` calendar events.
  schedule: string;
  // UNIX timestamp to start the calculation from. Defaults to the current time.
  starttime?: number;
}
```

### Returns

```ts
type Returns = {
  // UNIX timestamp for the run.
  timestamp: number;
  // UTC timestamp for the run.
  utc: string;
}[];
```

## GET /api2/json/cluster/mapping

List resource types.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = object[];
```

## GET /api2/json/cluster/mapping/dir

List directory mapping

### Input Parameters

```ts
interface Params {
  // If given, checks the configurations on the given node for correctness, and adds relevant diagnostics for the directory to the response.
  "check-node"?: string;
}
```

### Returns

```ts
type Returns = {
  // A list of checks, only present if 'check-node' is set.
  checks?: {
    // The message of the error
    message: string;
    // The severity of the error
    severity: "warning" | "error";
  }[];
  // A description of the logical mapping.
  description: string;
  // The logical ID of the mapping.
  id: string;
  // The entries of the mapping.
  map: object[];
}[];
```

## POST /api2/json/cluster/mapping/dir

Create a new directory mapping.

### Input Parameters

```ts
interface Params {
  // Description of the directory mapping
  description?: string;
  // The ID of the directory mapping
  id: string;
  // A list of maps for the cluster nodes.
  map: object[];
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/mapping/dir/{id}

Remove directory mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/mapping/dir/{id}

Get directory mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/mapping/dir/{id}

Update a directory mapping.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Description of the directory mapping
  description?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The ID of the directory mapping
  id: string;
  // A list of maps for the cluster nodes.
  map?: object[];
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/mapping/pci

List PCI Hardware Mapping

### Input Parameters

```ts
interface Params {
  // If given, checks the configurations on the given node for correctness, and adds relevant diagnostics for the devices to the response.
  "check-node"?: string;
}
```

### Returns

```ts
type Returns = {
  // A list of checks, only present if 'check_node' is set.
  checks?: {
    // The message of the error
    message: string;
    // The severity of the error
    severity: "warning" | "error";
  }[];
  // A description of the logical mapping.
  description: string;
  // The logical ID of the mapping.
  id: string;
  // The entries of the mapping.
  map: object[];
}[];
```

## POST /api2/json/cluster/mapping/pci

Create a new hardware mapping.

### Input Parameters

```ts
interface Params {
  // Description of the logical PCI device.
  description?: string;
  // The ID of the logical PCI mapping.
  id: string;
  // Marks the device(s) as being able to be live-migrated (Experimental). This needs hardware and driver support to work.
  "live-migration-capable"?: boolean;
  // A list of maps for the cluster nodes.
  map: object[];
  // Marks the device(s) as being capable of providing mediated devices.
  mdev?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/mapping/pci/{id}

Remove Hardware Mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/mapping/pci/{id}

Get PCI Mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/mapping/pci/{id}

Update a hardware mapping.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Description of the logical PCI device.
  description?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The ID of the logical PCI mapping.
  id: string;
  // Marks the device(s) as being able to be live-migrated (Experimental). This needs hardware and driver support to work.
  "live-migration-capable"?: boolean;
  // A list of maps for the cluster nodes.
  map?: object[];
  // Marks the device(s) as being capable of providing mediated devices.
  mdev?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/mapping/usb

List USB Hardware Mappings

### Input Parameters

```ts
interface Params {
  // If given, checks the configurations on the given node for correctness, and adds relevant errors to the devices.
  "check-node"?: string;
}
```

### Returns

```ts
type Returns = {
  // A description of the logical mapping.
  description: string;
  // A list of errors when 'check_node' is given.
  error: any;
  // The logical ID of the mapping.
  id: string;
  // The entries of the mapping.
  map: object[];
}[];
```

## POST /api2/json/cluster/mapping/usb

Create a new hardware mapping.

### Input Parameters

```ts
interface Params {
  // Description of the logical USB device.
  description?: string;
  // The ID of the logical USB mapping.
  id: string;
  // A list of maps for the cluster nodes.
  map: object[];
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/mapping/usb/{id}

Remove Hardware Mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/mapping/usb/{id}

Get USB Mapping.

### Input Parameters

```ts
interface Params {
  id: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/mapping/usb/{id}

Update a hardware mapping.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Description of the logical USB device.
  description?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The ID of the logical USB mapping.
  id: string;
  // A list of maps for the cluster nodes.
  map: object[];
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  id: string;
}[];
```

## PUT /api2/json/cluster/sdn

Apply sdn controller changes && reload.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/cluster/sdn/vnets

SDN vnets index.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/cluster/sdn/vnets

Create a new sdn vnet object.

### Input Parameters

```ts
interface Params {
  // alias name of the vnet
  alias?: string;
  // If true, sets the isolated property for all members of this VNet
  "isolate-ports"?: boolean;
  // vlan or vxlan id
  tag?: number;
  // Type
  type?: "vnet";
  // Allow vm VLANs to pass through this vnet.
  vlanaware?: boolean;
  // The SDN vnet object identifier.
  vnet: string;
  // zone id
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/vnets/{vnet}

Delete sdn vnet object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}

Read sdn vnet configuration.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/vnets/{vnet}

Update sdn vnet object configuration.

### Input Parameters

```ts
interface Params {
  // alias name of the vnet
  alias?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // If true, sets the isolated property for all members of this VNet
  "isolate-ports"?: boolean;
  // vlan or vxlan id
  tag?: number;
  // Allow vm VLANs to pass through this vnet.
  vlanaware?: boolean;
  // The SDN vnet object identifier.
  vnet: string;
  // zone id
  zone?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/firewall

Directory index.

### Input Parameters

```ts
interface Params {
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/firewall/rules

List rules.

### Input Parameters

```ts
interface Params {
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/cluster/sdn/vnets/{vnet}/firewall/rules

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action: string;
  // Descriptive comment.
  comment?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type: "in" | "out" | "forward" | "group";
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/vnets/{vnet}/firewall/rules/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Update rule at position <pos>.
  pos?: number;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/firewall/rules/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // Update rule at position <pos>.
  pos?: number;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/vnets/{vnet}/firewall/rules/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  action?: string;
  // Descriptive comment.
  comment?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  dest?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  dport?: string;
  // Flag to enable/disable a rule.
  enable?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  iface?: string;
  // Log level for firewall rule.
  log?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Use predefined standard macro.
  macro?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  moveto?: number;
  // Update rule at position <pos>.
  pos?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  proto?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  source?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  sport?: string;
  // Rule type.
  type?: "in" | "out" | "forward" | "group";
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/firewall/options

Get vnet firewall options.

### Input Parameters

```ts
interface Params {
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/vnets/{vnet}/firewall/options

Set Firewall options.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Enable/disable firewall rules.
  enable?: boolean;
  // Log level for forwarded traffic.
  log_level_forward?:
    | "emerg"
    | "alert"
    | "crit"
    | "err"
    | "warning"
    | "notice"
    | "info"
    | "debug"
    | "nolog";
  // Forward policy.
  policy_forward?: "ACCEPT" | "DROP";
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/subnets

SDN subnets index.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/cluster/sdn/vnets/{vnet}/subnets

Create a new sdn subnet object.

### Input Parameters

```ts
interface Params {
  // IP address for the DNS server
  "dhcp-dns-server"?: string;
  // A list of DHCP ranges for this subnet
  "dhcp-range"?: object[];
  // dns domain zone prefix  ex: 'adm' -> <hostname>.adm.mydomain.com
  dnszoneprefix?: string;
  // Subnet Gateway: Will be assign on vnet for layer3 zones
  gateway?: string;
  // enable masquerade for this subnet if pve-firewall
  snat?: boolean;
  // The SDN subnet object identifier.
  subnet: string;
  type: "subnet";
  // associated vnet
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/vnets/{vnet}/subnets/{subnet}

Delete sdn subnet object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN subnet object identifier.
  subnet: string;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/vnets/{vnet}/subnets/{subnet}

Read sdn subnet configuration.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // The SDN subnet object identifier.
  subnet: string;
  // The SDN vnet object identifier.
  vnet: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/vnets/{vnet}/subnets/{subnet}

Update sdn subnet object configuration.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // IP address for the DNS server
  "dhcp-dns-server"?: string;
  // A list of DHCP ranges for this subnet
  "dhcp-range"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // dns domain zone prefix  ex: 'adm' -> <hostname>.adm.mydomain.com
  dnszoneprefix?: string;
  // Subnet Gateway: Will be assign on vnet for layer3 zones
  gateway?: string;
  // enable masquerade for this subnet if pve-firewall
  snat?: boolean;
  // The SDN subnet object identifier.
  subnet: string;
  // associated vnet
  vnet?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/vnets/{vnet}/ips

Delete IP Mappings in a VNet

### Input Parameters

```ts
interface Params {
  // The IP address to delete
  ip: string;
  // Unicast MAC address.
  mac?: string;
  // The SDN vnet object identifier.
  vnet: string;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/cluster/sdn/vnets/{vnet}/ips

Create IP Mapping in a VNet

### Input Parameters

```ts
interface Params {
  // The IP address to associate with the given MAC address
  ip: string;
  // Unicast MAC address.
  mac?: string;
  // The SDN vnet object identifier.
  vnet: string;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/vnets/{vnet}/ips

Update IP Mapping in a VNet

### Input Parameters

```ts
interface Params {
  // The IP address to associate with the given MAC address
  ip: string;
  // Unicast MAC address.
  mac?: string;
  // The (unique) ID of the VM.
  vmid?: number;
  // The SDN vnet object identifier.
  vnet: string;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/zones

SDN zones index.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // Only list SDN zones of specific type
  type?: "evpn" | "faucet" | "qinq" | "simple" | "vlan" | "vxlan";
}
```

### Returns

```ts
type Returns = {
  dhcp?: string;
  dns?: string;
  dnszone?: string;
  ipam?: string;
  mtu?: number;
  nodes?: string;
  pending?: boolean;
  reversedns?: string;
  state?: string;
  type: string;
  zone: string;
}[];
```

## POST /api2/json/cluster/sdn/zones

Create a new sdn zone object.

### Input Parameters

```ts
interface Params {
  // Advertise evpn subnets if you have silent hosts
  "advertise-subnets"?: boolean;
  bridge?: string;
  // Disable auto mac learning.
  "bridge-disable-mac-learning"?: boolean;
  // Frr router name
  controller?: string;
  // Type of the DHCP backend for this zone
  dhcp?: "dnsmasq";
  // Disable ipv4 arp && ipv6 neighbour discovery suppression
  "disable-arp-nd-suppression"?: boolean;
  // dns api server
  dns?: string;
  // dns domain zone  ex: mydomain.com
  dnszone?: string;
  // Faucet dataplane id
  "dp-id"?: number;
  // List of cluster node names.
  exitnodes?: string;
  // Allow exitnodes to connect to evpn guests
  "exitnodes-local-routing"?: boolean;
  // Force traffic to this exitnode first.
  "exitnodes-primary"?: string;
  // use a specific ipam
  ipam?: string;
  // Anycast logical router mac address
  mac?: string;
  // MTU
  mtu?: number;
  // List of cluster node names.
  nodes?: string;
  // peers address list.
  peers?: string;
  // reverse dns api server
  reversedns?: string;
  // Route-Target import
  "rt-import"?: string;
  // Service-VLAN Tag
  tag?: number;
  // Plugin type.
  type: "evpn" | "faucet" | "qinq" | "simple" | "vlan" | "vxlan";
  "vlan-protocol"?: "802.1q" | "802.1ad";
  // l3vni.
  "vrf-vxlan"?: number;
  // Vxlan tunnel udp port (default 4789).
  "vxlan-port"?: number;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/zones/{zone}

Delete sdn zone object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/zones/{zone}

Read sdn zone configuration.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/zones/{zone}

Update sdn zone object configuration.

### Input Parameters

```ts
interface Params {
  // Advertise evpn subnets if you have silent hosts
  "advertise-subnets"?: boolean;
  bridge?: string;
  // Disable auto mac learning.
  "bridge-disable-mac-learning"?: boolean;
  // Frr router name
  controller?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Type of the DHCP backend for this zone
  dhcp?: "dnsmasq";
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Disable ipv4 arp && ipv6 neighbour discovery suppression
  "disable-arp-nd-suppression"?: boolean;
  // dns api server
  dns?: string;
  // dns domain zone  ex: mydomain.com
  dnszone?: string;
  // Faucet dataplane id
  "dp-id"?: number;
  // List of cluster node names.
  exitnodes?: string;
  // Allow exitnodes to connect to evpn guests
  "exitnodes-local-routing"?: boolean;
  // Force traffic to this exitnode first.
  "exitnodes-primary"?: string;
  // use a specific ipam
  ipam?: string;
  // Anycast logical router mac address
  mac?: string;
  // MTU
  mtu?: number;
  // List of cluster node names.
  nodes?: string;
  // peers address list.
  peers?: string;
  // reverse dns api server
  reversedns?: string;
  // Route-Target import
  "rt-import"?: string;
  // Service-VLAN Tag
  tag?: number;
  "vlan-protocol"?: "802.1q" | "802.1ad";
  // l3vni.
  "vrf-vxlan"?: number;
  // Vxlan tunnel udp port (default 4789).
  "vxlan-port"?: number;
  // The SDN zone object identifier.
  zone: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/controllers

SDN controllers index.

### Input Parameters

```ts
interface Params {
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
  // Only list sdn controllers of specific type
  type?: "bgp" | "evpn" | "faucet" | "isis";
}
```

### Returns

```ts
type Returns = {
  controller: string;
  pending?: boolean;
  state?: string;
  type: string;
}[];
```

## POST /api2/json/cluster/sdn/controllers

Create a new sdn controller object.

### Input Parameters

```ts
interface Params {
  // autonomous system number
  asn?: number;
  "bgp-multipath-as-path-relax"?: boolean;
  // The SDN controller object identifier.
  controller: string;
  // Enable ebgp. (remote-as external)
  ebgp?: boolean;
  "ebgp-multihop"?: number;
  // ISIS domain.
  "isis-domain"?: string;
  // ISIS interface.
  "isis-ifaces"?: string;
  // ISIS network entity title.
  "isis-net"?: string;
  // source loopback interface.
  loopback?: string;
  // The cluster node name.
  node?: string;
  // peers address list.
  peers?: string;
  // Plugin type.
  type: "bgp" | "evpn" | "faucet" | "isis";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/controllers/{controller}

Delete sdn controller object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN controller object identifier.
  controller: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/controllers/{controller}

Read sdn controller configuration.

### Input Parameters

```ts
interface Params {
  // The SDN controller object identifier.
  controller: string;
  // Display pending config.
  pending?: boolean;
  // Display running config.
  running?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/controllers/{controller}

Update sdn controller object configuration.

### Input Parameters

```ts
interface Params {
  // autonomous system number
  asn?: number;
  "bgp-multipath-as-path-relax"?: boolean;
  // The SDN controller object identifier.
  controller: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Enable ebgp. (remote-as external)
  ebgp?: boolean;
  "ebgp-multihop"?: number;
  // ISIS domain.
  "isis-domain"?: string;
  // ISIS interface.
  "isis-ifaces"?: string;
  // ISIS network entity title.
  "isis-net"?: string;
  // source loopback interface.
  loopback?: string;
  // The cluster node name.
  node?: string;
  // peers address list.
  peers?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/ipams

SDN ipams index.

### Input Parameters

```ts
interface Params {
  // Only list sdn ipams of specific type
  type?: "netbox" | "phpipam" | "pve";
}
```

### Returns

```ts
type Returns = {
  ipam: string;
  type: string;
}[];
```

## POST /api2/json/cluster/sdn/ipams

Create a new sdn ipam object.

### Input Parameters

```ts
interface Params {
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  // The SDN ipam object identifier.
  ipam: string;
  section?: number;
  token?: string;
  // Plugin type.
  type: "netbox" | "phpipam" | "pve";
  url?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/ipams/{ipam}

Delete sdn ipam object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN ipam object identifier.
  ipam: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/ipams/{ipam}

Read sdn ipam configuration.

### Input Parameters

```ts
interface Params {
  // The SDN ipam object identifier.
  ipam: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/ipams/{ipam}

Update sdn ipam object configuration.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  // The SDN ipam object identifier.
  ipam: string;
  section?: number;
  token?: string;
  url?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/ipams/{ipam}/status

List PVE IPAM Entries

### Input Parameters

```ts
interface Params {
  // The SDN ipam object identifier.
  ipam: string;
}
```

### Returns

```ts
type Returns = object[];
```

## GET /api2/json/cluster/sdn/dns

SDN dns index.

### Input Parameters

```ts
interface Params {
  // Only list sdn dns of specific type
  type?: "powerdns";
}
```

### Returns

```ts
type Returns = {
  dns: string;
  type: string;
}[];
```

## POST /api2/json/cluster/sdn/dns

Create a new sdn dns object.

### Input Parameters

```ts
interface Params {
  // The SDN dns object identifier.
  dns: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  key: string;
  reversemaskv6?: number;
  reversev6mask?: number;
  ttl?: number;
  // Plugin type.
  type: "powerdns";
  url: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/cluster/sdn/dns/{dns}

Delete sdn dns object configuration.

### Input Parameters

```ts
interface Params {
  // The SDN dns object identifier.
  dns: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/sdn/dns/{dns}

Read sdn dns configuration.

### Input Parameters

```ts
interface Params {
  // The SDN dns object identifier.
  dns: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/sdn/dns/{dns}

Update sdn dns object configuration.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // The SDN dns object identifier.
  dns: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  key?: string;
  reversemaskv6?: number;
  ttl?: number;
  url?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/log

Read cluster log

### Input Parameters

```ts
interface Params {
  // Maximum number of entries.
  max?: number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/cluster/resources

Resources index (cluster wide).

### Input Parameters

```ts
interface Params {
  // Resource type.
  type?: "vm" | "storage" | "node" | "sdn";
}
```

### Returns

```ts
type Returns = {
  // The cgroup mode the node operates under (for type 'node').
  cgroup-mode?: number;
  // Allowed storage content types (for type 'storage').
  content?: string;
  // CPU utilization (for types 'node', 'qemu' and 'lxc').
  cpu?: number;
  // Used disk space in bytes (for type 'storage'), used root image space for VMs (for types 'qemu' and 'lxc').
  disk?: number;
  // The amount of bytes the guest read from its block devices since the guest was started. This info is not available for all storage types. (for types 'qemu' and 'lxc')
  diskread?: number;
  // The amount of bytes the guest wrote to its block devices since the guest was started. This info is not available for all storage types. (for types 'qemu' and 'lxc')
  diskwrite?: number;
  // HA service status (for HA managed VMs).
  hastate?: string;
  // Resource id.
  id: string;
  // Support level (for type 'node').
  level?: string;
  // The guest's current config lock (for types 'qemu' and 'lxc')
  lock?: string;
  // Number of available CPUs (for types 'node', 'qemu' and 'lxc').
  maxcpu?: number;
  // Storage size in bytes (for type 'storage'), root image size for VMs (for types 'qemu' and 'lxc').
  maxdisk?: number;
  // Number of available memory in bytes (for types 'node', 'qemu' and 'lxc').
  maxmem?: number;
  // Used memory in bytes (for types 'node', 'qemu' and 'lxc').
  mem?: number;
  // Name of the resource.
  name?: string;
  // The amount of traffic in bytes that was sent to the guest over the network since it was started. (for types 'qemu' and 'lxc')
  netin?: number;
  // The amount of traffic in bytes that was sent from the guest over the network since it was started. (for types 'qemu' and 'lxc')
  netout?: number;
  // The cluster node name (for types 'node', 'storage', 'qemu', and 'lxc').
  node?: string;
  // More specific type, if available.
  plugintype?: string;
  // The pool name (for types 'pool', 'qemu' and 'lxc').
  pool?: string;
  // Resource type dependent status.
  status?: string;
  // The storage identifier (for type 'storage').
  storage?: string;
  // The guest's tags (for types 'qemu' and 'lxc')
  tags?: string;
  // Determines if the guest is a template. (for types 'qemu' and 'lxc')
  template?: boolean;
  // Resource type.
  type: "node" | "storage" | "pool" | "qemu" | "lxc" | "openvz" | "sdn";
  // Uptime of node or virtual guest in seconds (for types 'node', 'qemu' and 'lxc').
  uptime?: number;
  // The numerical vmid (for types 'qemu' and 'lxc').
  vmid?: number;
}[];
```

## GET /api2/json/cluster/tasks

List recent tasks (cluster wide).

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  upid: string;
}[];
```

## GET /api2/json/cluster/options

Get datacenter options. Without 'Sys.Audit' on '/' not all options are returned.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/cluster/options

Set datacenter options.

### Input Parameters

```ts
interface Params {
  // Set I/O bandwidth limit for various operations (in KiB/s).
  bwlimit?: string;
  // Consent text that is displayed before logging in.
  "consent-text"?: string;
  // Select the default Console viewer. You can either use the builtin java applet (VNC; deprecated and maps to html5), an external virt-viewer comtatible application (SPICE), an HTML5 based vnc viewer (noVNC), or an HTML5 based console client (xtermjs). If the selected viewer is not available (e.g. SPICE not activated for the VM), the fallback is noVNC.
  console?: "applet" | "vv" | "html5" | "xtermjs";
  // Cluster resource scheduling settings.
  crs?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Datacenter description. Shown in the web-interface datacenter notes panel. This is saved as comment inside the configuration file.
  description?: string;
  // Specify email address to send notification from (default is root@$hostname)
  email_from?: string;
  // Set the fencing mode of the HA cluster. Hardware mode needs a valid configuration of fence devices in /etc/pve/ha/fence.cfg. With both all two modes are used.  WARNING: 'hardware' and 'both' are EXPERIMENTAL & WIP
  fencing?: "watchdog" | "hardware" | "both";
  // Cluster wide HA settings.
  ha?: string;
  // Specify external http proxy which is used for downloads (example: 'http://username:password@host:port/')
  http_proxy?: string;
  // Default keybord layout for vnc server.
  keyboard?:
    | "de"
    | "de-ch"
    | "da"
    | "en-gb"
    | "en-us"
    | "es"
    | "fi"
    | "fr"
    | "fr-be"
    | "fr-ca"
    | "fr-ch"
    | "hu"
    | "is"
    | "it"
    | "ja"
    | "lt"
    | "mk"
    | "nl"
    | "no"
    | "pl"
    | "pt"
    | "pt-br"
    | "sv"
    | "sl"
    | "tr";
  // Default GUI language.
  language?:
    | "ar"
    | "ca"
    | "da"
    | "de"
    | "en"
    | "es"
    | "eu"
    | "fa"
    | "fr"
    | "hr"
    | "he"
    | "it"
    | "ja"
    | "ka"
    | "kr"
    | "nb"
    | "nl"
    | "nn"
    | "pl"
    | "pt_BR"
    | "ru"
    | "sl"
    | "sv"
    | "tr"
    | "ukr"
    | "zh_CN"
    | "zh_TW";
  // Prefix for the auto-generated MAC addresses of virtual guests. The default 'BC:24:11' is the OUI assigned by the IEEE to Proxmox Server Solutions GmbH for a 24-bit large MAC block. You're allowed to use this in local networks, i.e., those not directly reachable by the public (e.g., in a LAN or behind NAT).
  mac_prefix?: string;
  // Defines how many workers (per node) are maximal started  on actions like 'stopall VMs' or task from the ha-manager.
  max_workers?: number;
  // For cluster wide migration settings.
  migration?: string;
  // Migration is secure using SSH tunnel by default. For secure private networks you can disable it to speed up migration. Deprecated, use the 'migration' property instead!
  migration_unsecure?: boolean;
  // Control the range for the free VMID auto-selection pool.
  "next-id"?: string;
  // Cluster-wide notification settings.
  notify?: string;
  // A list of tags that require a `Sys.Modify` on '/' to set and delete. Tags set here that are also in 'user-tag-access' also require `Sys.Modify`.
  "registered-tags"?: string;
  // Tag style options.
  "tag-style"?: string;
  // u2f
  u2f?: string;
  // Privilege options for user-settable tags
  "user-tag-access"?: string;
  // webauthn configuration
  webauthn?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/cluster/status

Get cluster status information.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  id: string;
  // [node] IP of the resolved nodename.
  ip?: string;
  // [node] Proxmox VE Subscription level, indicates if eligible for enterprise support as well as access to the stable Proxmox VE Enterprise Repository.
  level?: string;
  // [node] Indicates if this is the responding node.
  local?: boolean;
  name: string;
  // [node] ID of the node from the corosync configuration.
  nodeid?: number;
  // [cluster] Nodes count, including offline nodes.
  nodes?: number;
  // [node] Indicates if the node is online or offline.
  online?: boolean;
  // [cluster] Indicates if there is a majority of nodes online to make decisions
  quorate?: boolean;
  // Indicates the type, either cluster or node. The type defines the object properties e.g. quorate available for type cluster.
  type: "cluster" | "node";
  // [cluster] Current version of the corosync configuration file.
  version?: number;
}[];
```

## GET /api2/json/cluster/nextid

Get next free VMID. Pass a VMID to assert that its free (at time of check).

### Input Parameters

```ts
interface Params {
  // The (unique) ID of the VM.
  vmid?: number;
}
```

### Returns

```ts
type Returns = number;
```
