# /access endpoints

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
  enabled?: boolean;
  // Include group and token information.
  full?: boolean;
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
  // Initial password.
  password?: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  userid: string;
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
  userid: string;
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
  append?: boolean;
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
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  multiple?: boolean;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  userid: string;
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
  userid: string;
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
  tokenid: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  tokenid: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  comment?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  expire?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  privsep?: boolean;
  // User-specific token identifier.
  tokenid: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  comment?: string;
  // API token expiration date (seconds since epoch). '0' means no expiration date.
  expire?: number;
  // Restrict API token privileges with separate ACLs (default), or give full privileges of corresponding user.
  privsep?: boolean;
  // User-specific token identifier.
  tokenid: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  comment?: string;
  groupid: string;
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
  groupid: string;
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
  groupid: string;
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
  comment?: string;
  groupid: string;
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
  privs?: string;
  roleid: string;
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
  roleid: string;
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
  roleid: string;
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
  append?: boolean;
  privs?: string;
  roleid: string;
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
  delete?: boolean;
  // List of groups.
  groups?: string;
  // Access control path
  path: string;
  // Allow to propagate (inherit) permissions.
  propagate?: boolean;
  // List of roles.
  roles: string;
  // List of API tokens.
  tokens?: string;
  // List of users.
  users?: string;
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
  autocreate?: boolean;
  // LDAP base domain name
  base_dn?: string;
  // LDAP bind domain name
  bind_dn?: string;
  // Path to the CA certificate store
  capath?: string;
  // username is case-sensitive
  "case-sensitive"?: boolean;
  // Path to the client certificate
  cert?: string;
  // Path to the client certificate key
  certkey?: string;
  // Check bind connection to the server.
  "check-connection"?: boolean;
  // OpenID Client ID
  "client-id"?: string;
  // OpenID Client Key
  "client-key"?: string;
  // Description.
  comment?: string;
  // Use this as default realm
  default?: boolean;
  // AD domain name
  domain?: string;
  // LDAP filter for user sync.
  filter?: string;
  // The objectclasses for groups.
  group_classes?: string;
  // LDAP base domain name for group sync. If not set, the base_dn will be used.
  group_dn?: string;
  // LDAP filter for group sync.
  group_filter?: string;
  // LDAP attribute representing a groups name. If not set or found, the first value of the DN will be used as name.
  group_name_attr?: string;
  // Automatically create groups if they do not exist.
  "groups-autocreate"?: boolean;
  // OpenID claim used to retrieve groups with.
  "groups-claim"?: string;
  // All groups will be overwritten for the user on login.
  "groups-overwrite"?: boolean;
  // OpenID Issuer Url
  "issuer-url"?: string;
  // LDAP protocol mode.
  mode?: "ldap" | "ldaps" | "ldap+starttls";
  // LDAP bind password. Will be stored in '/etc/pve/priv/realm/<REALM>.pw'.
  password?: string;
  // Server port.
  port?: number;
  // Specifies whether the Authorization Server prompts the End-User for reauthentication and consent.
  prompt?: string;
  // Enables querying the userinfo endpoint for claims values.
  "query-userinfo"?: boolean;
  // Authentication domain ID
  realm: string;
  // Specifies the scopes (user details) that should be authorized and returned, for example 'email' or 'profile'.
  scopes?: string;
  // Use secure LDAPS protocol. DEPRECATED: use 'mode' instead.
  secure?: boolean;
  // Server IP address (or DNS name)
  server1?: string;
  // Fallback Server IP address (or DNS name)
  server2?: string;
  // LDAPS TLS/SSL version. It's not recommended to use version older than 1.2!
  sslversion?: "tlsv1" | "tlsv1_1" | "tlsv1_2" | "tlsv1_3";
  // The default options for behavior of synchronizations.
  "sync-defaults-options"?: string;
  // Comma separated list of key=value pairs for specifying which LDAP attributes map to which PVE user field. For example, to map the LDAP attribute 'mail' to PVEs 'email', write  'email=mail'. By default, each PVE user field is represented  by an LDAP attribute of the same name.
  sync_attributes?: string;
  // Use Two-factor authentication.
  tfa?: string;
  // Realm type.
  type: "ad" | "ldap" | "openid" | "pam" | "pve";
  // LDAP user attribute name
  user_attr?: string;
  // The objectclasses for users.
  user_classes?: string;
  // OpenID claim used to generate the unique username.
  "username-claim"?: string;
  // Verify the server's SSL certificate
  verify?: boolean;
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
  realm: string;
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
  realm: string;
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
  autocreate?: boolean;
  // LDAP base domain name
  base_dn?: string;
  // LDAP bind domain name
  bind_dn?: string;
  // Path to the CA certificate store
  capath?: string;
  // username is case-sensitive
  "case-sensitive"?: boolean;
  // Path to the client certificate
  cert?: string;
  // Path to the client certificate key
  certkey?: string;
  // Check bind connection to the server.
  "check-connection"?: boolean;
  // OpenID Client ID
  "client-id"?: string;
  // OpenID Client Key
  "client-key"?: string;
  // Description.
  comment?: string;
  // Use this as default realm
  default?: boolean;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // AD domain name
  domain?: string;
  // LDAP filter for user sync.
  filter?: string;
  // The objectclasses for groups.
  group_classes?: string;
  // LDAP base domain name for group sync. If not set, the base_dn will be used.
  group_dn?: string;
  // LDAP filter for group sync.
  group_filter?: string;
  // LDAP attribute representing a groups name. If not set or found, the first value of the DN will be used as name.
  group_name_attr?: string;
  // Automatically create groups if they do not exist.
  "groups-autocreate"?: boolean;
  // OpenID claim used to retrieve groups with.
  "groups-claim"?: string;
  // All groups will be overwritten for the user on login.
  "groups-overwrite"?: boolean;
  // OpenID Issuer Url
  "issuer-url"?: string;
  // LDAP protocol mode.
  mode?: "ldap" | "ldaps" | "ldap+starttls";
  // LDAP bind password. Will be stored in '/etc/pve/priv/realm/<REALM>.pw'.
  password?: string;
  // Server port.
  port?: number;
  // Specifies whether the Authorization Server prompts the End-User for reauthentication and consent.
  prompt?: string;
  // Enables querying the userinfo endpoint for claims values.
  "query-userinfo"?: boolean;
  // Authentication domain ID
  realm: string;
  // Specifies the scopes (user details) that should be authorized and returned, for example 'email' or 'profile'.
  scopes?: string;
  // Use secure LDAPS protocol. DEPRECATED: use 'mode' instead.
  secure?: boolean;
  // Server IP address (or DNS name)
  server1?: string;
  // Fallback Server IP address (or DNS name)
  server2?: string;
  // LDAPS TLS/SSL version. It's not recommended to use version older than 1.2!
  sslversion?: "tlsv1" | "tlsv1_1" | "tlsv1_2" | "tlsv1_3";
  // The default options for behavior of synchronizations.
  "sync-defaults-options"?: string;
  // Comma separated list of key=value pairs for specifying which LDAP attributes map to which PVE user field. For example, to map the LDAP attribute 'mail' to PVEs 'email', write  'email=mail'. By default, each PVE user field is represented  by an LDAP attribute of the same name.
  sync_attributes?: string;
  // Use Two-factor authentication.
  tfa?: string;
  // LDAP user attribute name
  user_attr?: string;
  // The objectclasses for users.
  user_classes?: string;
  // Verify the server's SSL certificate
  verify?: boolean;
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
  full?: boolean;
  // DEPRECATED: use 'remove-vanished' instead. Remove ACLs for users or groups which were removed from the config during a sync.
  purge?: boolean;
  // Authentication domain ID
  realm: string;
  // A semicolon-separated list of things to remove when they or the user vanishes during a sync. The following values are possible: 'entry' removes the user/group when not returned from the sync. 'properties' removes the set properties on existing user/group that do not appear in the source (even custom ones). 'acl' removes acls when the user/group is not returned from the sync. Instead of a list it also can be 'none' (the default).
  "remove-vanished"?: string;
  // Select what to sync.
  scope?: "users" | "groups" | "both";
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
  realm: string;
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
  code: string;
  // Redirection Url. The client should set this to the used server url (location.origin).
  "redirect-url": string;
  // OpenId state.
  state: string;
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
  userid: string;
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
  challenge?: string;
  // A description to distinguish multiple entries from one another
  description?: string;
  // The current password of the user performing the change.
  password?: string;
  // A totp URI.
  totp?: string;
  // TFA Entry Type.
  type: "totp" | "u2f" | "webauthn" | "recovery" | "yubico";
  // Full User ID, in the `name@realm` format.
  userid: string;
  // The current value for the provided totp URI, or a Webauthn/U2F challenge response
  value?: string;
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
  id: string;
  // The current password of the user performing the change.
  password?: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  id: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  description?: string;
  // Whether the entry should be enabled for login.
  enable?: boolean;
  // A TFA entry id.
  id: string;
  // The current password of the user performing the change.
  password?: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  otp?: string;
  // The secret password. This can also be a valid ticket.
  password: string;
  // Verify ticket, and check if user have access 'privs' on 'path'
  path?: string;
  // Verify ticket, and check if user have access 'privs' on 'path'
  privs?: string;
  // You can optionally pass the realm using this parameter. Normally the realm is simply added to the username <username>@<realm>.
  realm?: string;
  // The signed TFA challenge string the user wants to respond to.
  "tfa-challenge"?: string;
  // User name
  username: string;
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
  password: string;
  // Full User ID, in the `name@realm` format.
  userid: string;
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
  path?: string;
  // User ID or full API token ID
  userid?: string;
}
```

### Returns

```ts
type Returns = any;
```
