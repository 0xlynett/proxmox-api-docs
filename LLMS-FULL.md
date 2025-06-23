# Proxmox API Documentation for LLMs

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
  "comment"?: string;
  // Flag to disable/deactivate the entry.
  "disable"?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // Rate limit in mbps (megabytes per second) as floating point number.
  "rate"?: number;
  // Mark the replication job for removal. The job will remove all local replication snapshots. When set to 'full', it also tries to remove replicated volumes on the target. The job then removes itself from the configuration file.
  "remove_job"?: "local" | "full";
  // Storage replication schedule. The format is a subset of `systemd` calendar events.
  "schedule"?: string;
  // For internal use, to detect if the guest was stolen.
  "source"?: string;
  // Target node.
  "target": string;
  // Section type.
  "type": "local";
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
  "force"?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // Keep replicated data at target (do not remove).
  "keep"?: boolean;
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
  "id": string;
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Flag to disable/deactivate the entry.
  "disable"?: boolean;
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // Rate limit in mbps (megabytes per second) as floating point number.
  "rate"?: number;
  // Mark the replication job for removal. The job will remove all local replication snapshots. When set to 'full', it also tries to remove replicated volumes on the target. The job then removes itself from the configuration file.
  "remove_job"?: "local" | "full";
  // Storage replication schedule. The format is a subset of `systemd` calendar events.
  "schedule"?: string;
  // For internal use, to detect if the guest was stolen.
  "source"?: string;
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
  "id": string;
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
  "id": string;
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
  "bucket"?: string;
  // Flag to disable the plugin.
  "disable"?: boolean;
  // The ID of the entry.
  "id": string;
  "influxdbproto"?: "udp" | "http" | "https";
  // InfluxDB max-body-size in bytes. Requests are batched up to this size.
  "max-body-size"?: number;
  // MTU for metrics transmission over UDP
  "mtu"?: number;
  // The InfluxDB organization. Only necessary when using the http v2 api. Has no meaning when using v2 compatibility api.
  "organization"?: string;
  // root graphite path (ex: proxmox.mycluster.mykey)
  "path"?: string;
  // server network port
  "port": number;
  // Protocol to send graphite data. TCP or UDP (default)
  "proto"?: "udp" | "tcp";
  // server dns name or IP address
  "server": string;
  // graphite TCP socket timeout (default=1)
  "timeout"?: number;
  // The InfluxDB access token. Only necessary when using the http v2 api. If the v2 compatibility api is used, use 'user:password' instead.
  "token"?: string;
  // Plugin type.
  "type": "graphite" | "influxdb";
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
  "bucket"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Flag to disable the plugin.
  "disable"?: boolean;
  // The ID of the entry.
  "id": string;
  "influxdbproto"?: "udp" | "http" | "https";
  // InfluxDB max-body-size in bytes. Requests are batched up to this size.
  "max-body-size"?: number;
  // MTU for metrics transmission over UDP
  "mtu"?: number;
  // The InfluxDB organization. Only necessary when using the http v2 api. Has no meaning when using v2 compatibility api.
  "organization"?: string;
  // root graphite path (ex: proxmox.mycluster.mykey)
  "path"?: string;
  // server network port
  "port": number;
  // Protocol to send graphite data. TCP or UDP (default)
  "proto"?: "udp" | "tcp";
  // server dns name or IP address
  "server": string;
  // graphite TCP socket timeout (default=1)
  "timeout"?: number;
  // The InfluxDB access token. Only necessary when using the http v2 api. If the v2 compatibility api is used, use 'user:password' instead.
  "token"?: string;
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
  "history"?: boolean;
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
  "author"?: string;
  // Comment
  "comment"?: string;
  // Disable this target
  "disable"?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  "mailto"?: object[];
  // List of users
  "mailto-user"?: object[];
  // The name of the endpoint.
  "name": string;
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
  "name": string;
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
  "name": string;
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
  "author"?: string;
  // Comment
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable this target
  "disable"?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  "mailto"?: object[];
  // List of users
  "mailto-user"?: object[];
  // The name of the endpoint.
  "name": string;
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
  "comment"?: string;
  // Disable this target
  "disable"?: boolean;
  // The name of the endpoint.
  "name": string;
  // Server URL
  "server": string;
  // Secret token
  "token": string;
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
  "name": string;
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
  "name": string;
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable this target
  "disable"?: boolean;
  // The name of the endpoint.
  "name": string;
  // Server URL
  "server"?: string;
  // Secret token
  "token"?: string;
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
  "author"?: string;
  // Comment
  "comment"?: string;
  // Disable this target
  "disable"?: boolean;
  // `From` address for the mail
  "from-address": string;
  // List of email recipients
  "mailto"?: object[];
  // List of users
  "mailto-user"?: object[];
  // Determine which encryption method shall be used for the connection.
  "mode"?: "insecure" | "starttls" | "tls";
  // The name of the endpoint.
  "name": string;
  // Password for SMTP authentication
  "password"?: string;
  // The port to be used. Defaults to 465 for TLS based connections, 587 for STARTTLS based connections and port 25 for insecure plain-text connections.
  "port"?: number;
  // The address of the SMTP server.
  "server": string;
  // Username for SMTP authentication
  "username"?: string;
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
  "name": string;
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
  "name": string;
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
  "author"?: string;
  // Comment
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable this target
  "disable"?: boolean;
  // `From` address for the mail
  "from-address"?: string;
  // List of email recipients
  "mailto"?: object[];
  // List of users
  "mailto-user"?: object[];
  // Determine which encryption method shall be used for the connection.
  "mode"?: "insecure" | "starttls" | "tls";
  // The name of the endpoint.
  "name": string;
  // Password for SMTP authentication
  "password"?: string;
  // The port to be used. Defaults to 465 for TLS based connections, 587 for STARTTLS based connections and port 25 for insecure plain-text connections.
  "port"?: number;
  // The address of the SMTP server.
  "server"?: string;
  // Username for SMTP authentication
  "username"?: string;
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
  "body"?: string;
  // Comment
  "comment"?: string;
  // Disable this target
  "disable"?: boolean;
  // HTTP headers to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  "header"?: object[];
  // HTTP method
  "method": "post" | "put" | "get";
  // The name of the endpoint.
  "name": string;
  // Secrets to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  "secret"?: object[];
  // Server URL
  "url": string;
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
  "name": string;
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
  "name": string;
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
  "body"?: string;
  // Comment
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable this target
  "disable"?: boolean;
  // HTTP headers to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  "header"?: object[];
  // HTTP method
  "method"?: "post" | "put" | "get";
  // The name of the endpoint.
  "name": string;
  // Secrets to set. These have to be formatted as a property string in the format name=<name>,value=<base64 of value>
  "secret"?: object[];
  // Server URL
  "url"?: string;
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
  "name": string;
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
  "comment"?: string;
  // Disable this matcher
  "disable"?: boolean;
  // Invert match of the whole matcher
  "invert-match"?: boolean;
  // Match notification timestamp
  "match-calendar"?: object[];
  // Metadata fields to match (regex or exact match). Must be in the form (regex|exact):<field>=<value>
  "match-field"?: object[];
  // Notification severities to match
  "match-severity"?: object[];
  // Choose between 'all' and 'any' for when multiple properties are specified
  "mode"?: "all" | "any";
  // Name of the matcher.
  "name": string;
  // Targets to notify on match
  "target"?: object[];
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
  "name": string;
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
  "name": string;
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable this matcher
  "disable"?: boolean;
  // Invert match of the whole matcher
  "invert-match"?: boolean;
  // Match notification timestamp
  "match-calendar"?: object[];
  // Metadata fields to match (regex or exact match). Must be in the form (regex|exact):<field>=<value>
  "match-field"?: object[];
  // Notification severities to match
  "match-severity"?: object[];
  // Choose between 'all' and 'any' for when multiple properties are specified
  "mode"?: "all" | "any";
  // Name of the matcher.
  "name": string;
  // Targets to notify on match
  "target"?: object[];
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
  "clustername": string;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // Node id for this node.
  "nodeid"?: number;
  // Number of votes for this node.
  "votes"?: number;
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
  "node": string;
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
  "apiversion"?: number;
  // Do not throw error if node already exists.
  "force"?: boolean;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // IP Address of node to add. Used as fallback if no links are given.
  "new_node_ip"?: string;
  // The cluster node name.
  "node": string;
  // Node id for this node.
  "nodeid"?: number;
  // Number of votes for this node
  "votes"?: number;
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
  "node"?: string;
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
  "fingerprint": string;
  // Do not throw error if node already exists.
  "force"?: boolean;
  // Hostname (or IP) of an existing cluster member.
  "hostname": string;
  // Address and priority information of a single corosync link. (up to 8 links supported; link0..link7)
  "link[n]"?: string;
  // Node id for this node.
  "nodeid"?: number;
  // Superuser (root) password of peer node.
  "password": string;
  // Number of votes for this node
  "votes"?: number;
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
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Security Group name.
  "group": string;
  // Rename/update an existing security group. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing group.
  "rename"?: string;
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
  "group": string;
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
  "group": string;
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
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Security Group name.
  "group": string;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
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
  "digest"?: string;
  // Security Group name.
  "group": string;
  // Update rule at position <pos>.
  "pos"?: number;
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
  "group": string;
  // Update rule at position <pos>.
  "pos"?: number;
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
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Security Group name.
  "group": string;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
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
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
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
  "digest"?: string;
  // Update rule at position <pos>.
  "pos"?: number;
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
  "pos"?: number;
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
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
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
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // Rename an existing IPSet. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing IPSet.
  "rename"?: string;
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
  "force"?: boolean;
  // IP set name.
  "name": string;
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
  "name": string;
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
  "cidr": string;
  "comment"?: string;
  // IP set name.
  "name": string;
  "nomatch"?: boolean;
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
  "cidr": string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
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
  "cidr": string;
  // IP set name.
  "name": string;
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
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  "nomatch"?: boolean;
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
  "cidr": string;
  "comment"?: string;
  // Alias name.
  "name": string;
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
  "digest"?: string;
  // Alias name.
  "name": string;
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
  "name": string;
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
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Alias name.
  "name": string;
  // Rename an existing alias.
  "rename"?: string;
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
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable ebtables rules cluster wide.
  "ebtables"?: boolean;
  // Enable or disable the firewall cluster wide.
  "enable"?: number;
  // Log ratelimiting settings
  "log_ratelimit"?: string;
  // Forward policy.
  "policy_forward"?: "ACCEPT" | "DROP";
  // Input policy.
  "policy_in"?: "ACCEPT" | "REJECT" | "DROP";
  // Output policy.
  "policy_out"?: "ACCEPT" | "REJECT" | "DROP";
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
  "type"?: "alias" | "ipset";
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
  "all"?: boolean;
  // Limit I/O bandwidth (in KiB/s).
  "bwlimit"?: number;
  // Description for the Job.
  "comment"?: string;
  // Compress dump file.
  "compress"?: "0" | "1" | "gzip" | "lzo" | "zstd";
  // Day of week selection.
  "dow"?: string;
  // Store resulting files to specified directory.
  "dumpdir"?: string;
  // Enable or disable the job.
  "enabled"?: boolean;
  // Exclude specified guest systems (assumes --all)
  "exclude"?: string;
  // Exclude certain files/directories (shell globs). Paths starting with '/' are anchored to the container's root, other paths match relative to each subdirectory.
  "exclude-path"?: object[];
  // Options for backup fleecing (VM only).
  "fleecing"?: string;
  // Job ID (will be autogenerated).
  "id"?: string;
  // Set IO priority when using the BFQ scheduler. For snapshot and suspend mode backups of VMs, this only affects the compressor. A value of 8 means the idle priority is used, otherwise the best-effort priority is used with the specified value.
  "ionice"?: number;
  // Maximal time to wait for the global lock (minutes).
  "lockwait"?: number;
  // Deprecated: use notification targets/matchers instead. Specify when to send a notification mail
  "mailnotification"?: "always" | "failure";
  // Deprecated: Use notification targets/matchers instead. Comma-separated list of email addresses or users that should receive email notifications.
  "mailto"?: string;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per guest system.
  "maxfiles"?: number;
  // Backup mode.
  "mode"?: "snapshot" | "suspend" | "stop";
  // Only run if executed on this node.
  "node"?: string;
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
  "performance"?: string;
  // Use pigz instead of gzip when N>0. N=1 uses half of cores, N>1 uses N as thread count.
  "pigz"?: number;
  // Backup all known guest systems included in the specified pool.
  "pool"?: string;
  // If true, mark backup(s) as protected.
  "protected"?: boolean;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // Be quiet.
  "quiet"?: boolean;
  // Prune older backups according to 'prune-backups'.
  "remove"?: boolean;
  // If true, the job will be run as soon as possible if it was missed while the scheduler was not running.
  "repeat-missed"?: boolean;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  "schedule"?: string;
  // Use specified hook script.
  "script"?: string;
  // Job Start time.
  "starttime"?: string;
  // Exclude temporary files and logs.
  "stdexcludes"?: boolean;
  // Stop running backup jobs on this host.
  "stop"?: boolean;
  // Maximal time to wait until a guest system is stopped (minutes).
  "stopwait"?: number;
  // Store resulting file to this storage.
  "storage"?: string;
  // Store temporary files to specified directory.
  "tmpdir"?: string;
  // The ID of the guest system you want to backup.
  "vmid"?: string;
  // Zstd threads. N=0 uses half of the available cores, if N is set to a value bigger than 0, N is used as thread count.
  "zstd"?: number;
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
  "id": string;
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
  "id": string;
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
  "all"?: boolean;
  // Limit I/O bandwidth (in KiB/s).
  "bwlimit"?: number;
  // Description for the Job.
  "comment"?: string;
  // Compress dump file.
  "compress"?: "0" | "1" | "gzip" | "lzo" | "zstd";
  // A list of settings you want to delete.
  "delete"?: string;
  // Day of week selection.
  "dow"?: string;
  // Store resulting files to specified directory.
  "dumpdir"?: string;
  // Enable or disable the job.
  "enabled"?: boolean;
  // Exclude specified guest systems (assumes --all)
  "exclude"?: string;
  // Exclude certain files/directories (shell globs). Paths starting with '/' are anchored to the container's root, other paths match relative to each subdirectory.
  "exclude-path"?: object[];
  // Options for backup fleecing (VM only).
  "fleecing"?: string;
  // The job ID.
  "id": string;
  // Set IO priority when using the BFQ scheduler. For snapshot and suspend mode backups of VMs, this only affects the compressor. A value of 8 means the idle priority is used, otherwise the best-effort priority is used with the specified value.
  "ionice"?: number;
  // Maximal time to wait for the global lock (minutes).
  "lockwait"?: number;
  // Deprecated: use notification targets/matchers instead. Specify when to send a notification mail
  "mailnotification"?: "always" | "failure";
  // Deprecated: Use notification targets/matchers instead. Comma-separated list of email addresses or users that should receive email notifications.
  "mailto"?: string;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per guest system.
  "maxfiles"?: number;
  // Backup mode.
  "mode"?: "snapshot" | "suspend" | "stop";
  // Only run if executed on this node.
  "node"?: string;
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
  "performance"?: string;
  // Use pigz instead of gzip when N>0. N=1 uses half of cores, N>1 uses N as thread count.
  "pigz"?: number;
  // Backup all known guest systems included in the specified pool.
  "pool"?: string;
  // If true, mark backup(s) as protected.
  "protected"?: boolean;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // Be quiet.
  "quiet"?: boolean;
  // Prune older backups according to 'prune-backups'.
  "remove"?: boolean;
  // If true, the job will be run as soon as possible if it was missed while the scheduler was not running.
  "repeat-missed"?: boolean;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  "schedule"?: string;
  // Use specified hook script.
  "script"?: string;
  // Job Start time.
  "starttime"?: string;
  // Exclude temporary files and logs.
  "stdexcludes"?: boolean;
  // Stop running backup jobs on this host.
  "stop"?: boolean;
  // Maximal time to wait until a guest system is stopped (minutes).
  "stopwait"?: number;
  // Store resulting file to this storage.
  "storage"?: string;
  // Store temporary files to specified directory.
  "tmpdir"?: string;
  // The ID of the guest system you want to backup.
  "vmid"?: string;
  // Zstd threads. N=0 uses half of the available cores, if N is set to a value bigger than 0, N is used as thread count.
  "zstd"?: number;
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
  "id": string;
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
  "type"?: "ct" | "vm";
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
  "comment"?: string;
  // The HA group identifier.
  "group"?: string;
  // Maximal number of service relocate tries when a service failes to start.
  "max_relocate"?: number;
  // Maximal number of tries to restart the service on a node after its start failed.
  "max_restart"?: number;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  "sid": string;
  // Requested resource state.
  "state"?: "started" | "stopped" | "enabled" | "disabled" | "ignored";
  // Resource type.
  "type"?: "ct" | "vm";
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
  "sid": string;
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
  "sid": string;
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The HA group identifier.
  "group"?: string;
  // Maximal number of service relocate tries when a service failes to start.
  "max_relocate"?: number;
  // Maximal number of tries to restart the service on a node after its start failed.
  "max_restart"?: number;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  "sid": string;
  // Requested resource state.
  "state"?: "started" | "stopped" | "enabled" | "disabled" | "ignored";
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
  "node": string;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  "sid": string;
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
  "node": string;
  // HA resource ID. This consists of a resource type followed by a resource specific name, separated with colon (example: vm:100 / ct:100). For virtual machines and containers, you can simply use the VM or CT id as a shortcut (example: 100).
  "sid": string;
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
  "comment"?: string;
  // The HA group identifier.
  "group": string;
  // List of cluster node names with optional priority.
  "nodes": string;
  // The CRM tries to run services on the node with the highest priority. If a node with higher priority comes online, the CRM migrates the service to that node. Enabling nofailback prevents that behavior.
  "nofailback"?: boolean;
  // Resources bound to restricted groups may only run on nodes defined by the group.
  "restricted"?: boolean;
  // Group type.
  "type"?: "group";
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
  "group": string;
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
  "group": string;
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The HA group identifier.
  "group": string;
  // List of cluster node names with optional priority.
  "nodes"?: string;
  // The CRM tries to run services on the node with the highest priority. If a node with higher priority comes online, the CRM migrates the service to that node. Enabling nofailback prevents that behavior.
  "nofailback"?: boolean;
  // Resources bound to restricted groups may only run on nodes defined by the group.
  "restricted"?: boolean;
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
  "type"?: "dns" | "standalone";
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
  "api"?: "1984hosting" | "acmedns" | "acmeproxy" | "active24" | "ad" | "ali" | "alviy" | "anx" | "artfiles" | "arvan" | "aurora" | "autodns" | "aws" | "azion" | "azure" | "bookmyname" | "bunny" | "cf" | "clouddns" | "cloudns" | "cn" | "conoha" | "constellix" | "cpanel" | "curanet" | "cyon" | "da" | "ddnss" | "desec" | "df" | "dgon" | "dnsexit" | "dnshome" | "dnsimple" | "dnsservices" | "doapi" | "domeneshop" | "dp" | "dpi" | "dreamhost" | "duckdns" | "durabledns" | "dyn" | "dynu" | "dynv6" | "easydns" | "edgedns" | "euserv" | "exoscale" | "fornex" | "freedns" | "gandi_livedns" | "gcloud" | "gcore" | "gd" | "geoscaling" | "googledomains" | "he" | "hetzner" | "hexonet" | "hostingde" | "huaweicloud" | "infoblox" | "infomaniak" | "internetbs" | "inwx" | "ionos" | "ionos_cloud" | "ipv64" | "ispconfig" | "jd" | "joker" | "kappernet" | "kas" | "kinghost" | "knot" | "la" | "leaseweb" | "lexicon" | "limacity" | "linode" | "linode_v4" | "loopia" | "lua" | "maradns" | "me" | "miab" | "misaka" | "myapi" | "mydevil" | "mydnsjp" | "mythic_beasts" | "namecheap" | "namecom" | "namesilo" | "nanelo" | "nederhost" | "neodigit" | "netcup" | "netlify" | "nic" | "njalla" | "nm" | "nsd" | "nsone" | "nsupdate" | "nw" | "oci" | "omglol" | "one" | "online" | "openprovider" | "openstack" | "opnsense" | "ovh" | "pdns" | "pleskxml" | "pointhq" | "porkbun" | "rackcorp" | "rackspace" | "rage4" | "rcode0" | "regru" | "scaleway" | "schlundtech" | "selectel" | "selfhost" | "servercow" | "simply" | "technitium" | "tele3" | "tencent" | "timeweb" | "transip" | "udr" | "ultra" | "unoeuro" | "variomedia" | "veesp" | "vercel" | "vscale" | "vultr" | "websupport" | "west_cn" | "world4you" | "yandex360" | "yc" | "zilore" | "zone" | "zoneedit" | "zonomi";
  // DNS plugin data. (base64 encoded)
  "data"?: string;
  // Flag to disable the config.
  "disable"?: boolean;
  // ACME Plugin ID name
  "id": string;
  // List of cluster node names.
  "nodes"?: string;
  // ACME challenge type.
  "type": "dns" | "standalone";
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
  "id": string;
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
  "id": string;
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
  "api"?: "1984hosting" | "acmedns" | "acmeproxy" | "active24" | "ad" | "ali" | "alviy" | "anx" | "artfiles" | "arvan" | "aurora" | "autodns" | "aws" | "azion" | "azure" | "bookmyname" | "bunny" | "cf" | "clouddns" | "cloudns" | "cn" | "conoha" | "constellix" | "cpanel" | "curanet" | "cyon" | "da" | "ddnss" | "desec" | "df" | "dgon" | "dnsexit" | "dnshome" | "dnsimple" | "dnsservices" | "doapi" | "domeneshop" | "dp" | "dpi" | "dreamhost" | "duckdns" | "durabledns" | "dyn" | "dynu" | "dynv6" | "easydns" | "edgedns" | "euserv" | "exoscale" | "fornex" | "freedns" | "gandi_livedns" | "gcloud" | "gcore" | "gd" | "geoscaling" | "googledomains" | "he" | "hetzner" | "hexonet" | "hostingde" | "huaweicloud" | "infoblox" | "infomaniak" | "internetbs" | "inwx" | "ionos" | "ionos_cloud" | "ipv64" | "ispconfig" | "jd" | "joker" | "kappernet" | "kas" | "kinghost" | "knot" | "la" | "leaseweb" | "lexicon" | "limacity" | "linode" | "linode_v4" | "loopia" | "lua" | "maradns" | "me" | "miab" | "misaka" | "myapi" | "mydevil" | "mydnsjp" | "mythic_beasts" | "namecheap" | "namecom" | "namesilo" | "nanelo" | "nederhost" | "neodigit" | "netcup" | "netlify" | "nic" | "njalla" | "nm" | "nsd" | "nsone" | "nsupdate" | "nw" | "oci" | "omglol" | "one" | "online" | "openprovider" | "openstack" | "opnsense" | "ovh" | "pdns" | "pleskxml" | "pointhq" | "porkbun" | "rackcorp" | "rackspace" | "rage4" | "rcode0" | "regru" | "scaleway" | "schlundtech" | "selectel" | "selfhost" | "servercow" | "simply" | "technitium" | "tele3" | "tencent" | "timeweb" | "transip" | "udr" | "ultra" | "unoeuro" | "variomedia" | "veesp" | "vercel" | "vscale" | "vultr" | "websupport" | "west_cn" | "world4you" | "yandex360" | "yc" | "zilore" | "zone" | "zoneedit" | "zonomi";
  // DNS plugin data. (base64 encoded)
  "data"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Flag to disable the config.
  "disable"?: boolean;
  // ACME Plugin ID name
  "id": string;
  // List of cluster node names.
  "nodes"?: string;
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
  "contact": string;
  // URL of ACME CA directory endpoint.
  "directory"?: string;
  // HMAC key for External Account Binding.
  "eab-hmac-key"?: string;
  // Key Identifier for External Account Binding.
  "eab-kid"?: string;
  // ACME account config file name.
  "name"?: string;
  // URL of CA TermsOfService - setting this indicates agreement.
  "tos_url"?: string;
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
  "name"?: string;
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
  "name"?: string;
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
  "contact"?: string;
  // ACME account config file name.
  "name"?: string;
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
  "directory"?: string;
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
  "directory"?: string;
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
  "scope"?: "all" | "versions";
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
  name: "nobackfill" | "nodeep-scrub" | "nodown" | "noin" | "noout" | "norebalance" | "norecover" | "noscrub" | "notieragent" | "noup" | "pause";
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
  "nobackfill"?: boolean;
  // Deep Scrubbing is disabled.
  "nodeep-scrub"?: boolean;
  // OSD failure reports are being ignored, such that the monitors will not mark OSDs down.
  "nodown"?: boolean;
  // OSDs that were previously marked out will not be marked back in when they start.
  "noin"?: boolean;
  // OSDs will not automatically be marked out after the configured interval.
  "noout"?: boolean;
  // Rebalancing of PGs is suspended.
  "norebalance"?: boolean;
  // Recovery of PGs is suspended.
  "norecover"?: boolean;
  // Scrubbing is disabled.
  "noscrub"?: boolean;
  // Cache tiering activity is suspended.
  "notieragent"?: boolean;
  // OSDs are not allowed to start.
  "noup"?: boolean;
  // Pauses read and writes.
  "pause"?: boolean;
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
  "flag": "nobackfill" | "nodeep-scrub" | "nodown" | "noin" | "noout" | "norebalance" | "norecover" | "noscrub" | "notieragent" | "noup" | "pause";
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
  "flag": "nobackfill" | "nodeep-scrub" | "nodown" | "noin" | "noout" | "norebalance" | "norecover" | "noscrub" | "notieragent" | "noup" | "pause";
  // The new value of the flag
  "value": boolean;
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
  "id": string;
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
  "id": string;
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
  "comment"?: string;
  // Enable newly synced users immediately.
  "enable-new"?: boolean;
  // Determines if the job is enabled.
  "enabled"?: boolean;
  // The ID of the job.
  "id": string;
  // Authentication domain ID
  "realm"?: string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  "schedule": string;
  // Select what to sync.
  "scope"?: "users" | "groups" | "both";
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
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Enable newly synced users immediately.
  "enable-new"?: boolean;
  // Determines if the job is enabled.
  "enabled"?: boolean;
  // The ID of the job.
  "id": string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Backup schedule. The format is a subset of `systemd` calendar events.
  "schedule": string;
  // Select what to sync.
  "scope"?: "users" | "groups" | "both";
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
  "iterations"?: number;
  // Job schedule. The format is a subset of `systemd` calendar events.
  "schedule": string;
  // UNIX timestamp to start the calculation from. Defaults to the current time.
  "starttime"?: number;
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
  "description"?: string;
  // The ID of the directory mapping
  "id": string;
  // A list of maps for the cluster nodes.
  "map": object[];
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
  "id": string;
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
  "id": string;
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
  "delete"?: string;
  // Description of the directory mapping
  "description"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The ID of the directory mapping
  "id": string;
  // A list of maps for the cluster nodes.
  "map"?: object[];
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
  "description"?: string;
  // The ID of the logical PCI mapping.
  "id": string;
  // Marks the device(s) as being able to be live-migrated (Experimental). This needs hardware and driver support to work.
  "live-migration-capable"?: boolean;
  // A list of maps for the cluster nodes.
  "map": object[];
  // Marks the device(s) as being capable of providing mediated devices.
  "mdev"?: boolean;
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
  "id": string;
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
  "id": string;
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
  "delete"?: string;
  // Description of the logical PCI device.
  "description"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The ID of the logical PCI mapping.
  "id": string;
  // Marks the device(s) as being able to be live-migrated (Experimental). This needs hardware and driver support to work.
  "live-migration-capable"?: boolean;
  // A list of maps for the cluster nodes.
  "map"?: object[];
  // Marks the device(s) as being capable of providing mediated devices.
  "mdev"?: boolean;
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
  "description"?: string;
  // The ID of the logical USB mapping.
  "id": string;
  // A list of maps for the cluster nodes.
  "map": object[];
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
  "id": string;
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
  "id": string;
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
  "delete"?: string;
  // Description of the logical USB device.
  "description"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The ID of the logical USB mapping.
  "id": string;
  // A list of maps for the cluster nodes.
  "map": object[];
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
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
  "alias"?: string;
  // If true, sets the isolated property for all members of this VNet
  "isolate-ports"?: boolean;
  // vlan or vxlan id
  "tag"?: number;
  // Type
  "type"?: "vnet";
  // Allow vm VLANs to pass through this vnet.
  "vlanaware"?: boolean;
  // The SDN vnet object identifier.
  "vnet": string;
  // zone id
  "zone": string;
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
  "vnet": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "alias"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // If true, sets the isolated property for all members of this VNet
  "isolate-ports"?: boolean;
  // vlan or vxlan id
  "tag"?: number;
  // Allow vm VLANs to pass through this vnet.
  "vlanaware"?: boolean;
  // The SDN vnet object identifier.
  "vnet": string;
  // zone id
  "zone"?: string;
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
  "vnet": string;
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
  "vnet": string;
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
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
  // The SDN vnet object identifier.
  "vnet": string;
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
  "digest"?: string;
  // Update rule at position <pos>.
  "pos"?: number;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "pos"?: number;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
  // The SDN vnet object identifier.
  "vnet": string;
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
  "vnet": string;
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
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable/disable firewall rules.
  "enable"?: boolean;
  // Log level for forwarded traffic.
  "log_level_forward"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Forward policy.
  "policy_forward"?: "ACCEPT" | "DROP";
  // The SDN vnet object identifier.
  "vnet": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "dnszoneprefix"?: string;
  // Subnet Gateway: Will be assign on vnet for layer3 zones
  "gateway"?: string;
  // enable masquerade for this subnet if pve-firewall
  "snat"?: boolean;
  // The SDN subnet object identifier.
  "subnet": string;
  "type": "subnet";
  // associated vnet
  "vnet": string;
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
  "subnet": string;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // The SDN subnet object identifier.
  "subnet": string;
  // The SDN vnet object identifier.
  "vnet": string;
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
  "delete"?: string;
  // IP address for the DNS server
  "dhcp-dns-server"?: string;
  // A list of DHCP ranges for this subnet
  "dhcp-range"?: object[];
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // dns domain zone prefix  ex: 'adm' -> <hostname>.adm.mydomain.com
  "dnszoneprefix"?: string;
  // Subnet Gateway: Will be assign on vnet for layer3 zones
  "gateway"?: string;
  // enable masquerade for this subnet if pve-firewall
  "snat"?: boolean;
  // The SDN subnet object identifier.
  "subnet": string;
  // associated vnet
  "vnet"?: string;
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
  "ip": string;
  // Unicast MAC address.
  "mac"?: string;
  // The SDN vnet object identifier.
  "vnet": string;
  // The SDN zone object identifier.
  "zone": string;
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
  "ip": string;
  // Unicast MAC address.
  "mac"?: string;
  // The SDN vnet object identifier.
  "vnet": string;
  // The SDN zone object identifier.
  "zone": string;
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
  "ip": string;
  // Unicast MAC address.
  "mac"?: string;
  // The (unique) ID of the VM.
  "vmid"?: number;
  // The SDN vnet object identifier.
  "vnet": string;
  // The SDN zone object identifier.
  "zone": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // Only list SDN zones of specific type
  "type"?: "evpn" | "faucet" | "qinq" | "simple" | "vlan" | "vxlan";
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
  "bridge"?: string;
  // Disable auto mac learning.
  "bridge-disable-mac-learning"?: boolean;
  // Frr router name
  "controller"?: string;
  // Type of the DHCP backend for this zone
  "dhcp"?: "dnsmasq";
  // Disable ipv4 arp && ipv6 neighbour discovery suppression
  "disable-arp-nd-suppression"?: boolean;
  // dns api server
  "dns"?: string;
  // dns domain zone  ex: mydomain.com
  "dnszone"?: string;
  // Faucet dataplane id
  "dp-id"?: number;
  // List of cluster node names.
  "exitnodes"?: string;
  // Allow exitnodes to connect to evpn guests
  "exitnodes-local-routing"?: boolean;
  // Force traffic to this exitnode first.
  "exitnodes-primary"?: string;
  // use a specific ipam
  "ipam"?: string;
  // Anycast logical router mac address
  "mac"?: string;
  // MTU
  "mtu"?: number;
  // List of cluster node names.
  "nodes"?: string;
  // peers address list.
  "peers"?: string;
  // reverse dns api server
  "reversedns"?: string;
  // Route-Target import
  "rt-import"?: string;
  // Service-VLAN Tag
  "tag"?: number;
  // Plugin type.
  "type": "evpn" | "faucet" | "qinq" | "simple" | "vlan" | "vxlan";
  "vlan-protocol"?: "802.1q" | "802.1ad";
  // l3vni.
  "vrf-vxlan"?: number;
  // Vxlan tunnel udp port (default 4789).
  "vxlan-port"?: number;
  // The SDN zone object identifier.
  "zone": string;
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
  "zone": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // The SDN zone object identifier.
  "zone": string;
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
  "bridge"?: string;
  // Disable auto mac learning.
  "bridge-disable-mac-learning"?: boolean;
  // Frr router name
  "controller"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Type of the DHCP backend for this zone
  "dhcp"?: "dnsmasq";
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Disable ipv4 arp && ipv6 neighbour discovery suppression
  "disable-arp-nd-suppression"?: boolean;
  // dns api server
  "dns"?: string;
  // dns domain zone  ex: mydomain.com
  "dnszone"?: string;
  // Faucet dataplane id
  "dp-id"?: number;
  // List of cluster node names.
  "exitnodes"?: string;
  // Allow exitnodes to connect to evpn guests
  "exitnodes-local-routing"?: boolean;
  // Force traffic to this exitnode first.
  "exitnodes-primary"?: string;
  // use a specific ipam
  "ipam"?: string;
  // Anycast logical router mac address
  "mac"?: string;
  // MTU
  "mtu"?: number;
  // List of cluster node names.
  "nodes"?: string;
  // peers address list.
  "peers"?: string;
  // reverse dns api server
  "reversedns"?: string;
  // Route-Target import
  "rt-import"?: string;
  // Service-VLAN Tag
  "tag"?: number;
  "vlan-protocol"?: "802.1q" | "802.1ad";
  // l3vni.
  "vrf-vxlan"?: number;
  // Vxlan tunnel udp port (default 4789).
  "vxlan-port"?: number;
  // The SDN zone object identifier.
  "zone": string;
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
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
  // Only list sdn controllers of specific type
  "type"?: "bgp" | "evpn" | "faucet" | "isis";
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
  "asn"?: number;
  "bgp-multipath-as-path-relax"?: boolean;
  // The SDN controller object identifier.
  "controller": string;
  // Enable ebgp. (remote-as external)
  "ebgp"?: boolean;
  "ebgp-multihop"?: number;
  // ISIS domain.
  "isis-domain"?: string;
  // ISIS interface.
  "isis-ifaces"?: string;
  // ISIS network entity title.
  "isis-net"?: string;
  // source loopback interface.
  "loopback"?: string;
  // The cluster node name.
  "node"?: string;
  // peers address list.
  "peers"?: string;
  // Plugin type.
  "type": "bgp" | "evpn" | "faucet" | "isis";
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
  "controller": string;
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
  "controller": string;
  // Display pending config.
  "pending"?: boolean;
  // Display running config.
  "running"?: boolean;
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
  "asn"?: number;
  "bgp-multipath-as-path-relax"?: boolean;
  // The SDN controller object identifier.
  "controller": string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable ebgp. (remote-as external)
  "ebgp"?: boolean;
  "ebgp-multihop"?: number;
  // ISIS domain.
  "isis-domain"?: string;
  // ISIS interface.
  "isis-ifaces"?: string;
  // ISIS network entity title.
  "isis-net"?: string;
  // source loopback interface.
  "loopback"?: string;
  // The cluster node name.
  "node"?: string;
  // peers address list.
  "peers"?: string;
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
  "type"?: "netbox" | "phpipam" | "pve";
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
  "fingerprint"?: string;
  // The SDN ipam object identifier.
  "ipam": string;
  "section"?: number;
  "token"?: string;
  // Plugin type.
  "type": "netbox" | "phpipam" | "pve";
  "url"?: string;
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
  "ipam": string;
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
  "ipam": string;
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
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  // The SDN ipam object identifier.
  "ipam": string;
  "section"?: number;
  "token"?: string;
  "url"?: string;
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
  "ipam": string;
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
  "type"?: "powerdns";
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
  "dns": string;
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  "key": string;
  "reversemaskv6"?: number;
  "reversev6mask"?: number;
  "ttl"?: number;
  // Plugin type.
  "type": "powerdns";
  "url": string;
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
  "dns": string;
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
  "dns": string;
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
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The SDN dns object identifier.
  "dns": string;
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  "key"?: string;
  "reversemaskv6"?: number;
  "ttl"?: number;
  "url"?: string;
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
  "max"?: number;
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
  "type"?: "vm" | "storage" | "node" | "sdn";
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
  "bwlimit"?: string;
  // Consent text that is displayed before logging in.
  "consent-text"?: string;
  // Select the default Console viewer. You can either use the builtin java applet (VNC; deprecated and maps to html5), an external virt-viewer comtatible application (SPICE), an HTML5 based vnc viewer (noVNC), or an HTML5 based console client (xtermjs). If the selected viewer is not available (e.g. SPICE not activated for the VM), the fallback is noVNC.
  "console"?: "applet" | "vv" | "html5" | "xtermjs";
  // Cluster resource scheduling settings.
  "crs"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Datacenter description. Shown in the web-interface datacenter notes panel. This is saved as comment inside the configuration file.
  "description"?: string;
  // Specify email address to send notification from (default is root@$hostname)
  "email_from"?: string;
  // Set the fencing mode of the HA cluster. Hardware mode needs a valid configuration of fence devices in /etc/pve/ha/fence.cfg. With both all two modes are used.  WARNING: 'hardware' and 'both' are EXPERIMENTAL & WIP
  "fencing"?: "watchdog" | "hardware" | "both";
  // Cluster wide HA settings.
  "ha"?: string;
  // Specify external http proxy which is used for downloads (example: 'http://username:password@host:port/')
  "http_proxy"?: string;
  // Default keybord layout for vnc server.
  "keyboard"?: "de" | "de-ch" | "da" | "en-gb" | "en-us" | "es" | "fi" | "fr" | "fr-be" | "fr-ca" | "fr-ch" | "hu" | "is" | "it" | "ja" | "lt" | "mk" | "nl" | "no" | "pl" | "pt" | "pt-br" | "sv" | "sl" | "tr";
  // Default GUI language.
  "language"?: "ar" | "ca" | "da" | "de" | "en" | "es" | "eu" | "fa" | "fr" | "hr" | "he" | "it" | "ja" | "ka" | "kr" | "nb" | "nl" | "nn" | "pl" | "pt_BR" | "ru" | "sl" | "sv" | "tr" | "ukr" | "zh_CN" | "zh_TW";
  // Prefix for the auto-generated MAC addresses of virtual guests. The default 'BC:24:11' is the OUI assigned by the IEEE to Proxmox Server Solutions GmbH for a 24-bit large MAC block. You're allowed to use this in local networks, i.e., those not directly reachable by the public (e.g., in a LAN or behind NAT).
  "mac_prefix"?: string;
  // Defines how many workers (per node) are maximal started  on actions like 'stopall VMs' or task from the ha-manager.
  "max_workers"?: number;
  // For cluster wide migration settings.
  "migration"?: string;
  // Migration is secure using SSH tunnel by default. For secure private networks you can disable it to speed up migration. Deprecated, use the 'migration' property instead!
  "migration_unsecure"?: boolean;
  // Control the range for the free VMID auto-selection pool.
  "next-id"?: string;
  // Cluster-wide notification settings.
  "notify"?: string;
  // A list of tags that require a `Sys.Modify` on '/' to set and delete. Tags set here that are also in 'user-tag-access' also require `Sys.Modify`.
  "registered-tags"?: string;
  // Tag style options.
  "tag-style"?: string;
  // u2f
  "u2f"?: string;
  // Privilege options for user-settable tags
  "user-tag-access"?: string;
  // webauthn configuration
  "webauthn"?: string;
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
  "vmid"?: number;
}
```

### Returns

```ts
type Returns = number;
```

## GET /api2/json/nodes

Cluster node index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // CPU utilization.
  cpu?: number;
  // Support level.
  level?: string;
  // Number of available CPUs.
  maxcpu?: number;
  // Number of available memory in bytes.
  maxmem?: number;
  // Used memory in bytes.
  mem?: number;
  // The cluster node name.
  node: string;
  // The SSL fingerprint for the node certificate.
  ssl_fingerprint?: string;
  // Node status.
  status: "unknown" | "online" | "offline";
  // Node uptime in seconds.
  uptime?: number;
}[];
```

## GET /api2/json/nodes/{node}

Node index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/qemu

Virtual machine index (per node).

### Input Parameters

```ts
interface Params {
  // Determine the full status of active VMs.
  "full"?: boolean;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // Current CPU usage.
  cpu?: number;
  // Maximum usable CPUs.
  cpus?: number;
  // The amount of bytes the guest read from it's block devices since the guest was started. (Note: This info is not available for all storage types.)
  diskread?: number;
  // The amount of bytes the guest wrote from it's block devices since the guest was started. (Note: This info is not available for all storage types.)
  diskwrite?: number;
  // The current config lock, if any.
  lock?: string;
  // Root disk size in bytes.
  maxdisk?: number;
  // Maximum memory in bytes.
  maxmem?: number;
  // Currently used memory in bytes.
  mem?: number;
  // VM (host)name.
  name?: string;
  // The amount of traffic in bytes that was sent to the guest over the network since it was started.
  netin?: number;
  // The amount of traffic in bytes that was sent from the guest over the network since it was started.
  netout?: number;
  // PID of the QEMU process, if the VM is running.
  pid?: number;
  // VM run state from the 'query-status' QMP monitor command.
  qmpstatus?: string;
  // The currently running machine type (if running).
  running-machine?: string;
  // The QEMU version the VM is currently using (if running).
  running-qemu?: string;
  // Guest has serial device configured.
  serial?: boolean;
  // QEMU process status.
  status: "stopped" | "running";
  // The current configured tags, if any
  tags?: string;
  // Determines if the guest is a template.
  template?: boolean;
  // Uptime in seconds.
  uptime?: number;
  // The (unique) ID of the VM.
  vmid: number;
}[];
```

## POST /api2/json/nodes/{node}/qemu

Create or restore a virtual machine.

### Input Parameters

```ts
interface Params {
  // Enable/disable ACPI.
  "acpi"?: boolean;
  // List of host cores used to execute guest processes, for example: 0,5,8-11
  "affinity"?: string;
  // Enable/disable communication with the QEMU Guest Agent and its properties.
  "agent"?: string;
  // Secure Encrypted Virtualization (SEV) features by AMD CPUs
  "amd-sev"?: string;
  // Virtual processor architecture. Defaults to the host.
  "arch"?: "x86_64" | "aarch64";
  // The backup archive. Either the file system path to a .tar or .vma file (use '-' to pipe data from stdin) or a proxmox storage backup volume identifier.
  "archive"?: string;
  // Arbitrary arguments passed to kvm.
  "args"?: string;
  // Configure a audio device, useful in combination with QXL/Spice.
  "audio0"?: string;
  // Automatic restart after crash (currently ignored).
  "autostart"?: boolean;
  // Amount of target RAM for the VM in MiB. Using zero disables the ballon driver.
  "balloon"?: number;
  // Select BIOS implementation.
  "bios"?: "seabios" | "ovmf";
  // Specify guest boot order. Use the 'order=' sub-property as usage with no key or 'legacy=' is deprecated.
  "boot"?: string;
  // Enable booting from specified disk. Deprecated: Use 'boot: order=foo;bar' instead.
  "bootdisk"?: string;
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // This is an alias for option -ide2
  "cdrom"?: string;
  // cloud-init: Specify custom files to replace the automatically generated ones at start.
  "cicustom"?: string;
  // cloud-init: Password to assign the user. Using this is generally not recommended. Use ssh keys instead. Also note that older cloud-init versions do not support hashed passwords.
  "cipassword"?: string;
  // Specifies the cloud-init configuration format. The default depends on the configured operating system type (`ostype`. We use the `nocloud` format for Linux, and `configdrive2` for windows.
  "citype"?: "configdrive2" | "nocloud" | "opennebula";
  // cloud-init: do an automatic package upgrade after the first boot.
  "ciupgrade"?: boolean;
  // cloud-init: User name to change ssh keys and password for instead of the image's configured default user.
  "ciuser"?: string;
  // The number of cores per socket.
  "cores"?: number;
  // Emulated CPU type.
  "cpu"?: string;
  // Limit of CPU usage.
  "cpulimit"?: number;
  // CPU weight for a VM, will be clamped to [1, 10000] in cgroup v2.
  "cpuunits"?: number;
  // Description for the VM. Shown in the web-interface VM's summary. This is saved as comment inside the configuration file.
  "description"?: string;
  // Configure a disk for storing EFI vars. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and that the default EFI vars are copied to the volume instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "efidisk0"?: string;
  // Allow to overwrite existing VM.
  "force"?: boolean;
  // Freeze CPU at startup (use 'c' monitor command to start execution).
  "freeze"?: boolean;
  // Script that will be executed during various steps in the vms lifetime.
  "hookscript"?: string;
  // Map host PCI devices into guest.
  "hostpci[n]"?: string;
  // Selectively enable hotplug features. This is a comma separated list of hotplug features: 'network', 'disk', 'cpu', 'memory', 'usb' and 'cloudinit'. Use '0' to disable hotplug completely. Using '1' as value is an alias for the default `network,disk,usb`. USB hotplugging is possible for guests with machine version >= 7.1 and ostype l26 or windows > 7.
  "hotplug"?: string;
  // Enable/disable hugepages memory.
  "hugepages"?: "any" | "2" | "1024";
  // Use volume as IDE hard disk or CD-ROM (n is 0 to 3). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "ide[n]"?: string;
  // A file-based storage with 'images' content-type enabled, which is used as an intermediary extraction storage during import. Defaults to the source storage.
  "import-working-storage"?: string;
  // cloud-init: Specify IP addresses and gateways for the corresponding interface.  IP addresses use CIDR notation, gateways are optional but need an IP of the same type specified.  The special string 'dhcp' can be used for IP addresses to use DHCP, in which case no explicit gateway should be provided. For IPv6 the special string 'auto' can be used to use stateless autoconfiguration. This requires cloud-init 19.4 or newer.  If cloud-init is enabled and neither an IPv4 nor an IPv6 address is specified, it defaults to using dhcp on IPv4. 
  "ipconfig[n]"?: string;
  // Inter-VM shared memory. Useful for direct communication between VMs, or to the host.
  "ivshmem"?: string;
  // Use together with hugepages. If enabled, hugepages will not not be deleted after VM shutdown and can be used for subsequent starts.
  "keephugepages"?: boolean;
  // Keyboard layout for VNC server. This option is generally not required and is often better handled from within the guest OS.
  "keyboard"?: "de" | "de-ch" | "da" | "en-gb" | "en-us" | "es" | "fi" | "fr" | "fr-be" | "fr-ca" | "fr-ch" | "hu" | "is" | "it" | "ja" | "lt" | "mk" | "nl" | "no" | "pl" | "pt" | "pt-br" | "sv" | "sl" | "tr";
  // Enable/disable KVM hardware virtualization.
  "kvm"?: boolean;
  // Start the VM immediately while importing or restoring in the background.
  "live-restore"?: boolean;
  // Set the real time clock (RTC) to local time. This is enabled by default if the `ostype` indicates a Microsoft Windows OS.
  "localtime"?: boolean;
  // Lock/unlock the VM.
  "lock"?: "backup" | "clone" | "create" | "migrate" | "rollback" | "snapshot" | "snapshot-delete" | "suspending" | "suspended";
  // Specify the QEMU machine.
  "machine"?: string;
  // Memory properties.
  "memory"?: string;
  // Set maximum tolerated downtime (in seconds) for migrations. Should the migration not be able to converge in the very end, because too much newly dirtied RAM needs to be transferred, the limit will be increased automatically step-by-step until migration can converge.
  "migrate_downtime"?: number;
  // Set maximum speed (in MB/s) for migrations. Value 0 is no limit.
  "migrate_speed"?: number;
  // Set a name for the VM. Only used on the configuration web interface.
  "name"?: string;
  // cloud-init: Sets DNS server IP address for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "nameserver"?: string;
  // Specify network devices.
  "net[n]"?: string;
  // The cluster node name.
  "node": string;
  // Enable/disable NUMA.
  "numa"?: boolean;
  // NUMA topology.
  "numa[n]"?: string;
  // Specifies whether a VM will be started during system bootup.
  "onboot"?: boolean;
  // Specify guest operating system.
  "ostype"?: "other" | "wxp" | "w2k" | "w2k3" | "w2k8" | "wvista" | "win7" | "win8" | "win10" | "win11" | "l24" | "l26" | "solaris";
  // Map host parallel devices (n is 0 to 2).
  "parallel[n]"?: string;
  // Add the VM to the specified pool.
  "pool"?: string;
  // Sets the protection flag of the VM. This will disable the remove VM and remove disk operations.
  "protection"?: boolean;
  // Allow reboot. If set to '0' the VM exit on reboot.
  "reboot"?: boolean;
  // Configure a VirtIO-based Random Number Generator.
  "rng0"?: string;
  // Use volume as SATA hard disk or CD-ROM (n is 0 to 5). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "sata[n]"?: string;
  // Use volume as SCSI hard disk or CD-ROM (n is 0 to 30). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "scsi[n]"?: string;
  // SCSI controller model
  "scsihw"?: "lsi" | "lsi53c810" | "virtio-scsi-pci" | "virtio-scsi-single" | "megasas" | "pvscsi";
  // cloud-init: Sets DNS search domains for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "searchdomain"?: string;
  // Create a serial device inside the VM (n is 0 to 3)
  "serial[n]"?: string;
  // Amount of memory shares for auto-ballooning. The larger the number is, the more memory this VM gets. Number is relative to weights of all other running VMs. Using zero disables auto-ballooning. Auto-ballooning is done by pvestatd.
  "shares"?: number;
  // Specify SMBIOS type 1 fields.
  "smbios1"?: string;
  // The number of CPUs. Please use option -sockets instead.
  "smp"?: number;
  // The number of CPU sockets.
  "sockets"?: number;
  // Configure additional enhancements for SPICE.
  "spice_enhancements"?: string;
  // cloud-init: Setup public SSH keys (one key per line, OpenSSH format).
  "sshkeys"?: string;
  // Start VM after it was created successfully.
  "start"?: boolean;
  // Set the initial date of the real time clock. Valid format for date are:'now' or '2006-06-17T16:01:21' or '2006-06-17'.
  "startdate"?: string;
  // Startup and shutdown behavior. Order is a non-negative number defining the general startup order. Shutdown in done with reverse ordering. Additionally you can set the 'up' or 'down' delay in seconds, which specifies a delay to wait before the next VM is started or stopped.
  "startup"?: string;
  // Default storage.
  "storage"?: string;
  // Enable/disable the USB tablet device.
  "tablet"?: boolean;
  // Tags of the VM. This is only meta information.
  "tags"?: string;
  // Enable/disable time drift fix.
  "tdf"?: boolean;
  // Enable/disable Template.
  "template"?: boolean;
  // Configure a Disk for storing TPM state. The format is fixed to 'raw'. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and 4 MiB will be used instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "tpmstate0"?: string;
  // Assign a unique random ethernet address.
  "unique"?: boolean;
  // Reference to unused volumes. This is used internally, and should not be modified manually.
  "unused[n]"?: string;
  // Configure an USB device (n is 0 to 4, for machine version >= 7.1 and ostype l26 or windows > 7, n can be up to 14).
  "usb[n]"?: string;
  // Number of hotplugged vcpus.
  "vcpus"?: number;
  // Configure the VGA hardware.
  "vga"?: string;
  // Use volume as VIRTIO hard disk (n is 0 to 15). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "virtio[n]"?: string;
  // Configuration for sharing a directory between host and guest using Virtio-fs.
  "virtiofs[n]"?: string;
  // Set VM Generation ID. Use '1' to autogenerate on create or update, pass '0' to disable explicitly.
  "vmgenid"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Default storage for VM state volumes/files.
  "vmstatestorage"?: string;
  // Create a virtual hardware watchdog device.
  "watchdog"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}

Destroy the VM and  all used/owned volumes. Removes any VM specific permissions and firewall rules

### Input Parameters

```ts
interface Params {
  // If set, destroy additionally all disks not referenced in the config but with a matching VMID from all enabled storages.
  "destroy-unreferenced-disks"?: boolean;
  // The cluster node name.
  "node": string;
  // Remove VMID from configurations, like backup & replication jobs and HA.
  "purge"?: boolean;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}

Directory index

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/rules

List rules.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/firewall/rules

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}/firewall/rules/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/rules/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/firewall/rules/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/aliases

List aliases

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
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

## POST /api2/json/nodes/{node}/qemu/{vmid}/firewall/aliases

Create IP or Network Alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}/firewall/aliases/{name}

Remove IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/aliases/{name}

Read alias.

### Input Parameters

```ts
interface Params {
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/firewall/aliases/{name}

Update IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // Rename an existing alias.
  "rename"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset

List IPSets

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
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

## POST /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset

Create new IPSet

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // Rename an existing IPSet. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing IPSet.
  "rename"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}

Delete IPSet

### Input Parameters

```ts
interface Params {
  // Delete all members of the IPSet, if there are any.
  "force"?: boolean;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}

List IPSet content

### Input Parameters

```ts
interface Params {
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
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

## POST /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}

Add IP or Network to IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  "nomatch"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}/{cidr}

Remove IP or Network from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}/{cidr}

Read IP or Network settings from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/firewall/ipset/{name}/{cidr}

Update IP or Network settings

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  "nomatch"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/options

Get VM firewall options.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/firewall/options

Set Firewall options.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  "delete"?: string;
  // Enable DHCP.
  "dhcp"?: boolean;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable/disable firewall rules.
  "enable"?: boolean;
  // Enable default IP filters. This is equivalent to adding an empty ipfilter-net<id> ipset for every interface. Such ipsets implicitly contain sane default restrictions such as restricting IPv6 link local addresses to the one derived from the interface's MAC address. For containers the configured IP addresses will be implicitly added.
  "ipfilter"?: boolean;
  // Log level for incoming traffic.
  "log_level_in"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Log level for outgoing traffic.
  "log_level_out"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Enable/disable MAC address filter.
  "macfilter"?: boolean;
  // Enable NDP (Neighbor Discovery Protocol).
  "ndp"?: boolean;
  // The cluster node name.
  "node": string;
  // Input policy.
  "policy_in"?: "ACCEPT" | "REJECT" | "DROP";
  // Output policy.
  "policy_out"?: "ACCEPT" | "REJECT" | "DROP";
  // Allow sending Router Advertisement.
  "radv"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/log

Read firewall log

### Input Parameters

```ts
interface Params {
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Display log since this UNIX epoch.
  "since"?: number;
  "start"?: number;
  // Display log until this UNIX epoch.
  "until"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/firewall/refs

Lists possible IPSet/Alias reference which are allowed in source/dest properties.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Only list references of specified type.
  "type"?: "alias" | "ipset";
  // The (unique) ID of the VM.
  "vmid": number;
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

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent

QEMU Guest Agent command index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent

Execute QEMU Guest Agent commands.

### Input Parameters

```ts
interface Params {
  // The QGA command.
  "command": "fsfreeze-freeze" | "fsfreeze-status" | "fsfreeze-thaw" | "fstrim" | "get-fsinfo" | "get-host-name" | "get-memory-block-info" | "get-memory-blocks" | "get-osinfo" | "get-time" | "get-timezone" | "get-users" | "get-vcpus" | "info" | "network-get-interfaces" | "ping" | "shutdown" | "suspend-disk" | "suspend-hybrid" | "suspend-ram";
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/fsfreeze-freeze

Execute fsfreeze-freeze.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/fsfreeze-status

Execute fsfreeze-status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/fsfreeze-thaw

Execute fsfreeze-thaw.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/fstrim

Execute fstrim.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-fsinfo

Execute get-fsinfo.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-host-name

Execute get-host-name.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-memory-block-info

Execute get-memory-block-info.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-memory-blocks

Execute get-memory-blocks.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-osinfo

Execute get-osinfo.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-time

Execute get-time.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-timezone

Execute get-timezone.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-users

Execute get-users.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/get-vcpus

Execute get-vcpus.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/info

Execute info.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/network-get-interfaces

Execute network-get-interfaces.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/ping

Execute ping.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/shutdown

Execute shutdown.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/suspend-disk

Execute suspend-disk.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/suspend-hybrid

Execute suspend-hybrid.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/suspend-ram

Execute suspend-ram.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/set-user-password

Sets the password for the given user to the given password

### Input Parameters

```ts
interface Params {
  // set to 1 if the password has already been passed through crypt()
  "crypted"?: boolean;
  // The cluster node name.
  "node": string;
  // The new password.
  "password": string;
  // The user to set the password for.
  "username": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/exec

Executes the given command in the vm via the guest-agent and returns an object with the pid.

### Input Parameters

```ts
interface Params {
  // The command as a list of program + arguments.
  "command": object[];
  // Data to pass as 'input-data' to the guest. Usually treated as STDIN to 'command'.
  "input-data"?: string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/exec-status

Gets the status of the given pid started by the guest-agent

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The PID to query
  "pid": number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/agent/file-read

Reads the given file via guest agent. Is limited to 16777216 bytes.

### Input Parameters

```ts
interface Params {
  // The path to the file
  "file": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/agent/file-write

Writes the given file via guest agent.

### Input Parameters

```ts
interface Params {
  // The content to write into the file.
  "content": string;
  // If set, the content will be encoded as base64 (required by QEMU).Otherwise the content needs to be encoded beforehand - defaults to true.
  "encode"?: boolean;
  // The path to the file.
  "file": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/rrd

Read VM RRD statistics (returns PNG)

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The list of datasources you want to display.
  "ds": string;
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/rrddata

Read VM RRD statistics

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/config

Get the virtual machine configuration with pending configuration changes applied. Set the 'current' parameter to get the current configuration instead.

### Input Parameters

```ts
interface Params {
  // Get current values (instead of pending values).
  "current"?: boolean;
  // The cluster node name.
  "node": string;
  // Fetch config values from given snapshot.
  "snapshot"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/config

Set virtual machine options (asynchronous API).

### Input Parameters

```ts
interface Params {
  // Enable/disable ACPI.
  "acpi"?: boolean;
  // List of host cores used to execute guest processes, for example: 0,5,8-11
  "affinity"?: string;
  // Enable/disable communication with the QEMU Guest Agent and its properties.
  "agent"?: string;
  // Secure Encrypted Virtualization (SEV) features by AMD CPUs
  "amd-sev"?: string;
  // Virtual processor architecture. Defaults to the host.
  "arch"?: "x86_64" | "aarch64";
  // Arbitrary arguments passed to kvm.
  "args"?: string;
  // Configure a audio device, useful in combination with QXL/Spice.
  "audio0"?: string;
  // Automatic restart after crash (currently ignored).
  "autostart"?: boolean;
  // Time to wait for the task to finish. We return 'null' if the task finish within that time.
  "background_delay"?: number;
  // Amount of target RAM for the VM in MiB. Using zero disables the ballon driver.
  "balloon"?: number;
  // Select BIOS implementation.
  "bios"?: "seabios" | "ovmf";
  // Specify guest boot order. Use the 'order=' sub-property as usage with no key or 'legacy=' is deprecated.
  "boot"?: string;
  // Enable booting from specified disk. Deprecated: Use 'boot: order=foo;bar' instead.
  "bootdisk"?: string;
  // This is an alias for option -ide2
  "cdrom"?: string;
  // cloud-init: Specify custom files to replace the automatically generated ones at start.
  "cicustom"?: string;
  // cloud-init: Password to assign the user. Using this is generally not recommended. Use ssh keys instead. Also note that older cloud-init versions do not support hashed passwords.
  "cipassword"?: string;
  // Specifies the cloud-init configuration format. The default depends on the configured operating system type (`ostype`. We use the `nocloud` format for Linux, and `configdrive2` for windows.
  "citype"?: "configdrive2" | "nocloud" | "opennebula";
  // cloud-init: do an automatic package upgrade after the first boot.
  "ciupgrade"?: boolean;
  // cloud-init: User name to change ssh keys and password for instead of the image's configured default user.
  "ciuser"?: string;
  // The number of cores per socket.
  "cores"?: number;
  // Emulated CPU type.
  "cpu"?: string;
  // Limit of CPU usage.
  "cpulimit"?: number;
  // CPU weight for a VM, will be clamped to [1, 10000] in cgroup v2.
  "cpuunits"?: number;
  // A list of settings you want to delete.
  "delete"?: string;
  // Description for the VM. Shown in the web-interface VM's summary. This is saved as comment inside the configuration file.
  "description"?: string;
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Configure a disk for storing EFI vars. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and that the default EFI vars are copied to the volume instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "efidisk0"?: string;
  // Force physical removal. Without this, we simple remove the disk from the config file and create an additional configuration entry called 'unused[n]', which contains the volume ID. Unlink of unused[n] always cause physical removal.
  "force"?: boolean;
  // Freeze CPU at startup (use 'c' monitor command to start execution).
  "freeze"?: boolean;
  // Script that will be executed during various steps in the vms lifetime.
  "hookscript"?: string;
  // Map host PCI devices into guest.
  "hostpci[n]"?: string;
  // Selectively enable hotplug features. This is a comma separated list of hotplug features: 'network', 'disk', 'cpu', 'memory', 'usb' and 'cloudinit'. Use '0' to disable hotplug completely. Using '1' as value is an alias for the default `network,disk,usb`. USB hotplugging is possible for guests with machine version >= 7.1 and ostype l26 or windows > 7.
  "hotplug"?: string;
  // Enable/disable hugepages memory.
  "hugepages"?: "any" | "2" | "1024";
  // Use volume as IDE hard disk or CD-ROM (n is 0 to 3). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "ide[n]"?: string;
  // A file-based storage with 'images' content-type enabled, which is used as an intermediary extraction storage during import. Defaults to the source storage.
  "import-working-storage"?: string;
  // cloud-init: Specify IP addresses and gateways for the corresponding interface.  IP addresses use CIDR notation, gateways are optional but need an IP of the same type specified.  The special string 'dhcp' can be used for IP addresses to use DHCP, in which case no explicit gateway should be provided. For IPv6 the special string 'auto' can be used to use stateless autoconfiguration. This requires cloud-init 19.4 or newer.  If cloud-init is enabled and neither an IPv4 nor an IPv6 address is specified, it defaults to using dhcp on IPv4. 
  "ipconfig[n]"?: string;
  // Inter-VM shared memory. Useful for direct communication between VMs, or to the host.
  "ivshmem"?: string;
  // Use together with hugepages. If enabled, hugepages will not not be deleted after VM shutdown and can be used for subsequent starts.
  "keephugepages"?: boolean;
  // Keyboard layout for VNC server. This option is generally not required and is often better handled from within the guest OS.
  "keyboard"?: "de" | "de-ch" | "da" | "en-gb" | "en-us" | "es" | "fi" | "fr" | "fr-be" | "fr-ca" | "fr-ch" | "hu" | "is" | "it" | "ja" | "lt" | "mk" | "nl" | "no" | "pl" | "pt" | "pt-br" | "sv" | "sl" | "tr";
  // Enable/disable KVM hardware virtualization.
  "kvm"?: boolean;
  // Set the real time clock (RTC) to local time. This is enabled by default if the `ostype` indicates a Microsoft Windows OS.
  "localtime"?: boolean;
  // Lock/unlock the VM.
  "lock"?: "backup" | "clone" | "create" | "migrate" | "rollback" | "snapshot" | "snapshot-delete" | "suspending" | "suspended";
  // Specify the QEMU machine.
  "machine"?: string;
  // Memory properties.
  "memory"?: string;
  // Set maximum tolerated downtime (in seconds) for migrations. Should the migration not be able to converge in the very end, because too much newly dirtied RAM needs to be transferred, the limit will be increased automatically step-by-step until migration can converge.
  "migrate_downtime"?: number;
  // Set maximum speed (in MB/s) for migrations. Value 0 is no limit.
  "migrate_speed"?: number;
  // Set a name for the VM. Only used on the configuration web interface.
  "name"?: string;
  // cloud-init: Sets DNS server IP address for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "nameserver"?: string;
  // Specify network devices.
  "net[n]"?: string;
  // The cluster node name.
  "node": string;
  // Enable/disable NUMA.
  "numa"?: boolean;
  // NUMA topology.
  "numa[n]"?: string;
  // Specifies whether a VM will be started during system bootup.
  "onboot"?: boolean;
  // Specify guest operating system.
  "ostype"?: "other" | "wxp" | "w2k" | "w2k3" | "w2k8" | "wvista" | "win7" | "win8" | "win10" | "win11" | "l24" | "l26" | "solaris";
  // Map host parallel devices (n is 0 to 2).
  "parallel[n]"?: string;
  // Sets the protection flag of the VM. This will disable the remove VM and remove disk operations.
  "protection"?: boolean;
  // Allow reboot. If set to '0' the VM exit on reboot.
  "reboot"?: boolean;
  // Revert a pending change.
  "revert"?: string;
  // Configure a VirtIO-based Random Number Generator.
  "rng0"?: string;
  // Use volume as SATA hard disk or CD-ROM (n is 0 to 5). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "sata[n]"?: string;
  // Use volume as SCSI hard disk or CD-ROM (n is 0 to 30). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "scsi[n]"?: string;
  // SCSI controller model
  "scsihw"?: "lsi" | "lsi53c810" | "virtio-scsi-pci" | "virtio-scsi-single" | "megasas" | "pvscsi";
  // cloud-init: Sets DNS search domains for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "searchdomain"?: string;
  // Create a serial device inside the VM (n is 0 to 3)
  "serial[n]"?: string;
  // Amount of memory shares for auto-ballooning. The larger the number is, the more memory this VM gets. Number is relative to weights of all other running VMs. Using zero disables auto-ballooning. Auto-ballooning is done by pvestatd.
  "shares"?: number;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // Specify SMBIOS type 1 fields.
  "smbios1"?: string;
  // The number of CPUs. Please use option -sockets instead.
  "smp"?: number;
  // The number of CPU sockets.
  "sockets"?: number;
  // Configure additional enhancements for SPICE.
  "spice_enhancements"?: string;
  // cloud-init: Setup public SSH keys (one key per line, OpenSSH format).
  "sshkeys"?: string;
  // Set the initial date of the real time clock. Valid format for date are:'now' or '2006-06-17T16:01:21' or '2006-06-17'.
  "startdate"?: string;
  // Startup and shutdown behavior. Order is a non-negative number defining the general startup order. Shutdown in done with reverse ordering. Additionally you can set the 'up' or 'down' delay in seconds, which specifies a delay to wait before the next VM is started or stopped.
  "startup"?: string;
  // Enable/disable the USB tablet device.
  "tablet"?: boolean;
  // Tags of the VM. This is only meta information.
  "tags"?: string;
  // Enable/disable time drift fix.
  "tdf"?: boolean;
  // Enable/disable Template.
  "template"?: boolean;
  // Configure a Disk for storing TPM state. The format is fixed to 'raw'. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and 4 MiB will be used instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "tpmstate0"?: string;
  // Reference to unused volumes. This is used internally, and should not be modified manually.
  "unused[n]"?: string;
  // Configure an USB device (n is 0 to 4, for machine version >= 7.1 and ostype l26 or windows > 7, n can be up to 14).
  "usb[n]"?: string;
  // Number of hotplugged vcpus.
  "vcpus"?: number;
  // Configure the VGA hardware.
  "vga"?: string;
  // Use volume as VIRTIO hard disk (n is 0 to 15). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "virtio[n]"?: string;
  // Configuration for sharing a directory between host and guest using Virtio-fs.
  "virtiofs[n]"?: string;
  // Set VM Generation ID. Use '1' to autogenerate on create or update, pass '0' to disable explicitly.
  "vmgenid"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Default storage for VM state volumes/files.
  "vmstatestorage"?: string;
  // Create a virtual hardware watchdog device.
  "watchdog"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/config

Set virtual machine options (synchronous API) - You should consider using the POST method instead for any actions involving hotplug or storage allocation.

### Input Parameters

```ts
interface Params {
  // Enable/disable ACPI.
  "acpi"?: boolean;
  // List of host cores used to execute guest processes, for example: 0,5,8-11
  "affinity"?: string;
  // Enable/disable communication with the QEMU Guest Agent and its properties.
  "agent"?: string;
  // Secure Encrypted Virtualization (SEV) features by AMD CPUs
  "amd-sev"?: string;
  // Virtual processor architecture. Defaults to the host.
  "arch"?: "x86_64" | "aarch64";
  // Arbitrary arguments passed to kvm.
  "args"?: string;
  // Configure a audio device, useful in combination with QXL/Spice.
  "audio0"?: string;
  // Automatic restart after crash (currently ignored).
  "autostart"?: boolean;
  // Amount of target RAM for the VM in MiB. Using zero disables the ballon driver.
  "balloon"?: number;
  // Select BIOS implementation.
  "bios"?: "seabios" | "ovmf";
  // Specify guest boot order. Use the 'order=' sub-property as usage with no key or 'legacy=' is deprecated.
  "boot"?: string;
  // Enable booting from specified disk. Deprecated: Use 'boot: order=foo;bar' instead.
  "bootdisk"?: string;
  // This is an alias for option -ide2
  "cdrom"?: string;
  // cloud-init: Specify custom files to replace the automatically generated ones at start.
  "cicustom"?: string;
  // cloud-init: Password to assign the user. Using this is generally not recommended. Use ssh keys instead. Also note that older cloud-init versions do not support hashed passwords.
  "cipassword"?: string;
  // Specifies the cloud-init configuration format. The default depends on the configured operating system type (`ostype`. We use the `nocloud` format for Linux, and `configdrive2` for windows.
  "citype"?: "configdrive2" | "nocloud" | "opennebula";
  // cloud-init: do an automatic package upgrade after the first boot.
  "ciupgrade"?: boolean;
  // cloud-init: User name to change ssh keys and password for instead of the image's configured default user.
  "ciuser"?: string;
  // The number of cores per socket.
  "cores"?: number;
  // Emulated CPU type.
  "cpu"?: string;
  // Limit of CPU usage.
  "cpulimit"?: number;
  // CPU weight for a VM, will be clamped to [1, 10000] in cgroup v2.
  "cpuunits"?: number;
  // A list of settings you want to delete.
  "delete"?: string;
  // Description for the VM. Shown in the web-interface VM's summary. This is saved as comment inside the configuration file.
  "description"?: string;
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Configure a disk for storing EFI vars. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and that the default EFI vars are copied to the volume instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "efidisk0"?: string;
  // Force physical removal. Without this, we simple remove the disk from the config file and create an additional configuration entry called 'unused[n]', which contains the volume ID. Unlink of unused[n] always cause physical removal.
  "force"?: boolean;
  // Freeze CPU at startup (use 'c' monitor command to start execution).
  "freeze"?: boolean;
  // Script that will be executed during various steps in the vms lifetime.
  "hookscript"?: string;
  // Map host PCI devices into guest.
  "hostpci[n]"?: string;
  // Selectively enable hotplug features. This is a comma separated list of hotplug features: 'network', 'disk', 'cpu', 'memory', 'usb' and 'cloudinit'. Use '0' to disable hotplug completely. Using '1' as value is an alias for the default `network,disk,usb`. USB hotplugging is possible for guests with machine version >= 7.1 and ostype l26 or windows > 7.
  "hotplug"?: string;
  // Enable/disable hugepages memory.
  "hugepages"?: "any" | "2" | "1024";
  // Use volume as IDE hard disk or CD-ROM (n is 0 to 3). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "ide[n]"?: string;
  // cloud-init: Specify IP addresses and gateways for the corresponding interface.  IP addresses use CIDR notation, gateways are optional but need an IP of the same type specified.  The special string 'dhcp' can be used for IP addresses to use DHCP, in which case no explicit gateway should be provided. For IPv6 the special string 'auto' can be used to use stateless autoconfiguration. This requires cloud-init 19.4 or newer.  If cloud-init is enabled and neither an IPv4 nor an IPv6 address is specified, it defaults to using dhcp on IPv4. 
  "ipconfig[n]"?: string;
  // Inter-VM shared memory. Useful for direct communication between VMs, or to the host.
  "ivshmem"?: string;
  // Use together with hugepages. If enabled, hugepages will not not be deleted after VM shutdown and can be used for subsequent starts.
  "keephugepages"?: boolean;
  // Keyboard layout for VNC server. This option is generally not required and is often better handled from within the guest OS.
  "keyboard"?: "de" | "de-ch" | "da" | "en-gb" | "en-us" | "es" | "fi" | "fr" | "fr-be" | "fr-ca" | "fr-ch" | "hu" | "is" | "it" | "ja" | "lt" | "mk" | "nl" | "no" | "pl" | "pt" | "pt-br" | "sv" | "sl" | "tr";
  // Enable/disable KVM hardware virtualization.
  "kvm"?: boolean;
  // Set the real time clock (RTC) to local time. This is enabled by default if the `ostype` indicates a Microsoft Windows OS.
  "localtime"?: boolean;
  // Lock/unlock the VM.
  "lock"?: "backup" | "clone" | "create" | "migrate" | "rollback" | "snapshot" | "snapshot-delete" | "suspending" | "suspended";
  // Specify the QEMU machine.
  "machine"?: string;
  // Memory properties.
  "memory"?: string;
  // Set maximum tolerated downtime (in seconds) for migrations. Should the migration not be able to converge in the very end, because too much newly dirtied RAM needs to be transferred, the limit will be increased automatically step-by-step until migration can converge.
  "migrate_downtime"?: number;
  // Set maximum speed (in MB/s) for migrations. Value 0 is no limit.
  "migrate_speed"?: number;
  // Set a name for the VM. Only used on the configuration web interface.
  "name"?: string;
  // cloud-init: Sets DNS server IP address for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "nameserver"?: string;
  // Specify network devices.
  "net[n]"?: string;
  // The cluster node name.
  "node": string;
  // Enable/disable NUMA.
  "numa"?: boolean;
  // NUMA topology.
  "numa[n]"?: string;
  // Specifies whether a VM will be started during system bootup.
  "onboot"?: boolean;
  // Specify guest operating system.
  "ostype"?: "other" | "wxp" | "w2k" | "w2k3" | "w2k8" | "wvista" | "win7" | "win8" | "win10" | "win11" | "l24" | "l26" | "solaris";
  // Map host parallel devices (n is 0 to 2).
  "parallel[n]"?: string;
  // Sets the protection flag of the VM. This will disable the remove VM and remove disk operations.
  "protection"?: boolean;
  // Allow reboot. If set to '0' the VM exit on reboot.
  "reboot"?: boolean;
  // Revert a pending change.
  "revert"?: string;
  // Configure a VirtIO-based Random Number Generator.
  "rng0"?: string;
  // Use volume as SATA hard disk or CD-ROM (n is 0 to 5). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "sata[n]"?: string;
  // Use volume as SCSI hard disk or CD-ROM (n is 0 to 30). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "scsi[n]"?: string;
  // SCSI controller model
  "scsihw"?: "lsi" | "lsi53c810" | "virtio-scsi-pci" | "virtio-scsi-single" | "megasas" | "pvscsi";
  // cloud-init: Sets DNS search domains for a container. Create will automatically use the setting from the host if neither searchdomain nor nameserver are set.
  "searchdomain"?: string;
  // Create a serial device inside the VM (n is 0 to 3)
  "serial[n]"?: string;
  // Amount of memory shares for auto-ballooning. The larger the number is, the more memory this VM gets. Number is relative to weights of all other running VMs. Using zero disables auto-ballooning. Auto-ballooning is done by pvestatd.
  "shares"?: number;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // Specify SMBIOS type 1 fields.
  "smbios1"?: string;
  // The number of CPUs. Please use option -sockets instead.
  "smp"?: number;
  // The number of CPU sockets.
  "sockets"?: number;
  // Configure additional enhancements for SPICE.
  "spice_enhancements"?: string;
  // cloud-init: Setup public SSH keys (one key per line, OpenSSH format).
  "sshkeys"?: string;
  // Set the initial date of the real time clock. Valid format for date are:'now' or '2006-06-17T16:01:21' or '2006-06-17'.
  "startdate"?: string;
  // Startup and shutdown behavior. Order is a non-negative number defining the general startup order. Shutdown in done with reverse ordering. Additionally you can set the 'up' or 'down' delay in seconds, which specifies a delay to wait before the next VM is started or stopped.
  "startup"?: string;
  // Enable/disable the USB tablet device.
  "tablet"?: boolean;
  // Tags of the VM. This is only meta information.
  "tags"?: string;
  // Enable/disable time drift fix.
  "tdf"?: boolean;
  // Enable/disable Template.
  "template"?: boolean;
  // Configure a Disk for storing TPM state. The format is fixed to 'raw'. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Note that SIZE_IN_GiB is ignored here and 4 MiB will be used instead. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "tpmstate0"?: string;
  // Reference to unused volumes. This is used internally, and should not be modified manually.
  "unused[n]"?: string;
  // Configure an USB device (n is 0 to 4, for machine version >= 7.1 and ostype l26 or windows > 7, n can be up to 14).
  "usb[n]"?: string;
  // Number of hotplugged vcpus.
  "vcpus"?: number;
  // Configure the VGA hardware.
  "vga"?: string;
  // Use volume as VIRTIO hard disk (n is 0 to 15). Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume. Use STORAGE_ID:0 and the 'import-from' parameter to import from an existing volume.
  "virtio[n]"?: string;
  // Configuration for sharing a directory between host and guest using Virtio-fs.
  "virtiofs[n]"?: string;
  // Set VM Generation ID. Use '1' to autogenerate on create or update, pass '0' to disable explicitly.
  "vmgenid"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Default storage for VM state volumes/files.
  "vmstatestorage"?: string;
  // Create a virtual hardware watchdog device.
  "watchdog"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/pending

Get the virtual machine configuration with both current and pending values.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Indicates a pending delete request if present and not 0. The value 2 indicates a force-delete request.
  delete?: number;
  // Configuration option name.
  key: string;
  // Pending value.
  pending?: string;
  // Current value.
  value?: string;
}[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/cloudinit

Get the cloudinit configuration with both current and pending values.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Indicates a pending delete request if present and not 0. 
  delete?: number;
  // Configuration option name.
  key: string;
  // The new pending value.
  pending?: string;
  // Value as it was used to generate the current cloudinit image.
  value?: string;
}[];
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/cloudinit

Regenerate and change cloudinit config drive.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/cloudinit/dump

Get automatically generated cloudinit config.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Config type.
  "type": "user" | "network" | "meta";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/unlink

Unlink/delete disk images.

### Input Parameters

```ts
interface Params {
  // Force physical removal. Without this, we simple remove the disk from the config file and create an additional configuration entry called 'unused[n]', which contains the volume ID. Unlink of unused[n] always cause physical removal.
  "force"?: boolean;
  // A list of disk IDs you want to delete.
  "idlist": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/vncproxy

Creates a TCP VNC proxy connections.

### Input Parameters

```ts
interface Params {
  // Generates a random password to be used as ticket instead of the API ticket.
  "generate-password"?: boolean;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Prepare for websocket upgrade (only required when using serial terminal, otherwise upgrade is always possible).
  "websocket"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/termproxy

Creates a TCP proxy connections.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // opens a serial terminal (defaults to display)
  "serial"?: "serial0" | "serial1" | "serial2" | "serial3";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/vncwebsocket

Opens a weksocket for VNC traffic.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Port number returned by previous vncproxy call.
  "port": number;
  // The (unique) ID of the VM.
  "vmid": number;
  // Ticket from previous call to vncproxy.
  "vncticket": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/spiceproxy

Returns a SPICE configuration to connect to the VM.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // SPICE proxy server. This can be used by the client to specify the proxy server. All nodes in a cluster runs 'spiceproxy', so it is up to the client to choose one. By default, we return the node where the VM is currently running. As reasonable setting is to use same node you use to connect to the API (This is window.location.hostname for the JS GUI).
  "proxy"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/status

Directory index

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/status/current

Get virtual machine status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/start

Start virtual machine.

### Input Parameters

```ts
interface Params {
  // Override QEMU's -cpu argument with the given string.
  "force-cpu"?: string;
  // Specify the QEMU machine.
  "machine"?: string;
  // The cluster node name.
  "migratedfrom"?: string;
  // CIDR of the (sub) network that is used for migration.
  "migration_network"?: string;
  // Migration traffic is encrypted using an SSH tunnel by default. On secure, completely private networks this can be disabled to increase performance.
  "migration_type"?: "secure" | "insecure";
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // Some command save/restore state from this location.
  "stateuri"?: string;
  // Mapping from source to target storages. Providing only a single storage ID maps all source storages to that storage. Providing the special value '1' will map each source storage to itself.
  "targetstorage"?: string;
  // Wait maximal timeout seconds.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/stop

Stop virtual machine. The qemu process will exit immediately. This is akin to pulling the power plug of a running computer and may damage the VM data.

### Input Parameters

```ts
interface Params {
  // Do not deactivate storage volumes.
  "keepActive"?: boolean;
  // The cluster node name.
  "migratedfrom"?: string;
  // The cluster node name.
  "node": string;
  // Try to abort active 'qmshutdown' tasks before stopping.
  "overrule-shutdown"?: boolean;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // Wait maximal timeout seconds.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/reset

Reset virtual machine.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/shutdown

Shutdown virtual machine. This is similar to pressing the power button on a physical machine. This will send an ACPI event for the guest OS, which should then proceed to a clean shutdown.

### Input Parameters

```ts
interface Params {
  // Make sure the VM stops.
  "forceStop"?: boolean;
  // Do not deactivate storage volumes.
  "keepActive"?: boolean;
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // Wait maximal timeout seconds.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/reboot

Reboot the VM by shutting it down, and starting it again. Applies pending changes.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Wait maximal timeout seconds for the shutdown.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/suspend

Suspend virtual machine.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The storage for the VM state
  "statestorage"?: string;
  // If set, suspends the VM to disk. Will be resumed on next VM start.
  "todisk"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/status/resume

Resume virtual machine.

### Input Parameters

```ts
interface Params {
  "nocheck"?: boolean;
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/sendkey

Send key event to virtual machine.

### Input Parameters

```ts
interface Params {
  // The key (qemu monitor encoding).
  "key": string;
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/feature

Check if feature for virtual machine is available.

### Input Parameters

```ts
interface Params {
  // Feature to check.
  "feature": "snapshot" | "clone" | "copy";
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/clone

Create a copy of virtual machine/template.

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Description for the new VM.
  "description"?: string;
  // Target format for file storage. Only valid for full clone.
  "format"?: "raw" | "qcow2" | "vmdk";
  // Create a full copy of all disks. This is always done when you clone a normal VM. For VM templates, we try to create a linked clone by default.
  "full"?: boolean;
  // Set a name for the new VM.
  "name"?: string;
  // VMID for the clone.
  "newid": number;
  // The cluster node name.
  "node": string;
  // Add the new VM to the specified pool.
  "pool"?: string;
  // The name of the snapshot.
  "snapname"?: string;
  // Target storage for full clone.
  "storage"?: string;
  // Target node. Only allowed if the original VM is on shared storage.
  "target"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/move_disk

Move volume to different storage or to a different VM.

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Delete the original disk after successful copy. By default the original disk is kept as unused disk.
  "delete"?: boolean;
  // Prevent changes if current configuration file has different SHA1" 		    ." digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The disk you want to move.
  "disk": "ide0" | "ide1" | "ide2" | "ide3" | "scsi0" | "scsi1" | "scsi2" | "scsi3" | "scsi4" | "scsi5" | "scsi6" | "scsi7" | "scsi8" | "scsi9" | "scsi10" | "scsi11" | "scsi12" | "scsi13" | "scsi14" | "scsi15" | "scsi16" | "scsi17" | "scsi18" | "scsi19" | "scsi20" | "scsi21" | "scsi22" | "scsi23" | "scsi24" | "scsi25" | "scsi26" | "scsi27" | "scsi28" | "scsi29" | "scsi30" | "virtio0" | "virtio1" | "virtio2" | "virtio3" | "virtio4" | "virtio5" | "virtio6" | "virtio7" | "virtio8" | "virtio9" | "virtio10" | "virtio11" | "virtio12" | "virtio13" | "virtio14" | "virtio15" | "sata0" | "sata1" | "sata2" | "sata3" | "sata4" | "sata5" | "efidisk0" | "tpmstate0" | "unused0" | "unused1" | "unused2" | "unused3" | "unused4" | "unused5" | "unused6" | "unused7" | "unused8" | "unused9" | "unused10" | "unused11" | "unused12" | "unused13" | "unused14" | "unused15" | "unused16" | "unused17" | "unused18" | "unused19" | "unused20" | "unused21" | "unused22" | "unused23" | "unused24" | "unused25" | "unused26" | "unused27" | "unused28" | "unused29" | "unused30" | "unused31" | "unused32" | "unused33" | "unused34" | "unused35" | "unused36" | "unused37" | "unused38" | "unused39" | "unused40" | "unused41" | "unused42" | "unused43" | "unused44" | "unused45" | "unused46" | "unused47" | "unused48" | "unused49" | "unused50" | "unused51" | "unused52" | "unused53" | "unused54" | "unused55" | "unused56" | "unused57" | "unused58" | "unused59" | "unused60" | "unused61" | "unused62" | "unused63" | "unused64" | "unused65" | "unused66" | "unused67" | "unused68" | "unused69" | "unused70" | "unused71" | "unused72" | "unused73" | "unused74" | "unused75" | "unused76" | "unused77" | "unused78" | "unused79" | "unused80" | "unused81" | "unused82" | "unused83" | "unused84" | "unused85" | "unused86" | "unused87" | "unused88" | "unused89" | "unused90" | "unused91" | "unused92" | "unused93" | "unused94" | "unused95" | "unused96" | "unused97" | "unused98" | "unused99" | "unused100" | "unused101" | "unused102" | "unused103" | "unused104" | "unused105" | "unused106" | "unused107" | "unused108" | "unused109" | "unused110" | "unused111" | "unused112" | "unused113" | "unused114" | "unused115" | "unused116" | "unused117" | "unused118" | "unused119" | "unused120" | "unused121" | "unused122" | "unused123" | "unused124" | "unused125" | "unused126" | "unused127" | "unused128" | "unused129" | "unused130" | "unused131" | "unused132" | "unused133" | "unused134" | "unused135" | "unused136" | "unused137" | "unused138" | "unused139" | "unused140" | "unused141" | "unused142" | "unused143" | "unused144" | "unused145" | "unused146" | "unused147" | "unused148" | "unused149" | "unused150" | "unused151" | "unused152" | "unused153" | "unused154" | "unused155" | "unused156" | "unused157" | "unused158" | "unused159" | "unused160" | "unused161" | "unused162" | "unused163" | "unused164" | "unused165" | "unused166" | "unused167" | "unused168" | "unused169" | "unused170" | "unused171" | "unused172" | "unused173" | "unused174" | "unused175" | "unused176" | "unused177" | "unused178" | "unused179" | "unused180" | "unused181" | "unused182" | "unused183" | "unused184" | "unused185" | "unused186" | "unused187" | "unused188" | "unused189" | "unused190" | "unused191" | "unused192" | "unused193" | "unused194" | "unused195" | "unused196" | "unused197" | "unused198" | "unused199" | "unused200" | "unused201" | "unused202" | "unused203" | "unused204" | "unused205" | "unused206" | "unused207" | "unused208" | "unused209" | "unused210" | "unused211" | "unused212" | "unused213" | "unused214" | "unused215" | "unused216" | "unused217" | "unused218" | "unused219" | "unused220" | "unused221" | "unused222" | "unused223" | "unused224" | "unused225" | "unused226" | "unused227" | "unused228" | "unused229" | "unused230" | "unused231" | "unused232" | "unused233" | "unused234" | "unused235" | "unused236" | "unused237" | "unused238" | "unused239" | "unused240" | "unused241" | "unused242" | "unused243" | "unused244" | "unused245" | "unused246" | "unused247" | "unused248" | "unused249" | "unused250" | "unused251" | "unused252" | "unused253" | "unused254" | "unused255";
  // Target Format.
  "format"?: "raw" | "qcow2" | "vmdk";
  // The cluster node name.
  "node": string;
  // Target storage.
  "storage"?: string;
  // Prevent changes if the current config file of the target VM has a" 		    ." different SHA1 digest. This can be used to detect concurrent modifications.
  "target-digest"?: string;
  // The config key the disk will be moved to on the target VM (for example, ide0 or scsi1). Default is the source disk key.
  "target-disk"?: "ide0" | "ide1" | "ide2" | "ide3" | "scsi0" | "scsi1" | "scsi2" | "scsi3" | "scsi4" | "scsi5" | "scsi6" | "scsi7" | "scsi8" | "scsi9" | "scsi10" | "scsi11" | "scsi12" | "scsi13" | "scsi14" | "scsi15" | "scsi16" | "scsi17" | "scsi18" | "scsi19" | "scsi20" | "scsi21" | "scsi22" | "scsi23" | "scsi24" | "scsi25" | "scsi26" | "scsi27" | "scsi28" | "scsi29" | "scsi30" | "virtio0" | "virtio1" | "virtio2" | "virtio3" | "virtio4" | "virtio5" | "virtio6" | "virtio7" | "virtio8" | "virtio9" | "virtio10" | "virtio11" | "virtio12" | "virtio13" | "virtio14" | "virtio15" | "sata0" | "sata1" | "sata2" | "sata3" | "sata4" | "sata5" | "efidisk0" | "tpmstate0" | "unused0" | "unused1" | "unused2" | "unused3" | "unused4" | "unused5" | "unused6" | "unused7" | "unused8" | "unused9" | "unused10" | "unused11" | "unused12" | "unused13" | "unused14" | "unused15" | "unused16" | "unused17" | "unused18" | "unused19" | "unused20" | "unused21" | "unused22" | "unused23" | "unused24" | "unused25" | "unused26" | "unused27" | "unused28" | "unused29" | "unused30" | "unused31" | "unused32" | "unused33" | "unused34" | "unused35" | "unused36" | "unused37" | "unused38" | "unused39" | "unused40" | "unused41" | "unused42" | "unused43" | "unused44" | "unused45" | "unused46" | "unused47" | "unused48" | "unused49" | "unused50" | "unused51" | "unused52" | "unused53" | "unused54" | "unused55" | "unused56" | "unused57" | "unused58" | "unused59" | "unused60" | "unused61" | "unused62" | "unused63" | "unused64" | "unused65" | "unused66" | "unused67" | "unused68" | "unused69" | "unused70" | "unused71" | "unused72" | "unused73" | "unused74" | "unused75" | "unused76" | "unused77" | "unused78" | "unused79" | "unused80" | "unused81" | "unused82" | "unused83" | "unused84" | "unused85" | "unused86" | "unused87" | "unused88" | "unused89" | "unused90" | "unused91" | "unused92" | "unused93" | "unused94" | "unused95" | "unused96" | "unused97" | "unused98" | "unused99" | "unused100" | "unused101" | "unused102" | "unused103" | "unused104" | "unused105" | "unused106" | "unused107" | "unused108" | "unused109" | "unused110" | "unused111" | "unused112" | "unused113" | "unused114" | "unused115" | "unused116" | "unused117" | "unused118" | "unused119" | "unused120" | "unused121" | "unused122" | "unused123" | "unused124" | "unused125" | "unused126" | "unused127" | "unused128" | "unused129" | "unused130" | "unused131" | "unused132" | "unused133" | "unused134" | "unused135" | "unused136" | "unused137" | "unused138" | "unused139" | "unused140" | "unused141" | "unused142" | "unused143" | "unused144" | "unused145" | "unused146" | "unused147" | "unused148" | "unused149" | "unused150" | "unused151" | "unused152" | "unused153" | "unused154" | "unused155" | "unused156" | "unused157" | "unused158" | "unused159" | "unused160" | "unused161" | "unused162" | "unused163" | "unused164" | "unused165" | "unused166" | "unused167" | "unused168" | "unused169" | "unused170" | "unused171" | "unused172" | "unused173" | "unused174" | "unused175" | "unused176" | "unused177" | "unused178" | "unused179" | "unused180" | "unused181" | "unused182" | "unused183" | "unused184" | "unused185" | "unused186" | "unused187" | "unused188" | "unused189" | "unused190" | "unused191" | "unused192" | "unused193" | "unused194" | "unused195" | "unused196" | "unused197" | "unused198" | "unused199" | "unused200" | "unused201" | "unused202" | "unused203" | "unused204" | "unused205" | "unused206" | "unused207" | "unused208" | "unused209" | "unused210" | "unused211" | "unused212" | "unused213" | "unused214" | "unused215" | "unused216" | "unused217" | "unused218" | "unused219" | "unused220" | "unused221" | "unused222" | "unused223" | "unused224" | "unused225" | "unused226" | "unused227" | "unused228" | "unused229" | "unused230" | "unused231" | "unused232" | "unused233" | "unused234" | "unused235" | "unused236" | "unused237" | "unused238" | "unused239" | "unused240" | "unused241" | "unused242" | "unused243" | "unused244" | "unused245" | "unused246" | "unused247" | "unused248" | "unused249" | "unused250" | "unused251" | "unused252" | "unused253" | "unused254" | "unused255";
  // The (unique) ID of the VM.
  "target-vmid"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/migrate

Get preconditions for migration.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Target node.
  "target"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/migrate

Migrate virtual machine. Creates a new migration task.

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Allow to migrate VMs which use local devices. Only root may use this option.
  "force"?: boolean;
  // CIDR of the (sub) network that is used for migration.
  "migration_network"?: string;
  // Migration traffic is encrypted using an SSH tunnel by default. On secure, completely private networks this can be disabled to increase performance.
  "migration_type"?: "secure" | "insecure";
  // The cluster node name.
  "node": string;
  // Use online/live migration if VM is running. Ignored if VM is stopped.
  "online"?: boolean;
  // Target node.
  "target": string;
  // Mapping from source to target storages. Providing only a single storage ID maps all source storages to that storage. Providing the special value '1' will map each source storage to itself.
  "targetstorage"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Enable live storage migration for local disk
  "with-local-disks"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/remote_migrate

Migrate virtual machine to a remote cluster. Creates a new migration task. EXPERIMENTAL feature!

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Delete the original VM and related data after successful migration. By default the original VM is kept on the source cluster in a stopped state.
  "delete"?: boolean;
  // The cluster node name.
  "node": string;
  // Use online/live migration if VM is running. Ignored if VM is stopped.
  "online"?: boolean;
  // Mapping from source to target bridges. Providing only a single bridge ID maps all source bridges to that bridge. Providing the special value '1' will map each source bridge to itself.
  "target-bridge": string;
  // Remote target endpoint
  "target-endpoint": string;
  // Mapping from source to target storages. Providing only a single storage ID maps all source storages to that storage. Providing the special value '1' will map each source storage to itself.
  "target-storage": string;
  // The (unique) ID of the VM.
  "target-vmid"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/monitor

Execute QEMU monitor commands.

### Input Parameters

```ts
interface Params {
  // The monitor command.
  "command": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/resize

Extend volume size.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The disk you want to resize.
  "disk": "ide0" | "ide1" | "ide2" | "ide3" | "scsi0" | "scsi1" | "scsi2" | "scsi3" | "scsi4" | "scsi5" | "scsi6" | "scsi7" | "scsi8" | "scsi9" | "scsi10" | "scsi11" | "scsi12" | "scsi13" | "scsi14" | "scsi15" | "scsi16" | "scsi17" | "scsi18" | "scsi19" | "scsi20" | "scsi21" | "scsi22" | "scsi23" | "scsi24" | "scsi25" | "scsi26" | "scsi27" | "scsi28" | "scsi29" | "scsi30" | "virtio0" | "virtio1" | "virtio2" | "virtio3" | "virtio4" | "virtio5" | "virtio6" | "virtio7" | "virtio8" | "virtio9" | "virtio10" | "virtio11" | "virtio12" | "virtio13" | "virtio14" | "virtio15" | "sata0" | "sata1" | "sata2" | "sata3" | "sata4" | "sata5" | "efidisk0" | "tpmstate0";
  // The cluster node name.
  "node": string;
  // The new size. With the `+` sign the value is added to the actual size of the volume and without it, the value is taken as an absolute one. Shrinking disk size is not supported.
  "size": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/snapshot

List all snapshots.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Snapshot description.
  description: string;
  // Snapshot identifier. Value 'current' identifies the current VM.
  name: string;
  // Parent snapshot identifier.
  parent?: string;
  // Snapshot creation time
  snaptime?: number;
  // Snapshot includes RAM.
  vmstate?: boolean;
}[];
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/snapshot

Snapshot a VM.

### Input Parameters

```ts
interface Params {
  // A textual description or comment.
  "description"?: string;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
  // Save the vmstate
  "vmstate"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/qemu/{vmid}/snapshot/{snapname}

Delete a VM snapshot.

### Input Parameters

```ts
interface Params {
  // For removal from config file, even if removing disk snapshots fails.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/snapshot/{snapname}

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/snapshot/{snapname}/config

Get snapshot configuration

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/qemu/{vmid}/snapshot/{snapname}/config

Update snapshot metadata.

### Input Parameters

```ts
interface Params {
  // A textual description or comment.
  "description"?: string;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/snapshot/{snapname}/rollback

Rollback VM state to specified snapshot.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // Whether the VM should get started after rolling back successfully. (Note: VMs will be automatically started if the snapshot includes RAM.)
  "start"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/template

Create a Template.

### Input Parameters

```ts
interface Params {
  // If you want to convert only 1 disk to base image.
  "disk"?: "ide0" | "ide1" | "ide2" | "ide3" | "scsi0" | "scsi1" | "scsi2" | "scsi3" | "scsi4" | "scsi5" | "scsi6" | "scsi7" | "scsi8" | "scsi9" | "scsi10" | "scsi11" | "scsi12" | "scsi13" | "scsi14" | "scsi15" | "scsi16" | "scsi17" | "scsi18" | "scsi19" | "scsi20" | "scsi21" | "scsi22" | "scsi23" | "scsi24" | "scsi25" | "scsi26" | "scsi27" | "scsi28" | "scsi29" | "scsi30" | "virtio0" | "virtio1" | "virtio2" | "virtio3" | "virtio4" | "virtio5" | "virtio6" | "virtio7" | "virtio8" | "virtio9" | "virtio10" | "virtio11" | "virtio12" | "virtio13" | "virtio14" | "virtio15" | "sata0" | "sata1" | "sata2" | "sata3" | "sata4" | "sata5" | "efidisk0" | "tpmstate0";
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/qemu/{vmid}/mtunnel

Migration tunnel endpoint - only for internal use by VM migration.

### Input Parameters

```ts
interface Params {
  // List of network bridges to check availability. Will be checked again for actually used bridges during migration.
  "bridges"?: string;
  // The cluster node name.
  "node": string;
  // List of storages to check permission and availability. Will be checked again for all actually used storages during migration.
  "storages"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/qemu/{vmid}/mtunnelwebsocket

Migration tunnel endpoint for websocket upgrade - only for internal use by VM migration.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // unix socket to forward to
  "socket": string;
  // ticket return by initial 'mtunnel' API call, or retrieved via 'ticket' tunnel command
  "ticket": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc

LXC container index (per node).

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // Current CPU usage.
  cpu?: number;
  // Maximum usable CPUs.
  cpus?: number;
  // Root disk image space-usage in bytes.
  disk?: number;
  // The amount of bytes the guest read from it's block devices since the guest was started. (Note: This info is not available for all storage types.)
  diskread?: number;
  // The amount of bytes the guest wrote from it's block devices since the guest was started. (Note: This info is not available for all storage types.)
  diskwrite?: number;
  // The current config lock, if any.
  lock?: string;
  // Root disk image size in bytes.
  maxdisk?: number;
  // Maximum memory in bytes.
  maxmem?: number;
  // Maximum SWAP memory in bytes.
  maxswap?: number;
  // Currently used memory in bytes.
  mem?: number;
  // Container name.
  name?: string;
  // The amount of traffic in bytes that was sent to the guest over the network since it was started.
  netin?: number;
  // The amount of traffic in bytes that was sent from the guest over the network since it was started.
  netout?: number;
  // LXC Container status.
  status: "stopped" | "running";
  // The current configured tags, if any.
  tags?: string;
  // Determines if the guest is a template.
  template?: boolean;
  // Uptime in seconds.
  uptime?: number;
  // The (unique) ID of the VM.
  vmid: number;
}[];
```

## POST /api2/json/nodes/{node}/lxc

Create or restore a container.

### Input Parameters

```ts
interface Params {
  // OS architecture type.
  "arch"?: "amd64" | "i386" | "arm64" | "armhf" | "riscv32" | "riscv64";
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Console mode. By default, the console command tries to open a connection to one of the available tty devices. By setting cmode to 'console' it tries to attach to /dev/console instead. If you set cmode to 'shell', it simply invokes a shell inside the container (no login).
  "cmode"?: "shell" | "console" | "tty";
  // Attach a console device (/dev/console) to the container.
  "console"?: boolean;
  // The number of cores assigned to the container. A container can use all available cores by default.
  "cores"?: number;
  // Limit of CPU usage.  NOTE: If the computer has 2 CPUs, it has a total of '2' CPU time. Value '0' indicates no CPU limit.
  "cpulimit"?: number;
  // CPU weight for a container, will be clamped to [1, 10000] in cgroup v2.
  "cpuunits"?: number;
  // Try to be more verbose. For now this only enables debug log-level on start.
  "debug"?: boolean;
  // Description for the Container. Shown in the web-interface CT's summary. This is saved as comment inside the configuration file.
  "description"?: string;
  // Device to pass through to the container
  "dev[n]"?: string;
  // Allow containers access to advanced features.
  "features"?: string;
  // Allow to overwrite existing container.
  "force"?: boolean;
  // Script that will be executed during various steps in the containers lifetime.
  "hookscript"?: string;
  // Set a host name for the container.
  "hostname"?: string;
  // Ignore errors when extracting the template.
  "ignore-unpack-errors"?: boolean;
  // Lock/unlock the container.
  "lock"?: "backup" | "create" | "destroyed" | "disk" | "fstrim" | "migrate" | "mounted" | "rollback" | "snapshot" | "snapshot-delete";
  // Amount of RAM for the container in MB.
  "memory"?: number;
  // Use volume as container mount point. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume.
  "mp[n]"?: string;
  // Sets DNS server IP address for a container. Create will automatically use the setting from the host if you neither set searchdomain nor nameserver.
  "nameserver"?: string;
  // Specifies network interfaces for the container.
  "net[n]"?: string;
  // The cluster node name.
  "node": string;
  // Specifies whether a container will be started during system bootup.
  "onboot"?: boolean;
  // The OS template or backup file.
  "ostemplate": string;
  // OS type. This is used to setup configuration inside the container, and corresponds to lxc setup scripts in /usr/share/lxc/config/<ostype>.common.conf. Value 'unmanaged' can be used to skip and OS specific setup.
  "ostype"?: "debian" | "devuan" | "ubuntu" | "centos" | "fedora" | "opensuse" | "archlinux" | "alpine" | "gentoo" | "nixos" | "unmanaged";
  // Sets root password inside container.
  "password"?: string;
  // Add the VM to the specified pool.
  "pool"?: string;
  // Sets the protection flag of the container. This will prevent the CT or CT's disk remove/update operation.
  "protection"?: boolean;
  // Mark this as restore task.
  "restore"?: boolean;
  // Use volume as container root.
  "rootfs"?: string;
  // Sets DNS search domains for a container. Create will automatically use the setting from the host if you neither set searchdomain nor nameserver.
  "searchdomain"?: string;
  // Setup public SSH keys (one key per line, OpenSSH format).
  "ssh-public-keys"?: string;
  // Start the CT after its creation finished successfully.
  "start"?: boolean;
  // Startup and shutdown behavior. Order is a non-negative number defining the general startup order. Shutdown in done with reverse ordering. Additionally you can set the 'up' or 'down' delay in seconds, which specifies a delay to wait before the next VM is started or stopped.
  "startup"?: string;
  // Default Storage.
  "storage"?: string;
  // Amount of SWAP for the container in MB.
  "swap"?: number;
  // Tags of the Container. This is only meta information.
  "tags"?: string;
  // Enable/disable Template.
  "template"?: boolean;
  // Time zone to use in the container. If option isn't set, then nothing will be done. Can be set to 'host' to match the host time zone, or an arbitrary time zone option from /usr/share/zoneinfo/zone.tab
  "timezone"?: string;
  // Specify the number of tty available to the container
  "tty"?: number;
  // Assign a unique random ethernet address.
  "unique"?: boolean;
  // Makes the container run as unprivileged user. (Should not be modified manually.)
  "unprivileged"?: boolean;
  // Reference to unused volumes. This is used internally, and should not be modified manually.
  "unused[n]"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}

Destroy the container (also delete all uses files).

### Input Parameters

```ts
interface Params {
  // If set, destroy additionally all disks with the VMID from all enabled storages which are not referenced in the config.
  "destroy-unreferenced-disks"?: boolean;
  // Force destroy, even if running.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
  // Remove container from all related configurations. For example, backup jobs, replication jobs or HA. Related ACLs and Firewall entries will *always* be removed.
  "purge"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}

Directory index

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/config

Get container configuration.

### Input Parameters

```ts
interface Params {
  // Get current values (instead of pending values).
  "current"?: boolean;
  // The cluster node name.
  "node": string;
  // Fetch config values from given snapshot.
  "snapshot"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/config

Set container options.

### Input Parameters

```ts
interface Params {
  // OS architecture type.
  "arch"?: "amd64" | "i386" | "arm64" | "armhf" | "riscv32" | "riscv64";
  // Console mode. By default, the console command tries to open a connection to one of the available tty devices. By setting cmode to 'console' it tries to attach to /dev/console instead. If you set cmode to 'shell', it simply invokes a shell inside the container (no login).
  "cmode"?: "shell" | "console" | "tty";
  // Attach a console device (/dev/console) to the container.
  "console"?: boolean;
  // The number of cores assigned to the container. A container can use all available cores by default.
  "cores"?: number;
  // Limit of CPU usage.  NOTE: If the computer has 2 CPUs, it has a total of '2' CPU time. Value '0' indicates no CPU limit.
  "cpulimit"?: number;
  // CPU weight for a container, will be clamped to [1, 10000] in cgroup v2.
  "cpuunits"?: number;
  // Try to be more verbose. For now this only enables debug log-level on start.
  "debug"?: boolean;
  // A list of settings you want to delete.
  "delete"?: string;
  // Description for the Container. Shown in the web-interface CT's summary. This is saved as comment inside the configuration file.
  "description"?: string;
  // Device to pass through to the container
  "dev[n]"?: string;
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Allow containers access to advanced features.
  "features"?: string;
  // Script that will be executed during various steps in the containers lifetime.
  "hookscript"?: string;
  // Set a host name for the container.
  "hostname"?: string;
  // Lock/unlock the container.
  "lock"?: "backup" | "create" | "destroyed" | "disk" | "fstrim" | "migrate" | "mounted" | "rollback" | "snapshot" | "snapshot-delete";
  // Amount of RAM for the container in MB.
  "memory"?: number;
  // Use volume as container mount point. Use the special syntax STORAGE_ID:SIZE_IN_GiB to allocate a new volume.
  "mp[n]"?: string;
  // Sets DNS server IP address for a container. Create will automatically use the setting from the host if you neither set searchdomain nor nameserver.
  "nameserver"?: string;
  // Specifies network interfaces for the container.
  "net[n]"?: string;
  // The cluster node name.
  "node": string;
  // Specifies whether a container will be started during system bootup.
  "onboot"?: boolean;
  // OS type. This is used to setup configuration inside the container, and corresponds to lxc setup scripts in /usr/share/lxc/config/<ostype>.common.conf. Value 'unmanaged' can be used to skip and OS specific setup.
  "ostype"?: "debian" | "devuan" | "ubuntu" | "centos" | "fedora" | "opensuse" | "archlinux" | "alpine" | "gentoo" | "nixos" | "unmanaged";
  // Sets the protection flag of the container. This will prevent the CT or CT's disk remove/update operation.
  "protection"?: boolean;
  // Revert a pending change.
  "revert"?: string;
  // Use volume as container root.
  "rootfs"?: string;
  // Sets DNS search domains for a container. Create will automatically use the setting from the host if you neither set searchdomain nor nameserver.
  "searchdomain"?: string;
  // Startup and shutdown behavior. Order is a non-negative number defining the general startup order. Shutdown in done with reverse ordering. Additionally you can set the 'up' or 'down' delay in seconds, which specifies a delay to wait before the next VM is started or stopped.
  "startup"?: string;
  // Amount of SWAP for the container in MB.
  "swap"?: number;
  // Tags of the Container. This is only meta information.
  "tags"?: string;
  // Enable/disable Template.
  "template"?: boolean;
  // Time zone to use in the container. If option isn't set, then nothing will be done. Can be set to 'host' to match the host time zone, or an arbitrary time zone option from /usr/share/zoneinfo/zone.tab
  "timezone"?: string;
  // Specify the number of tty available to the container
  "tty"?: number;
  // Makes the container run as unprivileged user. (Should not be modified manually.)
  "unprivileged"?: boolean;
  // Reference to unused volumes. This is used internally, and should not be modified manually.
  "unused[n]"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/status

Directory index

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/status/current

Get virtual machine status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/start

Start the container.

### Input Parameters

```ts
interface Params {
  // If set, enables very verbose debug log-level on start.
  "debug"?: boolean;
  // The cluster node name.
  "node": string;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/stop

Stop the container. This will abruptly stop all processes running in the container.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Try to abort active 'vzshutdown' tasks before stopping.
  "overrule-shutdown"?: boolean;
  // Ignore locks - only root is allowed to use this option.
  "skiplock"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/shutdown

Shutdown the container. This will trigger a clean shutdown of the container, see lxc-stop(1) for details.

### Input Parameters

```ts
interface Params {
  // Make sure the Container stops.
  "forceStop"?: boolean;
  // The cluster node name.
  "node": string;
  // Wait maximal timeout seconds.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/suspend

Suspend the container. This is experimental.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/resume

Resume the container.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/status/reboot

Reboot the container by shutting it down, and starting it again. Applies pending changes.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Wait maximal timeout seconds for the shutdown.
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/snapshot

List all snapshots.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Snapshot description.
  description: string;
  // Snapshot identifier. Value 'current' identifies the current VM.
  name: string;
  // Parent snapshot identifier.
  parent?: string;
  // Snapshot creation time
  snaptime?: number;
}[];
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/snapshot

Snapshot a container.

### Input Parameters

```ts
interface Params {
  // A textual description or comment.
  "description"?: string;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}/snapshot/{snapname}

Delete a LXC snapshot.

### Input Parameters

```ts
interface Params {
  // For removal from config file, even if removing disk snapshots fails.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/snapshot/{snapname}

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/snapshot/{snapname}/rollback

Rollback LXC state to specified snapshot.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // Whether the container should get started after rolling back successfully
  "start"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/snapshot/{snapname}/config

Get snapshot configuration

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/snapshot/{snapname}/config

Update snapshot metadata.

### Input Parameters

```ts
interface Params {
  // A textual description or comment.
  "description"?: string;
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/rules

List rules.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/firewall/rules

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}/firewall/rules/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/rules/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/firewall/rules/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/aliases

List aliases

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
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

## POST /api2/json/nodes/{node}/lxc/{vmid}/firewall/aliases

Create IP or Network Alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}/firewall/aliases/{name}

Remove IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/aliases/{name}

Read alias.

### Input Parameters

```ts
interface Params {
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/firewall/aliases/{name}

Update IP or Network alias.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Alias name.
  "name": string;
  // The cluster node name.
  "node": string;
  // Rename an existing alias.
  "rename"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset

List IPSets

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
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

## POST /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset

Create new IPSet

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // Rename an existing IPSet. You can set 'rename' to the same value as 'name' to update the 'comment' of an existing IPSet.
  "rename"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}

Delete IPSet

### Input Parameters

```ts
interface Params {
  // Delete all members of the IPSet, if there are any.
  "force"?: boolean;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}

List IPSet content

### Input Parameters

```ts
interface Params {
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
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

## POST /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}

Add IP or Network to IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  "nomatch"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}/{cidr}

Remove IP or Network from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}/{cidr}

Read IP or Network settings from IPSet.

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/firewall/ipset/{name}/{cidr}

Update IP or Network settings

### Input Parameters

```ts
interface Params {
  // Network/IP specification in CIDR format.
  "cidr": string;
  "comment"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // IP set name.
  "name": string;
  // The cluster node name.
  "node": string;
  "nomatch"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/options

Get VM firewall options.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/firewall/options

Set Firewall options.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  "delete"?: string;
  // Enable DHCP.
  "dhcp"?: boolean;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable/disable firewall rules.
  "enable"?: boolean;
  // Enable default IP filters. This is equivalent to adding an empty ipfilter-net<id> ipset for every interface. Such ipsets implicitly contain sane default restrictions such as restricting IPv6 link local addresses to the one derived from the interface's MAC address. For containers the configured IP addresses will be implicitly added.
  "ipfilter"?: boolean;
  // Log level for incoming traffic.
  "log_level_in"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Log level for outgoing traffic.
  "log_level_out"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Enable/disable MAC address filter.
  "macfilter"?: boolean;
  // Enable NDP (Neighbor Discovery Protocol).
  "ndp"?: boolean;
  // The cluster node name.
  "node": string;
  // Input policy.
  "policy_in"?: "ACCEPT" | "REJECT" | "DROP";
  // Output policy.
  "policy_out"?: "ACCEPT" | "REJECT" | "DROP";
  // Allow sending Router Advertisement.
  "radv"?: boolean;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/log

Read firewall log

### Input Parameters

```ts
interface Params {
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Display log since this UNIX epoch.
  "since"?: number;
  "start"?: number;
  // Display log until this UNIX epoch.
  "until"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/firewall/refs

Lists possible IPSet/Alias reference which are allowed in source/dest properties.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Only list references of specified type.
  "type"?: "alias" | "ipset";
  // The (unique) ID of the VM.
  "vmid": number;
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

## GET /api2/json/nodes/{node}/lxc/{vmid}/rrd

Read VM RRD statistics (returns PNG)

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The list of datasources you want to display.
  "ds": string;
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/rrddata

Read VM RRD statistics

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/vncproxy

Creates a TCP VNC proxy connections.

### Input Parameters

```ts
interface Params {
  // sets the height of the console in pixels.
  "height"?: number;
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
  // use websocket instead of standard VNC.
  "websocket"?: boolean;
  // sets the width of the console in pixels.
  "width"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/termproxy

Creates a TCP proxy connection.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/vncwebsocket

Opens a weksocket for VNC traffic.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Port number returned by previous vncproxy call.
  "port": number;
  // The (unique) ID of the VM.
  "vmid": number;
  // Ticket from previous call to vncproxy.
  "vncticket": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/spiceproxy

Returns a SPICE configuration to connect to the CT.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // SPICE proxy server. This can be used by the client to specify the proxy server. All nodes in a cluster runs 'spiceproxy', so it is up to the client to choose one. By default, we return the node where the VM is currently running. As reasonable setting is to use same node you use to connect to the API (This is window.location.hostname for the JS GUI).
  "proxy"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/remote_migrate

Migrate the container to another cluster. Creates a new migration task. EXPERIMENTAL feature!

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Delete the original CT and related data after successful migration. By default the original CT is kept on the source cluster in a stopped state.
  "delete"?: boolean;
  // The cluster node name.
  "node": string;
  // Use online/live migration.
  "online"?: boolean;
  // Use restart migration
  "restart"?: boolean;
  // Mapping from source to target bridges. Providing only a single bridge ID maps all source bridges to that bridge. Providing the special value '1' will map each source bridge to itself.
  "target-bridge": string;
  // Remote target endpoint
  "target-endpoint": string;
  // Mapping from source to target storages. Providing only a single storage ID maps all source storages to that storage. Providing the special value '1' will map each source storage to itself.
  "target-storage": string;
  // The (unique) ID of the VM.
  "target-vmid"?: number;
  // Timeout in seconds for shutdown for restart migration
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/migrate

Migrate the container to another node. Creates a new migration task.

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // The cluster node name.
  "node": string;
  // Use online/live migration.
  "online"?: boolean;
  // Use restart migration
  "restart"?: boolean;
  // Target node.
  "target": string;
  // Mapping from source to target storages. Providing only a single storage ID maps all source storages to that storage. Providing the special value '1' will map each source storage to itself.
  "target-storage"?: string;
  // Timeout in seconds for shutdown for restart migration
  "timeout"?: number;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/feature

Check if feature for virtual machine is available.

### Input Parameters

```ts
interface Params {
  // Feature to check.
  "feature": "snapshot" | "clone" | "copy";
  // The cluster node name.
  "node": string;
  // The name of the snapshot.
  "snapname"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/template

Create a Template.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/clone

Create a container clone/copy

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Description for the new CT.
  "description"?: string;
  // Create a full copy of all disks. This is always done when you clone a normal CT. For CT templates, we try to create a linked clone by default.
  "full"?: boolean;
  // Set a hostname for the new CT.
  "hostname"?: string;
  // VMID for the clone.
  "newid": number;
  // The cluster node name.
  "node": string;
  // Add the new CT to the specified pool.
  "pool"?: string;
  // The name of the snapshot.
  "snapname"?: string;
  // Target storage for full clone.
  "storage"?: string;
  // Target node. Only allowed if the original VM is on shared storage.
  "target"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/lxc/{vmid}/resize

Resize a container mount point.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The disk you want to resize.
  "disk": "rootfs" | "mp0" | "mp1" | "mp2" | "mp3" | "mp4" | "mp5" | "mp6" | "mp7" | "mp8" | "mp9" | "mp10" | "mp11" | "mp12" | "mp13" | "mp14" | "mp15" | "mp16" | "mp17" | "mp18" | "mp19" | "mp20" | "mp21" | "mp22" | "mp23" | "mp24" | "mp25" | "mp26" | "mp27" | "mp28" | "mp29" | "mp30" | "mp31" | "mp32" | "mp33" | "mp34" | "mp35" | "mp36" | "mp37" | "mp38" | "mp39" | "mp40" | "mp41" | "mp42" | "mp43" | "mp44" | "mp45" | "mp46" | "mp47" | "mp48" | "mp49" | "mp50" | "mp51" | "mp52" | "mp53" | "mp54" | "mp55" | "mp56" | "mp57" | "mp58" | "mp59" | "mp60" | "mp61" | "mp62" | "mp63" | "mp64" | "mp65" | "mp66" | "mp67" | "mp68" | "mp69" | "mp70" | "mp71" | "mp72" | "mp73" | "mp74" | "mp75" | "mp76" | "mp77" | "mp78" | "mp79" | "mp80" | "mp81" | "mp82" | "mp83" | "mp84" | "mp85" | "mp86" | "mp87" | "mp88" | "mp89" | "mp90" | "mp91" | "mp92" | "mp93" | "mp94" | "mp95" | "mp96" | "mp97" | "mp98" | "mp99" | "mp100" | "mp101" | "mp102" | "mp103" | "mp104" | "mp105" | "mp106" | "mp107" | "mp108" | "mp109" | "mp110" | "mp111" | "mp112" | "mp113" | "mp114" | "mp115" | "mp116" | "mp117" | "mp118" | "mp119" | "mp120" | "mp121" | "mp122" | "mp123" | "mp124" | "mp125" | "mp126" | "mp127" | "mp128" | "mp129" | "mp130" | "mp131" | "mp132" | "mp133" | "mp134" | "mp135" | "mp136" | "mp137" | "mp138" | "mp139" | "mp140" | "mp141" | "mp142" | "mp143" | "mp144" | "mp145" | "mp146" | "mp147" | "mp148" | "mp149" | "mp150" | "mp151" | "mp152" | "mp153" | "mp154" | "mp155" | "mp156" | "mp157" | "mp158" | "mp159" | "mp160" | "mp161" | "mp162" | "mp163" | "mp164" | "mp165" | "mp166" | "mp167" | "mp168" | "mp169" | "mp170" | "mp171" | "mp172" | "mp173" | "mp174" | "mp175" | "mp176" | "mp177" | "mp178" | "mp179" | "mp180" | "mp181" | "mp182" | "mp183" | "mp184" | "mp185" | "mp186" | "mp187" | "mp188" | "mp189" | "mp190" | "mp191" | "mp192" | "mp193" | "mp194" | "mp195" | "mp196" | "mp197" | "mp198" | "mp199" | "mp200" | "mp201" | "mp202" | "mp203" | "mp204" | "mp205" | "mp206" | "mp207" | "mp208" | "mp209" | "mp210" | "mp211" | "mp212" | "mp213" | "mp214" | "mp215" | "mp216" | "mp217" | "mp218" | "mp219" | "mp220" | "mp221" | "mp222" | "mp223" | "mp224" | "mp225" | "mp226" | "mp227" | "mp228" | "mp229" | "mp230" | "mp231" | "mp232" | "mp233" | "mp234" | "mp235" | "mp236" | "mp237" | "mp238" | "mp239" | "mp240" | "mp241" | "mp242" | "mp243" | "mp244" | "mp245" | "mp246" | "mp247" | "mp248" | "mp249" | "mp250" | "mp251" | "mp252" | "mp253" | "mp254" | "mp255";
  // The cluster node name.
  "node": string;
  // The new size. With the '+' sign the value is added to the actual size of the volume and without it, the value is taken as an absolute one. Shrinking disk size is not supported.
  "size": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/move_volume

Move a rootfs-/mp-volume to a different storage or to a different container.

### Input Parameters

```ts
interface Params {
  // Override I/O bandwidth limit (in KiB/s).
  "bwlimit"?: number;
  // Delete the original volume after successful copy. By default the original is kept as an unused volume entry.
  "delete"?: boolean;
  // Prevent changes if current configuration file has different SHA1 " . 		    "digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
  // Target Storage.
  "storage"?: string;
  // Prevent changes if current configuration file of the target " . 		    "container has a different SHA1 digest. This can be used to prevent " . 		    "concurrent modifications.
  "target-digest"?: string;
  // The (unique) ID of the VM.
  "target-vmid"?: number;
  // The config key the volume will be moved to. Default is the source volume key.
  "target-volume"?: "rootfs" | "mp0" | "mp1" | "mp2" | "mp3" | "mp4" | "mp5" | "mp6" | "mp7" | "mp8" | "mp9" | "mp10" | "mp11" | "mp12" | "mp13" | "mp14" | "mp15" | "mp16" | "mp17" | "mp18" | "mp19" | "mp20" | "mp21" | "mp22" | "mp23" | "mp24" | "mp25" | "mp26" | "mp27" | "mp28" | "mp29" | "mp30" | "mp31" | "mp32" | "mp33" | "mp34" | "mp35" | "mp36" | "mp37" | "mp38" | "mp39" | "mp40" | "mp41" | "mp42" | "mp43" | "mp44" | "mp45" | "mp46" | "mp47" | "mp48" | "mp49" | "mp50" | "mp51" | "mp52" | "mp53" | "mp54" | "mp55" | "mp56" | "mp57" | "mp58" | "mp59" | "mp60" | "mp61" | "mp62" | "mp63" | "mp64" | "mp65" | "mp66" | "mp67" | "mp68" | "mp69" | "mp70" | "mp71" | "mp72" | "mp73" | "mp74" | "mp75" | "mp76" | "mp77" | "mp78" | "mp79" | "mp80" | "mp81" | "mp82" | "mp83" | "mp84" | "mp85" | "mp86" | "mp87" | "mp88" | "mp89" | "mp90" | "mp91" | "mp92" | "mp93" | "mp94" | "mp95" | "mp96" | "mp97" | "mp98" | "mp99" | "mp100" | "mp101" | "mp102" | "mp103" | "mp104" | "mp105" | "mp106" | "mp107" | "mp108" | "mp109" | "mp110" | "mp111" | "mp112" | "mp113" | "mp114" | "mp115" | "mp116" | "mp117" | "mp118" | "mp119" | "mp120" | "mp121" | "mp122" | "mp123" | "mp124" | "mp125" | "mp126" | "mp127" | "mp128" | "mp129" | "mp130" | "mp131" | "mp132" | "mp133" | "mp134" | "mp135" | "mp136" | "mp137" | "mp138" | "mp139" | "mp140" | "mp141" | "mp142" | "mp143" | "mp144" | "mp145" | "mp146" | "mp147" | "mp148" | "mp149" | "mp150" | "mp151" | "mp152" | "mp153" | "mp154" | "mp155" | "mp156" | "mp157" | "mp158" | "mp159" | "mp160" | "mp161" | "mp162" | "mp163" | "mp164" | "mp165" | "mp166" | "mp167" | "mp168" | "mp169" | "mp170" | "mp171" | "mp172" | "mp173" | "mp174" | "mp175" | "mp176" | "mp177" | "mp178" | "mp179" | "mp180" | "mp181" | "mp182" | "mp183" | "mp184" | "mp185" | "mp186" | "mp187" | "mp188" | "mp189" | "mp190" | "mp191" | "mp192" | "mp193" | "mp194" | "mp195" | "mp196" | "mp197" | "mp198" | "mp199" | "mp200" | "mp201" | "mp202" | "mp203" | "mp204" | "mp205" | "mp206" | "mp207" | "mp208" | "mp209" | "mp210" | "mp211" | "mp212" | "mp213" | "mp214" | "mp215" | "mp216" | "mp217" | "mp218" | "mp219" | "mp220" | "mp221" | "mp222" | "mp223" | "mp224" | "mp225" | "mp226" | "mp227" | "mp228" | "mp229" | "mp230" | "mp231" | "mp232" | "mp233" | "mp234" | "mp235" | "mp236" | "mp237" | "mp238" | "mp239" | "mp240" | "mp241" | "mp242" | "mp243" | "mp244" | "mp245" | "mp246" | "mp247" | "mp248" | "mp249" | "mp250" | "mp251" | "mp252" | "mp253" | "mp254" | "mp255" | "unused0" | "unused1" | "unused2" | "unused3" | "unused4" | "unused5" | "unused6" | "unused7" | "unused8" | "unused9" | "unused10" | "unused11" | "unused12" | "unused13" | "unused14" | "unused15" | "unused16" | "unused17" | "unused18" | "unused19" | "unused20" | "unused21" | "unused22" | "unused23" | "unused24" | "unused25" | "unused26" | "unused27" | "unused28" | "unused29" | "unused30" | "unused31" | "unused32" | "unused33" | "unused34" | "unused35" | "unused36" | "unused37" | "unused38" | "unused39" | "unused40" | "unused41" | "unused42" | "unused43" | "unused44" | "unused45" | "unused46" | "unused47" | "unused48" | "unused49" | "unused50" | "unused51" | "unused52" | "unused53" | "unused54" | "unused55" | "unused56" | "unused57" | "unused58" | "unused59" | "unused60" | "unused61" | "unused62" | "unused63" | "unused64" | "unused65" | "unused66" | "unused67" | "unused68" | "unused69" | "unused70" | "unused71" | "unused72" | "unused73" | "unused74" | "unused75" | "unused76" | "unused77" | "unused78" | "unused79" | "unused80" | "unused81" | "unused82" | "unused83" | "unused84" | "unused85" | "unused86" | "unused87" | "unused88" | "unused89" | "unused90" | "unused91" | "unused92" | "unused93" | "unused94" | "unused95" | "unused96" | "unused97" | "unused98" | "unused99" | "unused100" | "unused101" | "unused102" | "unused103" | "unused104" | "unused105" | "unused106" | "unused107" | "unused108" | "unused109" | "unused110" | "unused111" | "unused112" | "unused113" | "unused114" | "unused115" | "unused116" | "unused117" | "unused118" | "unused119" | "unused120" | "unused121" | "unused122" | "unused123" | "unused124" | "unused125" | "unused126" | "unused127" | "unused128" | "unused129" | "unused130" | "unused131" | "unused132" | "unused133" | "unused134" | "unused135" | "unused136" | "unused137" | "unused138" | "unused139" | "unused140" | "unused141" | "unused142" | "unused143" | "unused144" | "unused145" | "unused146" | "unused147" | "unused148" | "unused149" | "unused150" | "unused151" | "unused152" | "unused153" | "unused154" | "unused155" | "unused156" | "unused157" | "unused158" | "unused159" | "unused160" | "unused161" | "unused162" | "unused163" | "unused164" | "unused165" | "unused166" | "unused167" | "unused168" | "unused169" | "unused170" | "unused171" | "unused172" | "unused173" | "unused174" | "unused175" | "unused176" | "unused177" | "unused178" | "unused179" | "unused180" | "unused181" | "unused182" | "unused183" | "unused184" | "unused185" | "unused186" | "unused187" | "unused188" | "unused189" | "unused190" | "unused191" | "unused192" | "unused193" | "unused194" | "unused195" | "unused196" | "unused197" | "unused198" | "unused199" | "unused200" | "unused201" | "unused202" | "unused203" | "unused204" | "unused205" | "unused206" | "unused207" | "unused208" | "unused209" | "unused210" | "unused211" | "unused212" | "unused213" | "unused214" | "unused215" | "unused216" | "unused217" | "unused218" | "unused219" | "unused220" | "unused221" | "unused222" | "unused223" | "unused224" | "unused225" | "unused226" | "unused227" | "unused228" | "unused229" | "unused230" | "unused231" | "unused232" | "unused233" | "unused234" | "unused235" | "unused236" | "unused237" | "unused238" | "unused239" | "unused240" | "unused241" | "unused242" | "unused243" | "unused244" | "unused245" | "unused246" | "unused247" | "unused248" | "unused249" | "unused250" | "unused251" | "unused252" | "unused253" | "unused254" | "unused255";
  // The (unique) ID of the VM.
  "vmid": number;
  // Volume which will be moved.
  "volume": "rootfs" | "mp0" | "mp1" | "mp2" | "mp3" | "mp4" | "mp5" | "mp6" | "mp7" | "mp8" | "mp9" | "mp10" | "mp11" | "mp12" | "mp13" | "mp14" | "mp15" | "mp16" | "mp17" | "mp18" | "mp19" | "mp20" | "mp21" | "mp22" | "mp23" | "mp24" | "mp25" | "mp26" | "mp27" | "mp28" | "mp29" | "mp30" | "mp31" | "mp32" | "mp33" | "mp34" | "mp35" | "mp36" | "mp37" | "mp38" | "mp39" | "mp40" | "mp41" | "mp42" | "mp43" | "mp44" | "mp45" | "mp46" | "mp47" | "mp48" | "mp49" | "mp50" | "mp51" | "mp52" | "mp53" | "mp54" | "mp55" | "mp56" | "mp57" | "mp58" | "mp59" | "mp60" | "mp61" | "mp62" | "mp63" | "mp64" | "mp65" | "mp66" | "mp67" | "mp68" | "mp69" | "mp70" | "mp71" | "mp72" | "mp73" | "mp74" | "mp75" | "mp76" | "mp77" | "mp78" | "mp79" | "mp80" | "mp81" | "mp82" | "mp83" | "mp84" | "mp85" | "mp86" | "mp87" | "mp88" | "mp89" | "mp90" | "mp91" | "mp92" | "mp93" | "mp94" | "mp95" | "mp96" | "mp97" | "mp98" | "mp99" | "mp100" | "mp101" | "mp102" | "mp103" | "mp104" | "mp105" | "mp106" | "mp107" | "mp108" | "mp109" | "mp110" | "mp111" | "mp112" | "mp113" | "mp114" | "mp115" | "mp116" | "mp117" | "mp118" | "mp119" | "mp120" | "mp121" | "mp122" | "mp123" | "mp124" | "mp125" | "mp126" | "mp127" | "mp128" | "mp129" | "mp130" | "mp131" | "mp132" | "mp133" | "mp134" | "mp135" | "mp136" | "mp137" | "mp138" | "mp139" | "mp140" | "mp141" | "mp142" | "mp143" | "mp144" | "mp145" | "mp146" | "mp147" | "mp148" | "mp149" | "mp150" | "mp151" | "mp152" | "mp153" | "mp154" | "mp155" | "mp156" | "mp157" | "mp158" | "mp159" | "mp160" | "mp161" | "mp162" | "mp163" | "mp164" | "mp165" | "mp166" | "mp167" | "mp168" | "mp169" | "mp170" | "mp171" | "mp172" | "mp173" | "mp174" | "mp175" | "mp176" | "mp177" | "mp178" | "mp179" | "mp180" | "mp181" | "mp182" | "mp183" | "mp184" | "mp185" | "mp186" | "mp187" | "mp188" | "mp189" | "mp190" | "mp191" | "mp192" | "mp193" | "mp194" | "mp195" | "mp196" | "mp197" | "mp198" | "mp199" | "mp200" | "mp201" | "mp202" | "mp203" | "mp204" | "mp205" | "mp206" | "mp207" | "mp208" | "mp209" | "mp210" | "mp211" | "mp212" | "mp213" | "mp214" | "mp215" | "mp216" | "mp217" | "mp218" | "mp219" | "mp220" | "mp221" | "mp222" | "mp223" | "mp224" | "mp225" | "mp226" | "mp227" | "mp228" | "mp229" | "mp230" | "mp231" | "mp232" | "mp233" | "mp234" | "mp235" | "mp236" | "mp237" | "mp238" | "mp239" | "mp240" | "mp241" | "mp242" | "mp243" | "mp244" | "mp245" | "mp246" | "mp247" | "mp248" | "mp249" | "mp250" | "mp251" | "mp252" | "mp253" | "mp254" | "mp255" | "unused0" | "unused1" | "unused2" | "unused3" | "unused4" | "unused5" | "unused6" | "unused7" | "unused8" | "unused9" | "unused10" | "unused11" | "unused12" | "unused13" | "unused14" | "unused15" | "unused16" | "unused17" | "unused18" | "unused19" | "unused20" | "unused21" | "unused22" | "unused23" | "unused24" | "unused25" | "unused26" | "unused27" | "unused28" | "unused29" | "unused30" | "unused31" | "unused32" | "unused33" | "unused34" | "unused35" | "unused36" | "unused37" | "unused38" | "unused39" | "unused40" | "unused41" | "unused42" | "unused43" | "unused44" | "unused45" | "unused46" | "unused47" | "unused48" | "unused49" | "unused50" | "unused51" | "unused52" | "unused53" | "unused54" | "unused55" | "unused56" | "unused57" | "unused58" | "unused59" | "unused60" | "unused61" | "unused62" | "unused63" | "unused64" | "unused65" | "unused66" | "unused67" | "unused68" | "unused69" | "unused70" | "unused71" | "unused72" | "unused73" | "unused74" | "unused75" | "unused76" | "unused77" | "unused78" | "unused79" | "unused80" | "unused81" | "unused82" | "unused83" | "unused84" | "unused85" | "unused86" | "unused87" | "unused88" | "unused89" | "unused90" | "unused91" | "unused92" | "unused93" | "unused94" | "unused95" | "unused96" | "unused97" | "unused98" | "unused99" | "unused100" | "unused101" | "unused102" | "unused103" | "unused104" | "unused105" | "unused106" | "unused107" | "unused108" | "unused109" | "unused110" | "unused111" | "unused112" | "unused113" | "unused114" | "unused115" | "unused116" | "unused117" | "unused118" | "unused119" | "unused120" | "unused121" | "unused122" | "unused123" | "unused124" | "unused125" | "unused126" | "unused127" | "unused128" | "unused129" | "unused130" | "unused131" | "unused132" | "unused133" | "unused134" | "unused135" | "unused136" | "unused137" | "unused138" | "unused139" | "unused140" | "unused141" | "unused142" | "unused143" | "unused144" | "unused145" | "unused146" | "unused147" | "unused148" | "unused149" | "unused150" | "unused151" | "unused152" | "unused153" | "unused154" | "unused155" | "unused156" | "unused157" | "unused158" | "unused159" | "unused160" | "unused161" | "unused162" | "unused163" | "unused164" | "unused165" | "unused166" | "unused167" | "unused168" | "unused169" | "unused170" | "unused171" | "unused172" | "unused173" | "unused174" | "unused175" | "unused176" | "unused177" | "unused178" | "unused179" | "unused180" | "unused181" | "unused182" | "unused183" | "unused184" | "unused185" | "unused186" | "unused187" | "unused188" | "unused189" | "unused190" | "unused191" | "unused192" | "unused193" | "unused194" | "unused195" | "unused196" | "unused197" | "unused198" | "unused199" | "unused200" | "unused201" | "unused202" | "unused203" | "unused204" | "unused205" | "unused206" | "unused207" | "unused208" | "unused209" | "unused210" | "unused211" | "unused212" | "unused213" | "unused214" | "unused215" | "unused216" | "unused217" | "unused218" | "unused219" | "unused220" | "unused221" | "unused222" | "unused223" | "unused224" | "unused225" | "unused226" | "unused227" | "unused228" | "unused229" | "unused230" | "unused231" | "unused232" | "unused233" | "unused234" | "unused235" | "unused236" | "unused237" | "unused238" | "unused239" | "unused240" | "unused241" | "unused242" | "unused243" | "unused244" | "unused245" | "unused246" | "unused247" | "unused248" | "unused249" | "unused250" | "unused251" | "unused252" | "unused253" | "unused254" | "unused255";
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/pending

Get container configuration, including pending changes.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // Indicates a pending delete request if present and not 0.
  delete?: number;
  // Configuration option name.
  key: string;
  // Pending value.
  pending?: string;
  // Current value.
  value?: string;
}[];
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/interfaces

Get IP addresses of the specified container interface.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = {
  // The MAC address of the interface
  hardware-address: string;
  // The MAC address of the interface
  hwaddr: string;
  // The IPv4 address of the interface
  inet?: string;
  // The IPv6 address of the interface
  inet6?: string;
  // The addresses of the interface
  ip-addresses: {
  // IP-Address
  ip-address?: string;
  // IP-Family
  ip-address-type?: string;
  // IP-Prefix
  prefix?: number;
}[];
  // The name of the interface
  name: string;
}[];
```

## POST /api2/json/nodes/{node}/lxc/{vmid}/mtunnel

Migration tunnel endpoint - only for internal use by CT migration.

### Input Parameters

```ts
interface Params {
  // List of network bridges to check availability. Will be checked again for actually used bridges during migration.
  "bridges"?: string;
  // The cluster node name.
  "node": string;
  // List of storages to check permission and availability. Will be checked again for all actually used storages during migration.
  "storages"?: string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/lxc/{vmid}/mtunnelwebsocket

Migration tunnel endpoint for websocket upgrade - only for internal use by VM migration.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // unix socket to forward to
  "socket": string;
  // ticket return by initial 'mtunnel' API call, or retrieved via 'ticket' tunnel command
  "ticket": string;
  // The (unique) ID of the VM.
  "vmid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/ceph

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/ceph/cfg

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/ceph/cfg/raw

Get the Ceph configuration file.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/cfg/db

Get the Ceph configuration database.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  can_update_at_runtime: boolean;
  level: string;
  mask: string;
  name: string;
  section: string;
  value: string;
}[];
```

## GET /api2/json/nodes/{node}/ceph/cfg/value

Get configured values from either the config file or config DB.

### Input Parameters

```ts
interface Params {
  // List of <section>:<config key> items.
  "config-keys": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/ceph/osd

Get Ceph osd list/tree.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/osd

Create OSD

### Input Parameters

```ts
interface Params {
  // Set the device class of the OSD in crush.
  "crush-device-class"?: string;
  // Block device name for block.db.
  "db_dev"?: string;
  // Size in GiB for block.db.
  "db_dev_size"?: number;
  // Block device name.
  "dev": string;
  // Enables encryption of the OSD.
  "encrypted"?: boolean;
  // The cluster node name.
  "node": string;
  // OSD services per physical device. Only useful for fast NVMe devices" 		    ." to utilize their performance better.
  "osds-per-device"?: number;
  // Block device name for block.wal.
  "wal_dev"?: string;
  // Size in GiB for block.wal.
  "wal_dev_size"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/ceph/osd/{osdid}

Destroy OSD

### Input Parameters

```ts
interface Params {
  // If set, we remove partition table entries.
  "cleanup"?: boolean;
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/osd/{osdid}

OSD index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/ceph/osd/{osdid}/metadata

Get OSD details

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/ceph/osd/{osdid}/lv-info

Get OSD volume details

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
  // OSD device type
  "type"?: "block" | "db" | "wal";
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/osd/{osdid}/in

ceph osd in

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/osd/{osdid}/out

ceph osd out

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/osd/{osdid}/scrub

Instruct the OSD to scrub.

### Input Parameters

```ts
interface Params {
  // If set, instructs a deep scrub instead of a normal one.
  "deep"?: boolean;
  // The cluster node name.
  "node": string;
  // OSD ID
  "osdid": number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/ceph/mds

MDS directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  addr?: string;
  host?: string;
  // The name (ID) for the MDS
  name: any;
  rank?: number;
  // If true, the standby MDS is polling the active MDS for faster recovery (hot standby).
  standby_replay?: boolean;
  // State of the MDS
  state: string;
}[];
```

## DELETE /api2/json/nodes/{node}/ceph/mds/{name}

Destroy Ceph Metadata Server

### Input Parameters

```ts
interface Params {
  // The name (ID) of the mds
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/ceph/mds/{name}

Create Ceph Metadata Server (MDS)

### Input Parameters

```ts
interface Params {
  // Determines whether a ceph-mds daemon should poll and replay the log of an active MDS. Faster switch on MDS failure, but needs more idle resources.
  "hotstandby"?: boolean;
  // The ID for the mds, when omitted the same as the nodename
  "name"?: string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/mgr

MGR directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  addr?: string;
  host?: string;
  // The name (ID) for the MGR
  name: any;
  // State of the MGR
  state: string;
}[];
```

## DELETE /api2/json/nodes/{node}/ceph/mgr/{id}

Destroy Ceph Manager.

### Input Parameters

```ts
interface Params {
  // The ID of the manager
  "id": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/ceph/mgr/{id}

Create Ceph Manager

### Input Parameters

```ts
interface Params {
  // The ID for the manager, when omitted the same as the nodename
  "id"?: string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/mon

Get Ceph monitor list.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  addr?: string;
  ceph_version?: string;
  ceph_version_short?: string;
  direxists?: string;
  host?: boolean;
  name: string;
  quorum?: boolean;
  rank?: number;
  service?: number;
  state?: string;
}[];
```

## DELETE /api2/json/nodes/{node}/ceph/mon/{monid}

Destroy Ceph Monitor and Manager.

### Input Parameters

```ts
interface Params {
  // Monitor ID
  "monid": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/ceph/mon/{monid}

Create Ceph Monitor and Manager

### Input Parameters

```ts
interface Params {
  // Overwrites autodetected monitor IP address(es). Must be in the public network(s) of Ceph.
  "mon-address"?: string;
  // The ID for the monitor, when omitted the same as the nodename
  "monid"?: string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/fs

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // The name of the data pool.
  data_pool: string;
  // The name of the metadata pool.
  metadata_pool: string;
  // The ceph filesystem name.
  name: string;
}[];
```

## POST /api2/json/nodes/{node}/ceph/fs/{name}

Create a Ceph filesystem

### Input Parameters

```ts
interface Params {
  // Configure the created CephFS as storage for this cluster.
  "add-storage"?: boolean;
  // The ceph filesystem name.
  "name"?: string;
  // The cluster node name.
  "node": string;
  // Number of placement groups for the backing data pool. The metadata pool will use a quarter of this.
  "pg_num"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/pool

List all pools and their settings (which are settable by the POST/PUT endpoints).

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  application_metadata?: any;
  autoscale_status?: any;
  bytes_used: number;
  crush_rule: number;
  crush_rule_name: string;
  min_size: number;
  percent_used: number;
  pg_autoscale_mode?: string;
  pg_num: number;
  pg_num_final?: number;
  pg_num_min?: number;
  pool: number;
  pool_name: string;
  size: number;
  target_size?: number;
  target_size_ratio?: number;
  type: "replicated" | "erasure" | "unknown";
}[];
```

## POST /api2/json/nodes/{node}/ceph/pool

Create Ceph pool

### Input Parameters

```ts
interface Params {
  // Configure VM and CT storage using the new pool.
  "add_storages"?: boolean;
  // The application of the pool.
  "application"?: "rbd" | "cephfs" | "rgw";
  // The rule to use for mapping object placement in the cluster.
  "crush_rule"?: string;
  // Create an erasure coded pool for RBD with an accompaning replicated pool for metadata storage. With EC, the common ceph options 'size', 'min_size' and 'crush_rule' parameters will be applied to the metadata pool.
  "erasure-coding"?: string;
  // Minimum number of replicas per object
  "min_size"?: number;
  // The name of the pool. It must be unique.
  "name": string;
  // The cluster node name.
  "node": string;
  // The automatic PG scaling mode of the pool.
  "pg_autoscale_mode"?: "on" | "off" | "warn";
  // Number of placement groups.
  "pg_num"?: number;
  // Minimal number of placement groups.
  "pg_num_min"?: number;
  // Number of replicas per object
  "size"?: number;
  // The estimated target size of the pool for the PG autoscaler.
  "target_size"?: string;
  // The estimated target ratio of the pool for the PG autoscaler.
  "target_size_ratio"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/ceph/pool/{name}

Destroy pool

### Input Parameters

```ts
interface Params {
  // If true, destroys pool even if in use
  "force"?: boolean;
  // The name of the pool. It must be unique.
  "name": string;
  // The cluster node name.
  "node": string;
  // Remove the erasure code profile. Defaults to true, if applicable.
  "remove_ecprofile"?: boolean;
  // Remove all pveceph-managed storages configured for this pool
  "remove_storages"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/pool/{name}

Pool index.

### Input Parameters

```ts
interface Params {
  // The name of the pool.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## PUT /api2/json/nodes/{node}/ceph/pool/{name}

Change POOL settings

### Input Parameters

```ts
interface Params {
  // The application of the pool.
  "application"?: "rbd" | "cephfs" | "rgw";
  // The rule to use for mapping object placement in the cluster.
  "crush_rule"?: string;
  // Minimum number of replicas per object
  "min_size"?: number;
  // The name of the pool. It must be unique.
  "name": string;
  // The cluster node name.
  "node": string;
  // The automatic PG scaling mode of the pool.
  "pg_autoscale_mode"?: "on" | "off" | "warn";
  // Number of placement groups.
  "pg_num"?: number;
  // Minimal number of placement groups.
  "pg_num_min"?: number;
  // Number of replicas per object
  "size"?: number;
  // The estimated target size of the pool for the PG autoscaler.
  "target_size"?: string;
  // The estimated target ratio of the pool for the PG autoscaler.
  "target_size_ratio"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/pool/{name}/status

Show the current pool status.

### Input Parameters

```ts
interface Params {
  // The name of the pool. It must be unique.
  "name": string;
  // The cluster node name.
  "node": string;
  // If enabled, will display additional data(eg. statistics).
  "verbose"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/init

Create initial ceph default configuration and setup symlinks.

### Input Parameters

```ts
interface Params {
  // Declare a separate cluster network, OSDs will routeheartbeat, object replication and recovery traffic over it
  "cluster-network"?: string;
  // Disable cephx authentication.  WARNING: cephx is a security feature protecting against man-in-the-middle attacks. Only consider disabling cephx if your network is private!
  "disable_cephx"?: boolean;
  // Minimum number of available replicas per object to allow I/O
  "min_size"?: number;
  // Use specific network for all ceph related traffic
  "network"?: string;
  // The cluster node name.
  "node": string;
  // Placement group bits, used to specify the default number of placement groups.  Depreacted. This setting was deprecated in recent Ceph versions.
  "pg_bits"?: number;
  // Targeted number of replicas per object
  "size"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/ceph/stop

Stop ceph services.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Ceph service name.
  "service"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/ceph/start

Start ceph services.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Ceph service name.
  "service"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/ceph/restart

Restart ceph services.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Ceph service name.
  "service"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/status

Get ceph status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/ceph/crush

Get OSD crush map

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/ceph/log

Read ceph log

### Input Parameters

```ts
interface Params {
  "limit"?: number;
  // The cluster node name.
  "node": string;
  "start"?: number;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/ceph/rules

List ceph rules.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // Name of the CRUSH rule.
  name: string;
}[];
```

## GET /api2/json/nodes/{node}/ceph/cmd-safety

Heuristical check if it is safe to perform an action.

### Input Parameters

```ts
interface Params {
  // Action to check
  "action": "stop" | "destroy";
  // ID of the service
  "id": string;
  // The cluster node name.
  "node": string;
  // Service type
  "service": "osd" | "mon" | "mds";
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/vzdump

Create backup.

### Input Parameters

```ts
interface Params {
  // Backup all known guest systems on this host.
  "all"?: boolean;
  // Limit I/O bandwidth (in KiB/s).
  "bwlimit"?: number;
  // Compress dump file.
  "compress"?: "0" | "1" | "gzip" | "lzo" | "zstd";
  // Store resulting files to specified directory.
  "dumpdir"?: string;
  // Exclude specified guest systems (assumes --all)
  "exclude"?: string;
  // Exclude certain files/directories (shell globs). Paths starting with '/' are anchored to the container's root, other paths match relative to each subdirectory.
  "exclude-path"?: object[];
  // Options for backup fleecing (VM only).
  "fleecing"?: string;
  // Set IO priority when using the BFQ scheduler. For snapshot and suspend mode backups of VMs, this only affects the compressor. A value of 8 means the idle priority is used, otherwise the best-effort priority is used with the specified value.
  "ionice"?: number;
  // The ID of the backup job. If set, the 'backup-job' metadata field of the backup notification will be set to this value. Only root@pam can set this parameter.
  "job-id"?: string;
  // Maximal time to wait for the global lock (minutes).
  "lockwait"?: number;
  // Deprecated: use notification targets/matchers instead. Specify when to send a notification mail
  "mailnotification"?: "always" | "failure";
  // Deprecated: Use notification targets/matchers instead. Comma-separated list of email addresses or users that should receive email notifications.
  "mailto"?: string;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per guest system.
  "maxfiles"?: number;
  // Backup mode.
  "mode"?: "snapshot" | "suspend" | "stop";
  // Only run if executed on this node.
  "node"?: string;
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
  "performance"?: string;
  // Use pigz instead of gzip when N>0. N=1 uses half of cores, N>1 uses N as thread count.
  "pigz"?: number;
  // Backup all known guest systems included in the specified pool.
  "pool"?: string;
  // If true, mark backup(s) as protected.
  "protected"?: boolean;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // Be quiet.
  "quiet"?: boolean;
  // Prune older backups according to 'prune-backups'.
  "remove"?: boolean;
  // Use specified hook script.
  "script"?: string;
  // Exclude temporary files and logs.
  "stdexcludes"?: boolean;
  // Write tar to stdout, not to a file.
  "stdout"?: boolean;
  // Stop running backup jobs on this host.
  "stop"?: boolean;
  // Maximal time to wait until a guest system is stopped (minutes).
  "stopwait"?: number;
  // Store resulting file to this storage.
  "storage"?: string;
  // Store temporary files to specified directory.
  "tmpdir"?: string;
  // The ID of the guest system you want to backup.
  "vmid"?: string;
  // Zstd threads. N=0 uses half of the available cores, if N is set to a value bigger than 0, N is used as thread count.
  "zstd"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/vzdump/defaults

Get the currently configured vzdump defaults.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/vzdump/extractconfig

Extract configuration from vzdump backup archive.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Volume identifier
  "volume": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/services

Service list.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/services/{service}

Directory index

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/services/{service}/state

Read service properties

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/services/{service}/start

Start service.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/services/{service}/stop

Stop service.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/services/{service}/restart

Hard restart service. Use reload if you want to reduce interruptions.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/services/{service}/reload

Reload service. Falls back to restart if service cannot be reloaded.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Service ID
  "service": "chrony" | "corosync" | "cron" | "ksmtuned" | "postfix" | "pve-cluster" | "pve-firewall" | "pve-ha-crm" | "pve-ha-lrm" | "pvedaemon" | "pvefw-logger" | "pveproxy" | "pvescheduler" | "pvestatd" | "spiceproxy" | "sshd" | "syslog" | "systemd-journald" | "systemd-timesyncd";
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/subscription

Delete subscription key of this node.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/subscription

Read subscription info.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/subscription

Update subscription info.

### Input Parameters

```ts
interface Params {
  // Always connect to server, even if local cache is still valid.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/subscription

Set subscription key.

### Input Parameters

```ts
interface Params {
  // Proxmox VE subscription key
  "key": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/network

Revert network configuration changes.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/network

List available networks

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Only list specific interface types.
  "type"?: "bridge" | "bond" | "eth" | "alias" | "vlan" | "OVSBridge" | "OVSBond" | "OVSPort" | "OVSIntPort" | "vnet" | "any_bridge" | "any_local_bridge";
}
```

### Returns

```ts
type Returns = {
  // Set to true if the interface is active.
  active?: boolean;
  // IP address.
  address?: string;
  // IP address.
  address6?: string;
  // Automatically start interface on boot.
  autostart?: boolean;
  // Specify the primary interface for active-backup bond.
  bond-primary?: string;
  // Bonding mode.
  bond_mode?: "balance-rr" | "active-backup" | "balance-xor" | "broadcast" | "802.3ad" | "balance-tlb" | "balance-alb" | "balance-slb" | "lacp-balance-slb" | "lacp-balance-tcp";
  // Selects the transmit hash policy to use for slave selection in balance-xor and 802.3ad modes.
  bond_xmit_hash_policy?: "layer2" | "layer2+3" | "layer3+4";
  // The bridge port access VLAN.
  bridge-access?: number;
  // Bridge port ARP/ND suppress flag.
  bridge-arp-nd-suppress?: boolean;
  // Bridge port learning flag.
  bridge-learning?: boolean;
  // Bridge port multicast flood flag.
  bridge-multicast-flood?: boolean;
  // Bridge port unicast flood flag.
  bridge-unicast-flood?: boolean;
  // Specify the interfaces you want to add to your bridge.
  bridge_ports?: string;
  // Specify the allowed VLANs. For example: '2 4 100-200'. Only used if the bridge is VLAN aware.
  bridge_vids?: string;
  // Enable bridge vlan support.
  bridge_vlan_aware?: boolean;
  // IPv4 CIDR.
  cidr?: string;
  // IPv6 CIDR.
  cidr6?: string;
  // Comments
  comments?: string;
  // Comments
  comments6?: string;
  // Set to true if the interface physically exists.
  exists?: boolean;
  // The network families.
  families?: object[];
  // Default gateway address.
  gateway?: string;
  // Default ipv6 gateway address.
  gateway6?: string;
  // Network interface name.
  iface: string;
  // The link type.
  link-type?: string;
  // The network configuration method for IPv4.
  method?: "loopback" | "dhcp" | "manual" | "static" | "auto";
  // The network configuration method for IPv6.
  method6?: "loopback" | "dhcp" | "manual" | "static" | "auto";
  // MTU.
  mtu?: number;
  // Network mask.
  netmask?: string;
  // Network mask.
  netmask6?: number;
  // A list of additional interface options for IPv4.
  options?: object[];
  // A list of additional interface options for IPv6.
  options6?: object[];
  // Specify the interfaces used by the bonding device.
  ovs_bonds?: string;
  // The OVS bridge associated with a OVS port. This is required when you create an OVS port.
  ovs_bridge?: string;
  // OVS interface options.
  ovs_options?: string;
  // Specify the interfaces you want to add to your bridge.
  ovs_ports?: string;
  // Specify a VLan tag (used by OVSPort, OVSIntPort, OVSBond)
  ovs_tag?: number;
  // The order of the interface.
  priority?: number;
  // Specify the interfaces used by the bonding device.
  slaves?: string;
  // Network interface type
  type: "bridge" | "bond" | "eth" | "alias" | "vlan" | "OVSBridge" | "OVSBond" | "OVSPort" | "OVSIntPort" | "vnet" | "unknown";
  // The uplink ID.
  uplink-id?: string;
  // vlan-id for a custom named vlan interface (ifupdown2 only).
  vlan-id?: number;
  // The VLAN protocol.
  vlan-protocol?: "802.1ad" | "802.1q";
  // Specify the raw interface for the vlan interface.
  vlan-raw-device?: string;
  // The VXLAN ID.
  vxlan-id?: number;
  // The VXLAN local tunnel IP.
  vxlan-local-tunnelip?: string;
  // The physical device for the VXLAN tunnel.
  vxlan-physdev?: string;
  // The VXLAN SVC node IP.
  vxlan-svcnodeip?: string;
}[];
```

## POST /api2/json/nodes/{node}/network

Create network device configuration

### Input Parameters

```ts
interface Params {
  // IP address.
  "address"?: string;
  // IP address.
  "address6"?: string;
  // Automatically start interface on boot.
  "autostart"?: boolean;
  // Specify the primary interface for active-backup bond.
  "bond-primary"?: string;
  // Bonding mode.
  "bond_mode"?: "balance-rr" | "active-backup" | "balance-xor" | "broadcast" | "802.3ad" | "balance-tlb" | "balance-alb" | "balance-slb" | "lacp-balance-slb" | "lacp-balance-tcp";
  // Selects the transmit hash policy to use for slave selection in balance-xor and 802.3ad modes.
  "bond_xmit_hash_policy"?: "layer2" | "layer2+3" | "layer3+4";
  // Specify the interfaces you want to add to your bridge.
  "bridge_ports"?: string;
  // Specify the allowed VLANs. For example: '2 4 100-200'. Only used if the bridge is VLAN aware.
  "bridge_vids"?: string;
  // Enable bridge vlan support.
  "bridge_vlan_aware"?: boolean;
  // IPv4 CIDR.
  "cidr"?: string;
  // IPv6 CIDR.
  "cidr6"?: string;
  // Comments
  "comments"?: string;
  // Comments
  "comments6"?: string;
  // Default gateway address.
  "gateway"?: string;
  // Default ipv6 gateway address.
  "gateway6"?: string;
  // Network interface name.
  "iface": string;
  // MTU.
  "mtu"?: number;
  // Network mask.
  "netmask"?: string;
  // Network mask.
  "netmask6"?: number;
  // The cluster node name.
  "node": string;
  // Specify the interfaces used by the bonding device.
  "ovs_bonds"?: string;
  // The OVS bridge associated with a OVS port. This is required when you create an OVS port.
  "ovs_bridge"?: string;
  // OVS interface options.
  "ovs_options"?: string;
  // Specify the interfaces you want to add to your bridge.
  "ovs_ports"?: string;
  // Specify a VLan tag (used by OVSPort, OVSIntPort, OVSBond)
  "ovs_tag"?: number;
  // Specify the interfaces used by the bonding device.
  "slaves"?: string;
  // Network interface type
  "type": "bridge" | "bond" | "eth" | "alias" | "vlan" | "OVSBridge" | "OVSBond" | "OVSPort" | "OVSIntPort" | "vnet" | "unknown";
  // vlan-id for a custom named vlan interface (ifupdown2 only).
  "vlan-id"?: number;
  // Specify the raw interface for the vlan interface.
  "vlan-raw-device"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/network

Reload network configuration

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/network/{iface}

Delete network device configuration

### Input Parameters

```ts
interface Params {
  // Network interface name.
  "iface": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/network/{iface}

Read network device configuration

### Input Parameters

```ts
interface Params {
  // Network interface name.
  "iface": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/network/{iface}

Update network device configuration

### Input Parameters

```ts
interface Params {
  // IP address.
  "address"?: string;
  // IP address.
  "address6"?: string;
  // Automatically start interface on boot.
  "autostart"?: boolean;
  // Specify the primary interface for active-backup bond.
  "bond-primary"?: string;
  // Bonding mode.
  "bond_mode"?: "balance-rr" | "active-backup" | "balance-xor" | "broadcast" | "802.3ad" | "balance-tlb" | "balance-alb" | "balance-slb" | "lacp-balance-slb" | "lacp-balance-tcp";
  // Selects the transmit hash policy to use for slave selection in balance-xor and 802.3ad modes.
  "bond_xmit_hash_policy"?: "layer2" | "layer2+3" | "layer3+4";
  // Specify the interfaces you want to add to your bridge.
  "bridge_ports"?: string;
  // Specify the allowed VLANs. For example: '2 4 100-200'. Only used if the bridge is VLAN aware.
  "bridge_vids"?: string;
  // Enable bridge vlan support.
  "bridge_vlan_aware"?: boolean;
  // IPv4 CIDR.
  "cidr"?: string;
  // IPv6 CIDR.
  "cidr6"?: string;
  // Comments
  "comments"?: string;
  // Comments
  "comments6"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Default gateway address.
  "gateway"?: string;
  // Default ipv6 gateway address.
  "gateway6"?: string;
  // Network interface name.
  "iface": string;
  // MTU.
  "mtu"?: number;
  // Network mask.
  "netmask"?: string;
  // Network mask.
  "netmask6"?: number;
  // The cluster node name.
  "node": string;
  // Specify the interfaces used by the bonding device.
  "ovs_bonds"?: string;
  // The OVS bridge associated with a OVS port. This is required when you create an OVS port.
  "ovs_bridge"?: string;
  // OVS interface options.
  "ovs_options"?: string;
  // Specify the interfaces you want to add to your bridge.
  "ovs_ports"?: string;
  // Specify a VLan tag (used by OVSPort, OVSIntPort, OVSBond)
  "ovs_tag"?: number;
  // Specify the interfaces used by the bonding device.
  "slaves"?: string;
  // Network interface type
  "type": "bridge" | "bond" | "eth" | "alias" | "vlan" | "OVSBridge" | "OVSBond" | "OVSPort" | "OVSIntPort" | "vnet" | "unknown";
  // vlan-id for a custom named vlan interface (ifupdown2 only).
  "vlan-id"?: number;
  // Specify the raw interface for the vlan interface.
  "vlan-raw-device"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/tasks

Read task list for one node (finished tasks).

### Input Parameters

```ts
interface Params {
  // Only list tasks with a status of ERROR.
  "errors"?: boolean;
  // Only list this amount of tasks.
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Only list tasks since this UNIX epoch.
  "since"?: number;
  // List archived, active or all tasks.
  "source"?: "archive" | "active" | "all";
  // List tasks beginning from this offset.
  "start"?: number;
  // List of Task States that should be returned.
  "statusfilter"?: string;
  // Only list tasks of this type (e.g., vzstart, vzdump).
  "typefilter"?: string;
  // Only list tasks until this UNIX epoch.
  "until"?: number;
  // Only list tasks from this user.
  "userfilter"?: string;
  // Only list tasks for this VM.
  "vmid"?: number;
}
```

### Returns

```ts
type Returns = {
  endtime?: number;
  id: string;
  node: string;
  pid: number;
  pstart: number;
  starttime: number;
  status?: string;
  type: string;
  upid: string;
  user: string;
}[];
```

## DELETE /api2/json/nodes/{node}/tasks/{upid}

Stop a task.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  "upid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/tasks/{upid}

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  "upid": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/tasks/{upid}/log

Read task log.

### Input Parameters

```ts
interface Params {
  // Whether the tasklog file should be downloaded. This parameter can't be used in conjunction with other parameters
  "download"?: boolean;
  // The amount of lines to read from the tasklog.
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Start at this line when reading the tasklog
  "start"?: number;
  // The task's unique ID.
  "upid": string;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/tasks/{upid}/status

Read task status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The task's unique ID.
  "upid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/scan

Index of available scan methods

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  method: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/nfs

Scan remote NFS server.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The server address (name or IP).
  "server": string;
}
```

### Returns

```ts
type Returns = {
  // NFS export options.
  options: string;
  // The exported path.
  path: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/cifs

Scan remote CIFS server.

### Input Parameters

```ts
interface Params {
  // SMB domain (Workgroup).
  "domain"?: string;
  // The cluster node name.
  "node": string;
  // User password.
  "password"?: string;
  // The server address (name or IP).
  "server": string;
  // User name.
  "username"?: string;
}
```

### Returns

```ts
type Returns = {
  // Descriptive text from server.
  description: string;
  // The cifs share name.
  share: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/pbs

Scan remote Proxmox Backup Server.

### Input Parameters

```ts
interface Params {
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  // The cluster node name.
  "node": string;
  // User password or API token secret.
  "password": string;
  // Optional port.
  "port"?: number;
  // The server address (name or IP).
  "server": string;
  // User-name or API token-ID.
  "username": string;
}
```

### Returns

```ts
type Returns = {
  // Comment from server.
  comment?: string;
  // The datastore name.
  store: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/glusterfs

Scan remote GlusterFS server.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The server address (name or IP).
  "server": string;
}
```

### Returns

```ts
type Returns = {
  // The volume name.
  volname: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/iscsi

Scan remote iSCSI server.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The iSCSI portal (IP or DNS name with optional port).
  "portal": string;
}
```

### Returns

```ts
type Returns = {
  // The iSCSI portal name.
  portal: string;
  // The iSCSI target name.
  target: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/lvm

List local LVM volume groups.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // The LVM logical volume group name.
  vg: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/lvmthin

List local LVM Thin Pools.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  "vg": string;
}
```

### Returns

```ts
type Returns = {
  // The LVM Thin Pool name (LVM logical volume).
  lv: string;
}[];
```

## GET /api2/json/nodes/{node}/scan/zfs

Scan zfs pool list on local node.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // ZFS pool name.
  pool: string;
}[];
```

## GET /api2/json/nodes/{node}/hardware

Index of hardware types

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  type: string;
}[];
```

## GET /api2/json/nodes/{node}/hardware/pci

List local PCI devices.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // A list of blacklisted PCI classes, which will not be returned. Following are filtered by default: Memory Controller (05), Bridge (06) and Processor (0b).
  "pci-class-blacklist"?: string;
  // If disabled, does only print the PCI IDs. Otherwise, additional information like vendor and device will be returned.
  "verbose"?: boolean;
}
```

### Returns

```ts
type Returns = {
  // The PCI Class of the device.
  class: string;
  // The Device ID.
  device: string;
  device_name?: string;
  // The PCI ID.
  id: string;
  // The IOMMU group in which the device is in. If no IOMMU group is detected, it is set to -1.
  iommugroup: number;
  // If set, marks that the device is capable of creating mediated devices.
  mdev?: boolean;
  // The Subsystem Device ID.
  subsystem_device?: string;
  subsystem_device_name?: string;
  // The Subsystem Vendor ID.
  subsystem_vendor?: string;
  subsystem_vendor_name?: string;
  // The Vendor ID.
  vendor: string;
  vendor_name?: string;
}[];
```

## GET /api2/json/nodes/{node}/hardware/pci/{pci-id-or-mapping}

Index of available pci methods

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  "pci-id-or-mapping": string;
}
```

### Returns

```ts
type Returns = {
  method: string;
}[];
```

## GET /api2/json/nodes/{node}/hardware/pci/{pci-id-or-mapping}/mdev

List mediated device types for given PCI device.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The PCI ID or mapping to list the mdev types for.
  "pci-id-or-mapping": string;
}
```

### Returns

```ts
type Returns = {
  // The number of still available instances of this type.
  available: number;
  // Additional description of the type.
  description: string;
  // A human readable name for the type.
  name?: string;
  // The name of the mdev type.
  type: string;
}[];
```

## GET /api2/json/nodes/{node}/hardware/usb

List local USB devices.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  busnum: number;
  class: number;
  devnum: number;
  level: number;
  manufacturer?: string;
  port: number;
  prodid: string;
  product?: string;
  serial?: string;
  speed: string;
  usbpath?: string;
  vendid: string;
}[];
```

## GET /api2/json/nodes/{node}/capabilities

Node capabilities index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/capabilities/qemu

QEMU capabilities index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/capabilities/qemu/cpu

List all custom and default CPU models.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // True if this is a custom CPU model.
  custom: boolean;
  // Name of the CPU model. Identifies it for subsequent API calls. Prefixed with 'custom-' for custom models.
  name: string;
  // CPU vendor visible to the guest when this model is selected. Vendor of 'reported-model' in case of custom models.
  vendor: string;
}[];
```

## GET /api2/json/nodes/{node}/capabilities/qemu/machines

Get available QEMU/KVM machine types.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // Notable changes of a version, currently only set for +pveX versions.
  changes?: string;
  // Full name of machine type and version.
  id: string;
  // The machine type.
  type: "q35" | "i440fx";
  // The machine version.
  version: string;
}[];
```

## GET /api2/json/nodes/{node}/storage

Get status for all datastores.

### Input Parameters

```ts
interface Params {
  // Only list stores which support this content type.
  "content"?: string;
  // Only list stores which are enabled (not disabled in config).
  "enabled"?: boolean;
  // Include information about formats
  "format"?: boolean;
  // The cluster node name.
  "node": string;
  // Only list status for  specified storage
  "storage"?: string;
  // If target is different to 'node', we only lists shared storages which content is accessible on this 'node' and the specified 'target' node.
  "target"?: string;
}
```

### Returns

```ts
type Returns = {
  // Set when storage is accessible.
  active?: boolean;
  // Available storage space in bytes.
  avail?: number;
  // Allowed storage content types.
  content: string;
  // Set when storage is enabled (not disabled).
  enabled?: boolean;
  // Shared flag from storage configuration.
  shared?: boolean;
  // The storage identifier.
  storage: string;
  // Total storage space in bytes.
  total?: number;
  // Storage type.
  type: string;
  // Used storage space in bytes.
  used?: number;
  // Used fraction (used/total).
  used_fraction?: number;
}[];
```

## GET /api2/json/nodes/{node}/storage/{storage}

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## DELETE /api2/json/nodes/{node}/storage/{storage}/prunebackups

Prune backups. Only those using the standard naming scheme are considered.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // The storage identifier.
  "storage": string;
  // Either 'qemu' or 'lxc'. Only consider backups for guests of this type.
  "type"?: "qemu" | "lxc";
  // Only prune backups for this VM.
  "vmid"?: number;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/storage/{storage}/prunebackups

Get prune information for backups. NOTE: this is only a preview and might not be what a subsequent prune call does if backups are removed/added in the meantime.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Use these retention options instead of those from the storage configuration.
  "prune-backups"?: string;
  // The storage identifier.
  "storage": string;
  // Either 'qemu' or 'lxc'. Only consider backups for guests of this type.
  "type"?: "qemu" | "lxc";
  // Only consider backups for this guest.
  "vmid"?: number;
}
```

### Returns

```ts
type Returns = {
  // Creation time of the backup (seconds since the UNIX epoch).
  ctime: number;
  // Whether the backup would be kept or removed. Backups that are protected or don't use the standard naming scheme are not removed.
  mark: "keep" | "remove" | "protected" | "renamed";
  // One of 'qemu', 'lxc', 'openvz' or 'unknown'.
  type: string;
  // The VM the backup belongs to.
  vmid?: number;
  // Backup volume ID.
  volid: string;
}[];
```

## GET /api2/json/nodes/{node}/storage/{storage}/content

List storage content.

### Input Parameters

```ts
interface Params {
  // Only list content of this type.
  "content"?: string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Only list images for this VM
  "vmid"?: number;
}
```

### Returns

```ts
type Returns = {
  // Creation time (seconds since the UNIX Epoch).
  ctime?: number;
  // If whole backup is encrypted, value is the fingerprint or '1'  if encrypted. Only useful for the Proxmox Backup Server storage type.
  encrypted?: string;
  // Format identifier ('raw', 'qcow2', 'subvol', 'iso', 'tgz' ...)
  format: string;
  // Optional notes. If they contain multiple lines, only the first one is returned here.
  notes?: string;
  // Volume identifier of parent (for linked cloned).
  parent?: string;
  // Protection status. Currently only supported for backups.
  protected?: boolean;
  // Volume size in bytes.
  size: number;
  // Used space. Please note that most storage plugins do not report anything useful here.
  used?: number;
  // Last backup verification result, only useful for PBS storages.
  verification?: any;
  // Associated Owner VMID.
  vmid?: number;
  // Volume identifier.
  volid: string;
}[];
```

## POST /api2/json/nodes/{node}/storage/{storage}/content

Allocate disk images.

### Input Parameters

```ts
interface Params {
  // The name of the file to create.
  "filename": string;
  // Format of the image.
  "format"?: "raw" | "qcow2" | "subvol" | "vmdk";
  // The cluster node name.
  "node": string;
  // Size in kilobyte (1024 bytes). Optional suffixes 'M' (megabyte, 1024K) and 'G' (gigabyte, 1024M)
  "size": string;
  // The storage identifier.
  "storage": string;
  // Specify owner VM
  "vmid": number;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/storage/{storage}/content/{volume}

Delete volume

### Input Parameters

```ts
interface Params {
  // Time to wait for the task to finish. We return 'null' if the task finish within that time.
  "delay"?: number;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage"?: string;
  // Volume identifier
  "volume": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/storage/{storage}/content/{volume}

Get volume attributes

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage"?: string;
  // Volume identifier
  "volume": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/storage/{storage}/content/{volume}

Copy a volume. This is experimental code - do not use.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage"?: string;
  // Target volume identifier
  "target": string;
  // Target node. Default is local node.
  "target_node"?: string;
  // Source volume identifier
  "volume": string;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/storage/{storage}/content/{volume}

Update volume attributes

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The new notes.
  "notes"?: string;
  // Protection status. Currently only supported for backups.
  "protected"?: boolean;
  // The storage identifier.
  "storage"?: string;
  // Volume identifier
  "volume": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/storage/{storage}/file-restore/list

List files and directories for single file restore under the given path.

### Input Parameters

```ts
interface Params {
  // base64-path to the directory or file being listed, or "/".
  "filepath": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Backup volume ID or name. Currently only PBS snapshots are supported.
  "volume": string;
}
```

### Returns

```ts
type Returns = {
  // base64 path of the current entry
  filepath: string;
  // If this entry is a leaf in the directory graph.
  leaf: boolean;
  // Entry last-modified time (unix timestamp).
  mtime?: number;
  // Entry file size.
  size?: number;
  // Entry display text.
  text: string;
  // Entry type.
  type: string;
}[];
```

## GET /api2/json/nodes/{node}/storage/{storage}/file-restore/download

Extract a file or directory (as zip archive) from a PBS backup.

### Input Parameters

```ts
interface Params {
  // base64-path to the directory or file to download.
  "filepath": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Download dirs as 'tar.zst' instead of 'zip'.
  "tar"?: boolean;
  // Backup volume ID or name. Currently only PBS snapshots are supported.
  "volume": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/storage/{storage}/status

Read storage status.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/storage/{storage}/rrd

Read storage RRD statistics (returns PNG).

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The list of datasources you want to display.
  "ds": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/storage/{storage}/rrddata

Read storage RRD statistics.

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/storage/{storage}/upload

Upload templates, ISO images, OVAs and VM images.

### Input Parameters

```ts
interface Params {
  // The expected checksum of the file.
  "checksum"?: string;
  // The algorithm to calculate the checksum of the file.
  "checksum-algorithm"?: "md5" | "sha1" | "sha224" | "sha256" | "sha384" | "sha512";
  // Content type.
  "content": "iso" | "vztmpl" | "import";
  // The name of the file to create. Caution: This will be normalized!
  "filename": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // The source file name. This parameter is usually set by the REST handler. You can only overwrite it when connecting to the trusted port on localhost.
  "tmpfilename"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/storage/{storage}/download-url

Download templates, ISO images, OVAs and VM images by using an URL.

### Input Parameters

```ts
interface Params {
  // The expected checksum of the file.
  "checksum"?: string;
  // The algorithm to calculate the checksum of the file.
  "checksum-algorithm"?: "md5" | "sha1" | "sha224" | "sha256" | "sha384" | "sha512";
  // Decompress the downloaded file using the specified compression algorithm.
  "compression"?: string;
  // Content type.
  "content": "iso" | "vztmpl" | "import";
  // The name of the file to create. Caution: This will be normalized!
  "filename": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // The URL to download the file from.
  "url": string;
  // If false, no SSL/TLS certificates will be verified.
  "verify-certificates"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/storage/{storage}/import-metadata

Get the base parameters for creating a guest which imports data from a foreign importable guest, like an ESXi VM

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "storage": string;
  // Volume identifier for the guest archive/entry.
  "volume": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/disks

Node index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/disks/lvm

List LVM Volume Groups

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/disks/lvm

Create an LVM Volume Group

### Input Parameters

```ts
interface Params {
  // Configure storage using the Volume Group
  "add_storage"?: boolean;
  // The block device you want to create the volume group on
  "device": string;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/disks/lvm/{name}

Remove an LVM Volume Group.

### Input Parameters

```ts
interface Params {
  // Marks associated storage(s) as not available on this node anymore or removes them from the configuration (if configured for this node only).
  "cleanup-config"?: boolean;
  // Also wipe disks so they can be repurposed afterwards.
  "cleanup-disks"?: boolean;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/disks/lvmthin

List LVM thinpools

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // The name of the thinpool.
  lv: string;
  // The size of the thinpool in bytes.
  lv_size: number;
  // The size of the metadata lv in bytes.
  metadata_size: number;
  // The used bytes of the metadata lv.
  metadata_used: number;
  // The used bytes of the thinpool.
  used: number;
  // The associated volume group.
  vg: string;
}[];
```

## POST /api2/json/nodes/{node}/disks/lvmthin

Create an LVM thinpool

### Input Parameters

```ts
interface Params {
  // Configure storage using the thinpool.
  "add_storage"?: boolean;
  // The block device you want to create the thinpool on.
  "device": string;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/disks/lvmthin/{name}

Remove an LVM thin pool.

### Input Parameters

```ts
interface Params {
  // Marks associated storage(s) as not available on this node anymore or removes them from the configuration (if configured for this node only).
  "cleanup-config"?: boolean;
  // Also wipe disks so they can be repurposed afterwards.
  "cleanup-disks"?: boolean;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
  // The storage identifier.
  "volume-group": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/disks/directory

PVE Managed Directory storages.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // The mounted device.
  device: string;
  // The mount options.
  options: string;
  // The mount path.
  path: string;
  // The filesystem type.
  type: string;
  // The path of the mount unit.
  unitfile: string;
}[];
```

## POST /api2/json/nodes/{node}/disks/directory

Create a Filesystem on an unused disk. Will be mounted under '/mnt/pve/NAME'.

### Input Parameters

```ts
interface Params {
  // Configure storage using the directory.
  "add_storage"?: boolean;
  // The block device you want to create the filesystem on.
  "device": string;
  // The desired filesystem.
  "filesystem"?: "ext4" | "xfs";
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/disks/directory/{name}

Unmounts the storage and removes the mount unit.

### Input Parameters

```ts
interface Params {
  // Marks associated storage(s) as not available on this node anymore or removes them from the configuration (if configured for this node only).
  "cleanup-config"?: boolean;
  // Also wipe disk so it can be repurposed afterwards.
  "cleanup-disks"?: boolean;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/disks/zfs

List Zpools.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  alloc: number;
  dedup: number;
  frag: number;
  free: number;
  health: string;
  name: string;
  size: number;
}[];
```

## POST /api2/json/nodes/{node}/disks/zfs

Create a ZFS pool.

### Input Parameters

```ts
interface Params {
  // Configure storage using the zpool.
  "add_storage"?: boolean;
  // Pool sector size exponent.
  "ashift"?: number;
  // The compression algorithm to use.
  "compression"?: "on" | "off" | "gzip" | "lz4" | "lzjb" | "zle" | "zstd";
  // The block devices you want to create the zpool on.
  "devices": string;
  "draid-config"?: string;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
  // The RAID level to use.
  "raidlevel": "single" | "mirror" | "raid10" | "raidz" | "raidz2" | "raidz3" | "draid" | "draid2" | "draid3";
}
```

### Returns

```ts
type Returns = string;
```

## DELETE /api2/json/nodes/{node}/disks/zfs/{name}

Destroy a ZFS pool.

### Input Parameters

```ts
interface Params {
  // Marks associated storage(s) as not available on this node anymore or removes them from the configuration (if configured for this node only).
  "cleanup-config"?: boolean;
  // Also wipe disks so they can be repurposed afterwards.
  "cleanup-disks"?: boolean;
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/disks/zfs/{name}

Get details about a zpool.

### Input Parameters

```ts
interface Params {
  // The storage identifier.
  "name": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/disks/list

List local disks.

### Input Parameters

```ts
interface Params {
  // Also include partitions.
  "include-partitions"?: boolean;
  // The cluster node name.
  "node": string;
  // Skip smart checks.
  "skipsmart"?: boolean;
  // Only list specific types of disks.
  "type"?: "unused" | "journal_disks";
}
```

### Returns

```ts
type Returns = {
  // The device path
  devpath: string;
  gpt: boolean;
  health?: string;
  model?: string;
  mounted: boolean;
  osdid: number;
  osdid-list: object[];
  // For partitions only. The device path of the disk the partition resides on.
  parent?: string;
  serial?: string;
  size: number;
  used?: string;
  vendor?: string;
  wwn?: string;
}[];
```

## GET /api2/json/nodes/{node}/disks/smart

Get SMART Health of a disk.

### Input Parameters

```ts
interface Params {
  // Block device name
  "disk": string;
  // If true returns only the health status
  "healthonly"?: boolean;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/disks/initgpt

Initialize Disk with GPT

### Input Parameters

```ts
interface Params {
  // Block device name
  "disk": string;
  // The cluster node name.
  "node": string;
  // UUID for the GPT table
  "uuid"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/disks/wipedisk

Wipe a disk or partition.

### Input Parameters

```ts
interface Params {
  // Block device name
  "disk": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/apt

Directory index for apt (Advanced Package Tool).

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  id: string;
}[];
```

## GET /api2/json/nodes/{node}/apt/update

List available updates.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/apt/update

This is used to resynchronize the package index files from their sources (apt-get update).

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Send notification about new packages.
  "notify"?: boolean;
  // Only produces output suitable for logging, omitting progress indicators.
  "quiet"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/apt/changelog

Get package changelogs.

### Input Parameters

```ts
interface Params {
  // Package name.
  "name": string;
  // The cluster node name.
  "node": string;
  // Package version.
  "version"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/apt/repositories

Get APT repository information.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/apt/repositories

Change the properties of a repository. Currently only allows enabling/disabling.

### Input Parameters

```ts
interface Params {
  // Digest to detect modifications.
  "digest"?: string;
  // Whether the repository should be enabled or not.
  "enabled"?: boolean;
  // Index within the file (starting from 0).
  "index": number;
  // The cluster node name.
  "node": string;
  // Path to the containing file.
  "path": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/apt/repositories

Add a standard repository to the configuration

### Input Parameters

```ts
interface Params {
  // Digest to detect modifications.
  "digest"?: string;
  // Handle that identifies a repository.
  "handle": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/apt/versions

Get package information for important Proxmox packages.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/firewall

Directory index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/firewall/rules

List rules.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  pos: number;
}[];
```

## POST /api2/json/nodes/{node}/firewall/rules

Create new rule.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action": string;
  // Descriptive comment.
  "comment"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type": "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/nodes/{node}/firewall/rules/{pos}

Delete rule.

### Input Parameters

```ts
interface Params {
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/firewall/rules/{pos}

Get single rule data.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/firewall/rules/{pos}

Modify rule data.

### Input Parameters

```ts
interface Params {
  // Rule action ('ACCEPT', 'DROP', 'REJECT') or security group name.
  "action"?: string;
  // Descriptive comment.
  "comment"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Restrict packet destination address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "dest"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Restrict TCP/UDP destination port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "dport"?: string;
  // Flag to enable/disable a rule.
  "enable"?: number;
  // Specify icmp-type. Only valid if proto equals 'icmp' or 'icmpv6'/'ipv6-icmp'.
  "icmp-type"?: string;
  // Network interface name. You have to use network configuration key names for VMs and containers ('net\d+'). Host related rules can use arbitrary strings.
  "iface"?: string;
  // Log level for firewall rule.
  "log"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Use predefined standard macro.
  "macro"?: string;
  // Move rule to new position <moveto>. Other arguments are ignored.
  "moveto"?: number;
  // The cluster node name.
  "node": string;
  // Update rule at position <pos>.
  "pos"?: number;
  // IP protocol. You can use protocol names ('tcp'/'udp') or simple numbers, as defined in '/etc/protocols'.
  "proto"?: string;
  // Restrict packet source address. This can refer to a single IP address, an IP set ('+ipsetname') or an IP alias definition. You can also specify an address range like '20.34.101.207-201.3.9.99', or a list of IP addresses and networks (entries are separated by comma). Please do not mix IPv4 and IPv6 addresses inside such lists.
  "source"?: string;
  // Restrict TCP/UDP source port. You can use service names or simple numbers (0-65535), as defined in '/etc/services'. Port ranges can be specified with '\d+:\d+', for example '80:85', and you can use comma separated list to match several ports or ranges.
  "sport"?: string;
  // Rule type.
  "type"?: "in" | "out" | "forward" | "group";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/firewall/options

Get host firewall options.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/firewall/options

Set Firewall options.

### Input Parameters

```ts
interface Params {
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Enable host firewall rules.
  "enable"?: boolean;
  // Log level for forwarded traffic.
  "log_level_forward"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Log level for incoming traffic.
  "log_level_in"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Log level for outgoing traffic.
  "log_level_out"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Enable logging of conntrack information.
  "log_nf_conntrack"?: boolean;
  // Enable NDP (Neighbor Discovery Protocol).
  "ndp"?: boolean;
  // Allow invalid packets on connection tracking.
  "nf_conntrack_allow_invalid"?: boolean;
  // Enable conntrack helpers for specific protocols. Supported protocols: amanda, ftp, irc, netbios-ns, pptp, sane, sip, snmp, tftp
  "nf_conntrack_helpers"?: string;
  // Maximum number of tracked connections.
  "nf_conntrack_max"?: number;
  // Conntrack established timeout.
  "nf_conntrack_tcp_timeout_established"?: number;
  // Conntrack syn recv timeout.
  "nf_conntrack_tcp_timeout_syn_recv"?: number;
  // Enable nftables based firewall (tech preview)
  "nftables"?: boolean;
  // The cluster node name.
  "node": string;
  // Enable SMURFS filter.
  "nosmurfs"?: boolean;
  // Enable synflood protection
  "protection_synflood"?: boolean;
  // Synflood protection rate burst by ip src.
  "protection_synflood_burst"?: number;
  // Synflood protection rate syn/sec by ip src.
  "protection_synflood_rate"?: number;
  // Log level for SMURFS filter.
  "smurf_log_level"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Log level for illegal tcp flags filter.
  "tcp_flags_log_level"?: "emerg" | "alert" | "crit" | "err" | "warning" | "notice" | "info" | "debug" | "nolog";
  // Filter illegal combinations of TCP flags.
  "tcpflags"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/firewall/log

Read firewall log

### Input Parameters

```ts
interface Params {
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Display log since this UNIX epoch.
  "since"?: number;
  "start"?: number;
  // Display log until this UNIX epoch.
  "until"?: number;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/replication

List status of all replication jobs on this node.

### Input Parameters

```ts
interface Params {
  // Only list replication jobs for this guest.
  "guest"?: number;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  id: string;
}[];
```

## GET /api2/json/nodes/{node}/replication/{id}

Directory index.

### Input Parameters

```ts
interface Params {
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/replication/{id}/status

Get replication job status.

### Input Parameters

```ts
interface Params {
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/replication/{id}/log

Read replication job log.

### Input Parameters

```ts
interface Params {
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  "limit"?: number;
  // The cluster node name.
  "node": string;
  "start"?: number;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## POST /api2/json/nodes/{node}/replication/{id}/schedule_now

Schedule replication job to start as soon as possible.

### Input Parameters

```ts
interface Params {
  // Replication Job ID. The ID is composed of a Guest ID and a job number, separated by a hyphen, i.e. '<GUEST>-<JOBNUM>'.
  "id": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/certificates

Node index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/certificates/acme

ACME index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## DELETE /api2/json/nodes/{node}/certificates/acme/certificate

Revoke existing certificate from CA.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/certificates/acme/certificate

Order a new certificate from ACME-compatible CA.

### Input Parameters

```ts
interface Params {
  // Overwrite existing custom certificate.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## PUT /api2/json/nodes/{node}/certificates/acme/certificate

Renew existing certificate from CA.

### Input Parameters

```ts
interface Params {
  // Force renewal even if expiry is more than 30 days away.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/certificates/info

Get information about node's certificates.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  filename?: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  // Certificate issuer name.
  issuer?: string;
  // Certificate's notAfter timestamp (UNIX epoch).
  notafter?: number;
  // Certificate's notBefore timestamp (UNIX epoch).
  notbefore?: number;
  // Certificate in PEM format
  pem?: string;
  // Certificate's public key size
  public-key-bits?: number;
  // Certificate's public key algorithm
  public-key-type?: string;
  // List of Certificate's SubjectAlternativeName entries.
  san?: object[];
  // Certificate subject name.
  subject?: string;
}[];
```

## DELETE /api2/json/nodes/{node}/certificates/custom

DELETE custom certificate chain and key.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Restart pveproxy.
  "restart"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/certificates/custom

Upload or update custom certificate chain and key.

### Input Parameters

```ts
interface Params {
  // PEM encoded certificate (chain).
  "certificates": string;
  // Overwrite existing custom or ACME certificate files.
  "force"?: boolean;
  // PEM encoded private key.
  "key"?: string;
  // The cluster node name.
  "node": string;
  // Restart pveproxy.
  "restart"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/config

Get node configuration options.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Return only a specific property from the node configuration.
  "property"?: "acme" | "acmedomain0" | "acmedomain1" | "acmedomain2" | "acmedomain3" | "acmedomain4" | "acmedomain5" | "ballooning-target" | "description" | "startall-onboot-delay" | "wakeonlan";
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/config

Set node configuration options.

### Input Parameters

```ts
interface Params {
  // Node specific ACME settings.
  "acme"?: string;
  // ACME domain and validation plugin
  "acmedomain[n]"?: string;
  // RAM usage target for ballooning (in percent of total memory)
  "ballooning-target"?: number;
  // A list of settings you want to delete.
  "delete"?: string;
  // Description for the Node. Shown in the web-interface node notes panel. This is saved as comment inside the configuration file.
  "description"?: string;
  // Prevent changes if current configuration file has different SHA1 digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
  // Initial delay in seconds, before starting all the Virtual Guests with on-boot enabled.
  "startall-onboot-delay"?: number;
  // Node specific wake on LAN settings.
  "wakeonlan"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/sdn

SDN index.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/sdn/zones

Get status for all zones.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = {
  // Status of zone
  status: "available" | "pending" | "error";
  // The SDN zone object identifier.
  zone: string;
}[];
```

## GET /api2/json/nodes/{node}/sdn/zones/{zone}

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The SDN zone object identifier.
  "zone": string;
}
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/nodes/{node}/sdn/zones/{zone}/content

List zone content.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The SDN zone object identifier.
  "zone": string;
}
```

### Returns

```ts
type Returns = {
  // Status.
  status?: string;
  // Status details
  statusmsg?: string;
  // Vnet identifier.
  vnet: string;
}[];
```

## GET /api2/json/nodes/{node}/version

API version details

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/status

Read node status

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/status

Reboot or shutdown a node.

### Input Parameters

```ts
interface Params {
  // Specify the command.
  "command": "reboot" | "shutdown";
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/netstat

Read tap/vm network device interface counters

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/execute

Execute multiple commands in order, root only.

### Input Parameters

```ts
interface Params {
  // JSON encoded array of commands.
  "commands": string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/wakeonlan

Try to wake a node via 'wake on LAN' network packet.

### Input Parameters

```ts
interface Params {
  // target node for wake on LAN packet
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/rrd

Read node RRD statistics (returns PNG)

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The list of datasources you want to display.
  "ds": string;
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/rrddata

Read node RRD statistics

### Input Parameters

```ts
interface Params {
  // The RRD consolidation function
  "cf"?: "AVERAGE" | "MAX";
  // The cluster node name.
  "node": string;
  // Specify the time frame you are interested in.
  "timeframe": "hour" | "day" | "week" | "month" | "year";
}
```

### Returns

```ts
type Returns = any[];
```

## GET /api2/json/nodes/{node}/syslog

Read system log

### Input Parameters

```ts
interface Params {
  "limit"?: number;
  // The cluster node name.
  "node": string;
  // Service ID
  "service"?: string;
  // Display all log since this date-time string.
  "since"?: string;
  "start"?: number;
  // Display all log until this date-time string.
  "until"?: string;
}
```

### Returns

```ts
type Returns = {
  // Line number
  n: number;
  // Line text
  t: string;
}[];
```

## GET /api2/json/nodes/{node}/journal

Read Journal

### Input Parameters

```ts
interface Params {
  // End before the given Cursor. Conflicts with 'until'
  "endcursor"?: string;
  // Limit to the last X lines. Conflicts with a range.
  "lastentries"?: number;
  // The cluster node name.
  "node": string;
  // Display all log since this UNIX epoch. Conflicts with 'startcursor'.
  "since"?: number;
  // Start after the given Cursor. Conflicts with 'since'
  "startcursor"?: string;
  // Display all log until this UNIX epoch. Conflicts with 'endcursor'.
  "until"?: number;
}
```

### Returns

```ts
type Returns = object[];
```

## POST /api2/json/nodes/{node}/vncshell

Creates a VNC Shell proxy.

### Input Parameters

```ts
interface Params {
  // Run specific command or default to login (requires 'root@pam')
  "cmd"?: "ceph_install" | "upgrade" | "login";
  // Add parameters to a command. Encoded as null terminated strings.
  "cmd-opts"?: string;
  // sets the height of the console in pixels.
  "height"?: number;
  // The cluster node name.
  "node": string;
  // use websocket instead of standard vnc.
  "websocket"?: boolean;
  // sets the width of the console in pixels.
  "width"?: number;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/termproxy

Creates a VNC Shell proxy.

### Input Parameters

```ts
interface Params {
  // Run specific command or default to login (requires 'root@pam')
  "cmd"?: "ceph_install" | "upgrade" | "login";
  // Add parameters to a command. Encoded as null terminated strings.
  "cmd-opts"?: string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/vncwebsocket

Opens a websocket for VNC traffic.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Port number returned by previous vncproxy call.
  "port": number;
  // Ticket from previous call to vncproxy.
  "vncticket": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/spiceshell

Creates a SPICE shell.

### Input Parameters

```ts
interface Params {
  // Run specific command or default to login (requires 'root@pam')
  "cmd"?: "ceph_install" | "upgrade" | "login";
  // Add parameters to a command. Encoded as null terminated strings.
  "cmd-opts"?: string;
  // The cluster node name.
  "node": string;
  // SPICE proxy server. This can be used by the client to specify the proxy server. All nodes in a cluster runs 'spiceproxy', so it is up to the client to choose one. By default, we return the node where the VM is currently running. As reasonable setting is to use same node you use to connect to the API (This is window.location.hostname for the JS GUI).
  "proxy"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/dns

Read DNS settings.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/dns

Write DNS settings.

### Input Parameters

```ts
interface Params {
  // First name server IP address.
  "dns1"?: string;
  // Second name server IP address.
  "dns2"?: string;
  // Third name server IP address.
  "dns3"?: string;
  // The cluster node name.
  "node": string;
  // Search domain for host-name lookup.
  "search": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/time

Read server time and time zone settings.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/nodes/{node}/time

Set time zone.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Time zone. The file '/usr/share/zoneinfo/zone.tab' contains the list of valid names.
  "timezone": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/aplinfo

Get list of appliances.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any[];
```

## POST /api2/json/nodes/{node}/aplinfo

Download appliance templates.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The storage where the template will be stored
  "storage": string;
  // The template which will downloaded
  "template": string;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/query-url-metadata

Query metadata of an URL: file size, file name and mime type.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // The URL to query the metadata from.
  "url": string;
  // If false, no SSL/TLS certificates will be verified.
  "verify-certificates"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/nodes/{node}/report

Gather various systems information about a node

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/startall

Start all VMs and containers located on this node (by default only those with onboot=1).

### Input Parameters

```ts
interface Params {
  // Issue start command even if virtual guest have 'onboot' not set or set to off.
  "force"?: boolean;
  // The cluster node name.
  "node": string;
  // Only consider guests from this comma separated list of VMIDs.
  "vms"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/stopall

Stop all VMs and Containers.

### Input Parameters

```ts
interface Params {
  // Force a hard-stop after the timeout.
  "force-stop"?: boolean;
  // The cluster node name.
  "node": string;
  // Timeout for each guest shutdown task. Depending on `force-stop`, the shutdown gets then simply aborted or a hard-stop is forced.
  "timeout"?: number;
  // Only consider Guests with these IDs.
  "vms"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/suspendall

Suspend all VMs.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
  // Only consider Guests with these IDs.
  "vms"?: string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/nodes/{node}/migrateall

Migrate all VMs and Containers.

### Input Parameters

```ts
interface Params {
  // Maximal number of parallel migration job. If not set, uses'max_workers' from datacenter.cfg. One of both must be set!
  "maxworkers"?: number;
  // The cluster node name.
  "node": string;
  // Target node.
  "target": string;
  // Only consider Guests with these IDs.
  "vms"?: string;
  // Enable live storage migration for local disk
  "with-local-disks"?: boolean;
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/nodes/{node}/hosts

Get the content of /etc/hosts.

### Input Parameters

```ts
interface Params {
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/nodes/{node}/hosts

Write /etc/hosts.

### Input Parameters

```ts
interface Params {
  // The target content of /etc/hosts.
  "data": string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // The cluster node name.
  "node": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/storage

Storage index.

### Input Parameters

```ts
interface Params {
  // Only list storage of specific type
  "type"?: "btrfs" | "cephfs" | "cifs" | "dir" | "esxi" | "glusterfs" | "iscsi" | "iscsidirect" | "lvm" | "lvmthin" | "nfs" | "pbs" | "rbd" | "zfs" | "zfspool";
}
```

### Returns

```ts
type Returns = {
  storage: string;
}[];
```

## POST /api2/json/storage

Create a new storage.

### Input Parameters

```ts
interface Params {
  // Authsupported.
  "authsupported"?: string;
  // Base volume. This volume is automatically activated.
  "base"?: string;
  // block size
  "blocksize"?: string;
  // Set I/O bandwidth limit for various operations (in KiB/s).
  "bwlimit"?: string;
  // host group for comstar views
  "comstar_hg"?: string;
  // target group for comstar views
  "comstar_tg"?: string;
  // Allowed content types.  NOTE: the value 'rootdir' is used for Containers, and value 'images' for VMs. 
  "content"?: string;
  // Overrides for default content type directories.
  "content-dirs"?: string;
  // Create the base directory if it doesn't exist.
  "create-base-path"?: boolean;
  // Populate the directory with the default structure.
  "create-subdirs"?: boolean;
  // Data Pool (for erasure coding only)
  "data-pool"?: string;
  // Proxmox Backup Server datastore name.
  "datastore"?: string;
  // Flag to disable the storage.
  "disable"?: boolean;
  // CIFS domain.
  "domain"?: string;
  // Encryption key. Use 'autogen' to generate one automatically without passphrase.
  "encryption-key"?: string;
  // NFS export path.
  "export"?: string;
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  // Default image format.
  "format"?: "raw" | "qcow2" | "subvol" | "vmdk";
  // The Ceph filesystem name.
  "fs-name"?: string;
  // Mount CephFS through FUSE.
  "fuse"?: boolean;
  // Assume the given path is an externally managed mountpoint and consider the storage offline if it is not mounted. Using a boolean (yes/no) value serves as a shortcut to using the target path in this field.
  "is_mountpoint"?: string;
  // iscsi provider
  "iscsiprovider"?: string;
  // Client keyring contents (for external clusters).
  "keyring"?: string;
  // Always access rbd through krbd kernel module.
  "krbd"?: boolean;
  // target portal group for Linux LIO targets
  "lio_tpg"?: string;
  // Base64-encoded, PEM-formatted public RSA key. Used to encrypt a copy of the encryption-key which will be added to each encrypted backup.
  "master-pubkey"?: string;
  // Maximal number of protected backups per guest. Use '-1' for unlimited.
  "max-protected-backups"?: number;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per VM. Use '0' for unlimited.
  "maxfiles"?: number;
  // Create the directory if it doesn't exist and populate it with default sub-dirs. NOTE: Deprecated, use the 'create-base-path' and 'create-subdirs' options instead.
  "mkdir"?: boolean;
  // IP addresses of monitors (for external clusters).
  "monhost"?: string;
  // mount point
  "mountpoint"?: string;
  // Namespace.
  "namespace"?: string;
  // Set the NOCOW flag on files. Disables data checksumming and causes data errors to be unrecoverable from while allowing direct I/O. Only use this if data does not need to be any more safe than on a single ext4 formatted disk with no underlying raid system.
  "nocow"?: boolean;
  // List of nodes for which the storage configuration applies.
  "nodes"?: string;
  // disable write caching on the target
  "nowritecache"?: boolean;
  // NFS/CIFS mount options (see 'man nfs' or 'man mount.cifs')
  "options"?: string;
  // Password for accessing the share/datastore.
  "password"?: string;
  // File system path.
  "path"?: string;
  // Pool.
  "pool"?: string;
  // Use this port to connect to the storage instead of the default one (for example, with PBS or ESXi). For NFS and CIFS, use the 'options' option to configure the port via the mount options.
  "port"?: number;
  // iSCSI portal (IP or DNS name with optional port).
  "portal"?: string;
  // Preallocation mode for raw and qcow2 images. Using 'metadata' on raw images results in preallocation=off.
  "preallocation"?: "off" | "metadata" | "falloc" | "full";
  // The retention options with shorter intervals are processed first with --keep-last being the very first one. Each option covers a specific period of time. We say that backups within this period are covered by this option. The next option does not take care of already covered backups and only considers older backups.
  "prune-backups"?: string;
  // Zero-out data when removing LVs.
  "saferemove"?: boolean;
  // Wipe throughput (cstream -t parameter value).
  "saferemove_throughput"?: string;
  // Server IP or DNS name.
  "server"?: string;
  // Backup volfile server IP or DNS name.
  "server2"?: string;
  // CIFS share.
  "share"?: string;
  // Indicate that this is a single storage with the same contents on all nodes (or all listed in the 'nodes' option). It will not make the contents of a local storage automatically accessible to other nodes, it just marks an already shared storage as such!
  "shared"?: boolean;
  // Disable TLS certificate verification, only enable on fully trusted networks!
  "skip-cert-verification"?: boolean;
  // SMB protocol version. 'default' if not set, negotiates the highest SMB2+ version supported by both the client and server.
  "smbversion"?: "default" | "2.0" | "2.1" | "3" | "3.0" | "3.11";
  // use sparse volumes
  "sparse"?: boolean;
  // The storage identifier.
  "storage": string;
  // Subdir to mount.
  "subdir"?: string;
  // Only use logical volumes tagged with 'pve-vm-ID'.
  "tagged_only"?: boolean;
  // iSCSI target.
  "target"?: string;
  // LVM thin pool LV name.
  "thinpool"?: string;
  // Gluster transport: tcp or rdma
  "transport"?: "tcp" | "rdma" | "unix";
  // Storage type.
  "type": "btrfs" | "cephfs" | "cifs" | "dir" | "esxi" | "glusterfs" | "iscsi" | "iscsidirect" | "lvm" | "lvmthin" | "nfs" | "pbs" | "rbd" | "zfs" | "zfspool";
  // RBD Id.
  "username"?: string;
  // Volume group name.
  "vgname"?: string;
  // Glusterfs Volume.
  "volume"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/storage/{storage}

Delete storage configuration.

### Input Parameters

```ts
interface Params {
  // The storage identifier.
  "storage": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/storage/{storage}

Read storage configuration.

### Input Parameters

```ts
interface Params {
  // The storage identifier.
  "storage": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/storage/{storage}

Update storage configuration.

### Input Parameters

```ts
interface Params {
  // block size
  "blocksize"?: string;
  // Set I/O bandwidth limit for various operations (in KiB/s).
  "bwlimit"?: string;
  // host group for comstar views
  "comstar_hg"?: string;
  // target group for comstar views
  "comstar_tg"?: string;
  // Allowed content types.  NOTE: the value 'rootdir' is used for Containers, and value 'images' for VMs. 
  "content"?: string;
  // Overrides for default content type directories.
  "content-dirs"?: string;
  // Create the base directory if it doesn't exist.
  "create-base-path"?: boolean;
  // Populate the directory with the default structure.
  "create-subdirs"?: boolean;
  // Data Pool (for erasure coding only)
  "data-pool"?: string;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // Flag to disable the storage.
  "disable"?: boolean;
  // CIFS domain.
  "domain"?: string;
  // Encryption key. Use 'autogen' to generate one automatically without passphrase.
  "encryption-key"?: string;
  // Certificate SHA 256 fingerprint.
  "fingerprint"?: string;
  // Default image format.
  "format"?: "raw" | "qcow2" | "subvol" | "vmdk";
  // The Ceph filesystem name.
  "fs-name"?: string;
  // Mount CephFS through FUSE.
  "fuse"?: boolean;
  // Assume the given path is an externally managed mountpoint and consider the storage offline if it is not mounted. Using a boolean (yes/no) value serves as a shortcut to using the target path in this field.
  "is_mountpoint"?: string;
  // Client keyring contents (for external clusters).
  "keyring"?: string;
  // Always access rbd through krbd kernel module.
  "krbd"?: boolean;
  // target portal group for Linux LIO targets
  "lio_tpg"?: string;
  // Base64-encoded, PEM-formatted public RSA key. Used to encrypt a copy of the encryption-key which will be added to each encrypted backup.
  "master-pubkey"?: string;
  // Maximal number of protected backups per guest. Use '-1' for unlimited.
  "max-protected-backups"?: number;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per VM. Use '0' for unlimited.
  "maxfiles"?: number;
  // Create the directory if it doesn't exist and populate it with default sub-dirs. NOTE: Deprecated, use the 'create-base-path' and 'create-subdirs' options instead.
  "mkdir"?: boolean;
  // IP addresses of monitors (for external clusters).
  "monhost"?: string;
  // mount point
  "mountpoint"?: string;
  // Namespace.
  "namespace"?: string;
  // Set the NOCOW flag on files. Disables data checksumming and causes data errors to be unrecoverable from while allowing direct I/O. Only use this if data does not need to be any more safe than on a single ext4 formatted disk with no underlying raid system.
  "nocow"?: boolean;
  // List of nodes for which the storage configuration applies.
  "nodes"?: string;
  // disable write caching on the target
  "nowritecache"?: boolean;
  // NFS/CIFS mount options (see 'man nfs' or 'man mount.cifs')
  "options"?: string;
  // Password for accessing the share/datastore.
  "password"?: string;
  // Pool.
  "pool"?: string;
  // Use this port to connect to the storage instead of the default one (for example, with PBS or ESXi). For NFS and CIFS, use the 'options' option to configure the port via the mount options.
  "port"?: number;
  // Preallocation mode for raw and qcow2 images. Using 'metadata' on raw images results in preallocation=off.
  "preallocation"?: "off" | "metadata" | "falloc" | "full";
  // The retention options with shorter intervals are processed first with --keep-last being the very first one. Each option covers a specific period of time. We say that backups within this period are covered by this option. The next option does not take care of already covered backups and only considers older backups.
  "prune-backups"?: string;
  // Zero-out data when removing LVs.
  "saferemove"?: boolean;
  // Wipe throughput (cstream -t parameter value).
  "saferemove_throughput"?: string;
  // Server IP or DNS name.
  "server"?: string;
  // Backup volfile server IP or DNS name.
  "server2"?: string;
  // Indicate that this is a single storage with the same contents on all nodes (or all listed in the 'nodes' option). It will not make the contents of a local storage automatically accessible to other nodes, it just marks an already shared storage as such!
  "shared"?: boolean;
  // Disable TLS certificate verification, only enable on fully trusted networks!
  "skip-cert-verification"?: boolean;
  // SMB protocol version. 'default' if not set, negotiates the highest SMB2+ version supported by both the client and server.
  "smbversion"?: "default" | "2.0" | "2.1" | "3" | "3.0" | "3.11";
  // use sparse volumes
  "sparse"?: boolean;
  // The storage identifier.
  "storage": string;
  // Subdir to mount.
  "subdir"?: string;
  // Only use logical volumes tagged with 'pve-vm-ID'.
  "tagged_only"?: boolean;
  // Gluster transport: tcp or rdma
  "transport"?: "tcp" | "rdma" | "unix";
  // RBD Id.
  "username"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## GET /api2/json/access/users

User index.

### Input Parameters

```ts
interface Params {
  // Optional filter for enable property.
  "enabled"?: boolean;
  // Include group and token information.
  "full"?: boolean;
}
```

### Returns

```ts
type Returns = {
  comment?: string;
  email?: string;
  // Enable the account (default). You can set this to '0' to disable the account
  enable?: boolean;
  // Account expiration date (seconds since epoch). '0' means no expiration date.
  expire?: number;
  firstname?: string;
  groups?: string;
  // Keys for two factor auth (yubico).
  keys?: string;
  lastname?: string;
  // The type of the users realm
  realm-type?: string;
  // Contains a timestamp until when a user is locked out of 2nd factors.
  tfa-locked-until?: number;
  tokens?: {
  comment?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  expire?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  privsep?: boolean;
  // User-specific token identifier.
  tokenid: string;
}[];
  // True if the user is currently locked out of TOTP factors.
  totp-locked?: boolean;
  // Full User ID, in the `name@realm` format.
  userid: string;
}[];
```

## POST /api2/json/access/users

Create new user.

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  "email"?: string;
  // Enable the account (default). You can set this to '0' to disable the account
  "enable"?: boolean;
  // Account expiration date (seconds since epoch). '0' means no expiration date.
  "expire"?: number;
  "firstname"?: string;
  "groups"?: string;
  // Keys for two factor auth (yubico).
  "keys"?: string;
  "lastname"?: string;
  // Initial password.
  "password"?: string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/access/users/{userid}

Delete user.

### Input Parameters

```ts
interface Params {
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/users/{userid}

Get user configuration.

### Input Parameters

```ts
interface Params {
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/users/{userid}

Update user configuration.

### Input Parameters

```ts
interface Params {
  "append"?: boolean;
  "comment"?: string;
  "email"?: string;
  // Enable the account (default). You can set this to '0' to disable the account
  "enable"?: boolean;
  // Account expiration date (seconds since epoch). '0' means no expiration date.
  "expire"?: number;
  "firstname"?: string;
  "groups"?: string;
  // Keys for two factor auth (yubico).
  "keys"?: string;
  "lastname"?: string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/users/{userid}/tfa

Get user TFA types (Personal and Realm).

### Input Parameters

```ts
interface Params {
  // Request all entries as an array.
  "multiple"?: boolean;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/users/{userid}/unlock-tfa

Unlock a user's TFA authentication.

### Input Parameters

```ts
interface Params {
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = boolean;
```

## GET /api2/json/access/users/{userid}/token

Get user API tokens.

### Input Parameters

```ts
interface Params {
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = {
  comment?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  expire?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  privsep?: boolean;
  // User-specific token identifier.
  tokenid: string;
}[];
```

## DELETE /api2/json/access/users/{userid}/token/{tokenid}

Remove API token for a specific user.

### Input Parameters

```ts
interface Params {
  // User-specific token identifier.
  "tokenid": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/users/{userid}/token/{tokenid}

Get specific API token information.

### Input Parameters

```ts
interface Params {
  // User-specific token identifier.
  "tokenid": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/access/users/{userid}/token/{tokenid}

Generate a new API token for a specific user. NOTE: returns API token value, which needs to be stored as it cannot be retrieved afterwards!

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  "expire"?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  "privsep"?: boolean;
  // User-specific token identifier.
  "tokenid": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/users/{userid}/token/{tokenid}

Update API token for a specific user.

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  "expire"?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  "privsep"?: boolean;
  // User-specific token identifier.
  "tokenid": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/groups

Group index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  comment?: string;
  groupid: string;
  // list of users which form this group
  users?: string;
}[];
```

## POST /api2/json/access/groups

Create new group.

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  "groupid": string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/access/groups/{groupid}

Delete group.

### Input Parameters

```ts
interface Params {
  "groupid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/groups/{groupid}

Get group configuration.

### Input Parameters

```ts
interface Params {
  "groupid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/groups/{groupid}

Update group data.

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  "groupid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/roles

Role index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  privs?: string;
  roleid: string;
  special?: boolean;
}[];
```

## POST /api2/json/access/roles

Create new role.

### Input Parameters

```ts
interface Params {
  "privs"?: string;
  "roleid": string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/access/roles/{roleid}

Delete role.

### Input Parameters

```ts
interface Params {
  "roleid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/roles/{roleid}

Get role configuration.

### Input Parameters

```ts
interface Params {
  "roleid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/roles/{roleid}

Update an existing role.

### Input Parameters

```ts
interface Params {
  "append"?: boolean;
  "privs"?: string;
  "roleid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/acl

Get Access Control List (ACLs).

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // Access control path
  path: string;
  // Allow to propagate (inherit) permissions.
  propagate?: boolean;
  roleid: string;
  type: "user" | "group" | "token";
  ugid: string;
}[];
```

## PUT /api2/json/access/acl

Update Access Control List (add or remove permissions).

### Input Parameters

```ts
interface Params {
  // Remove permissions (instead of adding it).
  "delete"?: boolean;
  // List of groups.
  "groups"?: string;
  // Access control path
  "path": string;
  // Allow to propagate (inherit) permissions.
  "propagate"?: boolean;
  // List of roles.
  "roles": string;
  // List of API tokens.
  "tokens"?: string;
  // List of users.
  "users"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/domains

Authentication domain index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  // A comment. The GUI use this text when you select a domain (Realm) on the login window.
  comment?: string;
  realm: string;
  // Two-factor authentication provider.
  tfa?: "yubico" | "oath";
  type: string;
}[];
```

## POST /api2/json/access/domains

Add an authentication server.

### Input Parameters

```ts
interface Params {
  // Specifies the Authentication Context Class Reference values that theAuthorization Server is being requested to use for the Auth Request.
  "acr-values"?: string;
  // Automatically create users if they do not exist.
  "autocreate"?: boolean;
  // LDAP base domain name
  "base_dn"?: string;
  // LDAP bind domain name
  "bind_dn"?: string;
  // Path to the CA certificate store
  "capath"?: string;
  // username is case-sensitive
  "case-sensitive"?: boolean;
  // Path to the client certificate
  "cert"?: string;
  // Path to the client certificate key
  "certkey"?: string;
  // Check bind connection to the server.
  "check-connection"?: boolean;
  // OpenID Client ID
  "client-id"?: string;
  // OpenID Client Key
  "client-key"?: string;
  // Description.
  "comment"?: string;
  // Use this as default realm
  "default"?: boolean;
  // AD domain name
  "domain"?: string;
  // LDAP filter for user sync.
  "filter"?: string;
  // The objectclasses for groups.
  "group_classes"?: string;
  // LDAP base domain name for group sync. If not set, the base_dn will be used.
  "group_dn"?: string;
  // LDAP filter for group sync.
  "group_filter"?: string;
  // LDAP attribute representing a groups name. If not set or found, the first value of the DN will be used as name.
  "group_name_attr"?: string;
  // Automatically create groups if they do not exist.
  "groups-autocreate"?: boolean;
  // OpenID claim used to retrieve groups with.
  "groups-claim"?: string;
  // All groups will be overwritten for the user on login.
  "groups-overwrite"?: boolean;
  // OpenID Issuer Url
  "issuer-url"?: string;
  // LDAP protocol mode.
  "mode"?: "ldap" | "ldaps" | "ldap+starttls";
  // LDAP bind password. Will be stored in '/etc/pve/priv/realm/<REALM>.pw'.
  "password"?: string;
  // Server port.
  "port"?: number;
  // Specifies whether the Authorization Server prompts the End-User for reauthentication and consent.
  "prompt"?: string;
  // Enables querying the userinfo endpoint for claims values.
  "query-userinfo"?: boolean;
  // Authentication domain ID
  "realm": string;
  // Specifies the scopes (user details) that should be authorized and returned, for example 'email' or 'profile'.
  "scopes"?: string;
  // Use secure LDAPS protocol. DEPRECATED: use 'mode' instead.
  "secure"?: boolean;
  // Server IP address (or DNS name)
  "server1"?: string;
  // Fallback Server IP address (or DNS name)
  "server2"?: string;
  // LDAPS TLS/SSL version. It's not recommended to use version older than 1.2!
  "sslversion"?: "tlsv1" | "tlsv1_1" | "tlsv1_2" | "tlsv1_3";
  // The default options for behavior of synchronizations.
  "sync-defaults-options"?: string;
  // Comma separated list of key=value pairs for specifying which LDAP attributes map to which PVE user field. For example, to map the LDAP attribute 'mail' to PVEs 'email', write  'email=mail'. By default, each PVE user field is represented  by an LDAP attribute of the same name.
  "sync_attributes"?: string;
  // Use Two-factor authentication.
  "tfa"?: string;
  // Realm type.
  "type": "ad" | "ldap" | "openid" | "pam" | "pve";
  // LDAP user attribute name
  "user_attr"?: string;
  // The objectclasses for users.
  "user_classes"?: string;
  // OpenID claim used to generate the unique username.
  "username-claim"?: string;
  // Verify the server's SSL certificate
  "verify"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/access/domains/{realm}

Delete an authentication server.

### Input Parameters

```ts
interface Params {
  // Authentication domain ID
  "realm": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/domains/{realm}

Get auth server configuration.

### Input Parameters

```ts
interface Params {
  // Authentication domain ID
  "realm": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/domains/{realm}

Update authentication server settings.

### Input Parameters

```ts
interface Params {
  // Specifies the Authentication Context Class Reference values that theAuthorization Server is being requested to use for the Auth Request.
  "acr-values"?: string;
  // Automatically create users if they do not exist.
  "autocreate"?: boolean;
  // LDAP base domain name
  "base_dn"?: string;
  // LDAP bind domain name
  "bind_dn"?: string;
  // Path to the CA certificate store
  "capath"?: string;
  // username is case-sensitive
  "case-sensitive"?: boolean;
  // Path to the client certificate
  "cert"?: string;
  // Path to the client certificate key
  "certkey"?: string;
  // Check bind connection to the server.
  "check-connection"?: boolean;
  // OpenID Client ID
  "client-id"?: string;
  // OpenID Client Key
  "client-key"?: string;
  // Description.
  "comment"?: string;
  // Use this as default realm
  "default"?: boolean;
  // A list of settings you want to delete.
  "delete"?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  "digest"?: string;
  // AD domain name
  "domain"?: string;
  // LDAP filter for user sync.
  "filter"?: string;
  // The objectclasses for groups.
  "group_classes"?: string;
  // LDAP base domain name for group sync. If not set, the base_dn will be used.
  "group_dn"?: string;
  // LDAP filter for group sync.
  "group_filter"?: string;
  // LDAP attribute representing a groups name. If not set or found, the first value of the DN will be used as name.
  "group_name_attr"?: string;
  // Automatically create groups if they do not exist.
  "groups-autocreate"?: boolean;
  // OpenID claim used to retrieve groups with.
  "groups-claim"?: string;
  // All groups will be overwritten for the user on login.
  "groups-overwrite"?: boolean;
  // OpenID Issuer Url
  "issuer-url"?: string;
  // LDAP protocol mode.
  "mode"?: "ldap" | "ldaps" | "ldap+starttls";
  // LDAP bind password. Will be stored in '/etc/pve/priv/realm/<REALM>.pw'.
  "password"?: string;
  // Server port.
  "port"?: number;
  // Specifies whether the Authorization Server prompts the End-User for reauthentication and consent.
  "prompt"?: string;
  // Enables querying the userinfo endpoint for claims values.
  "query-userinfo"?: boolean;
  // Authentication domain ID
  "realm": string;
  // Specifies the scopes (user details) that should be authorized and returned, for example 'email' or 'profile'.
  "scopes"?: string;
  // Use secure LDAPS protocol. DEPRECATED: use 'mode' instead.
  "secure"?: boolean;
  // Server IP address (or DNS name)
  "server1"?: string;
  // Fallback Server IP address (or DNS name)
  "server2"?: string;
  // LDAPS TLS/SSL version. It's not recommended to use version older than 1.2!
  "sslversion"?: "tlsv1" | "tlsv1_1" | "tlsv1_2" | "tlsv1_3";
  // The default options for behavior of synchronizations.
  "sync-defaults-options"?: string;
  // Comma separated list of key=value pairs for specifying which LDAP attributes map to which PVE user field. For example, to map the LDAP attribute 'mail' to PVEs 'email', write  'email=mail'. By default, each PVE user field is represented  by an LDAP attribute of the same name.
  "sync_attributes"?: string;
  // Use Two-factor authentication.
  "tfa"?: string;
  // LDAP user attribute name
  "user_attr"?: string;
  // The objectclasses for users.
  "user_classes"?: string;
  // Verify the server's SSL certificate
  "verify"?: boolean;
}
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/access/domains/{realm}/sync

Syncs users and/or groups from the configured LDAP to user.cfg. NOTE: Synced groups will have the name 'name-$realm', so make sure those groups do not exist to prevent overwriting.

### Input Parameters

```ts
interface Params {
  // If set, does not write anything.
  "dry-run"?: boolean;
  // Enable newly synced users immediately.
  "enable-new"?: boolean;
  // DEPRECATED: use 'remove-vanished' instead. If set, uses the LDAP Directory as source of truth, deleting users or groups not returned from the sync and removing all locally modified properties of synced users. If not set, only syncs information which is present in the synced data, and does not delete or modify anything else.
  "full"?: boolean;
  // DEPRECATED: use 'remove-vanished' instead. Remove ACLs for users or groups which were removed from the config during a sync.
  "purge"?: boolean;
  // Authentication domain ID
  "realm": string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Select what to sync.
  "scope"?: "users" | "groups" | "both";
}
```

### Returns

```ts
type Returns = string;
```

## GET /api2/json/access/openid

Directory index.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  subdir: string;
}[];
```

## POST /api2/json/access/openid/auth-url

Get the OpenId Authorization Url for the specified realm.

### Input Parameters

```ts
interface Params {
  // Authentication domain ID
  "realm": string;
  // Redirection Url. The client should set this to the used server url (location.origin).
  "redirect-url": string;
}
```

### Returns

```ts
type Returns = string;
```

## POST /api2/json/access/openid/login

 Verify OpenID authorization code and create a ticket.

### Input Parameters

```ts
interface Params {
  // OpenId authorization code.
  "code": string;
  // Redirection Url. The client should set this to the used server url (location.origin).
  "redirect-url": string;
  // OpenId state.
  "state": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/tfa

List TFA configurations of users.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = {
  entries: {
  // Creation time of this entry as unix epoch.
  created: number;
  // User chosen description for this entry.
  description: string;
  // Whether this TFA entry is currently enabled.
  enable?: boolean;
  // The id used to reference this entry.
  id: string;
  // TFA Entry Type.
  type: "totp" | "u2f" | "webauthn" | "recovery" | "yubico";
}[];
  // Contains a timestamp until when a user is locked out of 2nd factors.
  tfa-locked-until?: number;
  // True if the user is currently locked out of TOTP factors.
  totp-locked?: boolean;
  // User this entry belongs to.
  userid: string;
}[];
```

## GET /api2/json/access/tfa/{userid}

List TFA configurations of users.

### Input Parameters

```ts
interface Params {
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = {
  // Creation time of this entry as unix epoch.
  created: number;
  // User chosen description for this entry.
  description: string;
  // Whether this TFA entry is currently enabled.
  enable?: boolean;
  // The id used to reference this entry.
  id: string;
  // TFA Entry Type.
  type: "totp" | "u2f" | "webauthn" | "recovery" | "yubico";
}[];
```

## POST /api2/json/access/tfa/{userid}

Add a TFA entry for a user.

### Input Parameters

```ts
interface Params {
  // When responding to a u2f challenge: the original challenge string
  "challenge"?: string;
  // A description to distinguish multiple entries from one another
  "description"?: string;
  // The current password of the user performing the change.
  "password"?: string;
  // A totp URI.
  "totp"?: string;
  // TFA Entry Type.
  "type": "totp" | "u2f" | "webauthn" | "recovery" | "yubico";
  // Full User ID, in the `name@realm` format.
  "userid": string;
  // The current value for the provided totp URI, or a Webauthn/U2F challenge response
  "value"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/access/tfa/{userid}/{id}

Delete a TFA entry by ID.

### Input Parameters

```ts
interface Params {
  // A TFA entry id.
  "id": string;
  // The current password of the user performing the change.
  "password"?: string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/tfa/{userid}/{id}

Fetch a requested TFA entry if present.

### Input Parameters

```ts
interface Params {
  // A TFA entry id.
  "id": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/tfa/{userid}/{id}

Add a TFA entry for a user.

### Input Parameters

```ts
interface Params {
  // A description to distinguish multiple entries from one another
  "description"?: string;
  // Whether the entry should be enabled for login.
  "enable"?: boolean;
  // A TFA entry id.
  "id": string;
  // The current password of the user performing the change.
  "password"?: string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/ticket

Dummy. Useful for formatters which want to provide a login page.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

## POST /api2/json/access/ticket

Create or verify authentication ticket.

### Input Parameters

```ts
interface Params {
  // This parameter is now ignored and assumed to be 1.
  "new-format"?: boolean;
  // One-time password for Two-factor authentication.
  "otp"?: string;
  // The secret password. This can also be a valid ticket.
  "password": string;
  // Verify ticket, and check if user have access 'privs' on 'path'
  "path"?: string;
  // Verify ticket, and check if user have access 'privs' on 'path'
  "privs"?: string;
  // You can optionally pass the realm using this parameter. Normally the realm is simply added to the username <username>@<realm>.
  "realm"?: string;
  // The signed TFA challenge string the user wants to respond to.
  "tfa-challenge"?: string;
  // User name
  "username": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/access/password

Change user password.

### Input Parameters

```ts
interface Params {
  // The current password of the user performing the change.
  "confirmation-password"?: string;
  // The new password.
  "password": string;
  // Full User ID, in the `name@realm` format.
  "userid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/access/permissions

Retrieve effective permissions of given user/token.

### Input Parameters

```ts
interface Params {
  // Only dump this specific path, not the whole tree.
  "path"?: string;
  // User ID or full API token ID
  "userid"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/pools

Delete pool.

### Input Parameters

```ts
interface Params {
  "poolid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/pools

List pools or get pool configuration.

### Input Parameters

```ts
interface Params {
  "poolid"?: string;
  "type"?: "qemu" | "lxc" | "storage";
}
```

### Returns

```ts
type Returns = {
  comment?: string;
  members?: {
  id: string;
  node: string;
  storage?: string;
  type: "qemu" | "lxc" | "openvz" | "storage";
  vmid?: number;
}[];
  poolid: string;
}[];
```

## POST /api2/json/pools

Create new pool.

### Input Parameters

```ts
interface Params {
  "comment"?: string;
  "poolid": string;
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/pools

Update pool.

### Input Parameters

```ts
interface Params {
  // Allow adding a guest even if already in another pool. The guest will be removed from its current pool and added to this one.
  "allow-move"?: boolean;
  "comment"?: string;
  // Remove the passed VMIDs and/or storage IDs instead of adding them.
  "delete"?: boolean;
  "poolid": string;
  // List of storage IDs to add or remove from this pool.
  "storage"?: string;
  // List of guest VMIDs to add or remove from this pool.
  "vms"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## DELETE /api2/json/pools/{poolid}

Delete pool (deprecated, no support for nested pools, use 'DELETE /pools/?poolid={poolid}').

### Input Parameters

```ts
interface Params {
  "poolid": string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/pools/{poolid}

Get pool configuration (deprecated, no support for nested pools, use 'GET /pools/?poolid={poolid}').

### Input Parameters

```ts
interface Params {
  "poolid": string;
  "type"?: "qemu" | "lxc" | "storage";
}
```

### Returns

```ts
type Returns = any;
```

## PUT /api2/json/pools/{poolid}

Update pool data (deprecated, no support for nested pools - use 'PUT /pools/?poolid={poolid}' instead).

### Input Parameters

```ts
interface Params {
  // Allow adding a guest even if already in another pool. The guest will be removed from its current pool and added to this one.
  "allow-move"?: boolean;
  "comment"?: string;
  // Remove the passed VMIDs and/or storage IDs instead of adding them.
  "delete"?: boolean;
  "poolid": string;
  // List of storage IDs to add or remove from this pool.
  "storage"?: string;
  // List of guest VMIDs to add or remove from this pool.
  "vms"?: string;
}
```

### Returns

```ts
type Returns = any;
```

## GET /api2/json/version

API version details, including some parts of the global datacenter config.

### Input Parameters

```ts
type Params = void;
```

### Returns

```ts
type Returns = any;
```

