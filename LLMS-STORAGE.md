# /storage endpoints

## GET /api2/json/storage

Storage index.

### Input Parameters

```ts
interface Params {
  // Only list storage of specific type
  type?:
    | "btrfs"
    | "cephfs"
    | "cifs"
    | "dir"
    | "esxi"
    | "glusterfs"
    | "iscsi"
    | "iscsidirect"
    | "lvm"
    | "lvmthin"
    | "nfs"
    | "pbs"
    | "rbd"
    | "zfs"
    | "zfspool";
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
  authsupported?: string;
  // Base volume. This volume is automatically activated.
  base?: string;
  // block size
  blocksize?: string;
  // Set I/O bandwidth limit for various operations (in KiB/s).
  bwlimit?: string;
  // host group for comstar views
  comstar_hg?: string;
  // target group for comstar views
  comstar_tg?: string;
  // Allowed content types.  NOTE: the value 'rootdir' is used for Containers, and value 'images' for VMs.
  content?: string;
  // Overrides for default content type directories.
  "content-dirs"?: string;
  // Create the base directory if it doesn't exist.
  "create-base-path"?: boolean;
  // Populate the directory with the default structure.
  "create-subdirs"?: boolean;
  // Data Pool (for erasure coding only)
  "data-pool"?: string;
  // Proxmox Backup Server datastore name.
  datastore?: string;
  // Flag to disable the storage.
  disable?: boolean;
  // CIFS domain.
  domain?: string;
  // Encryption key. Use 'autogen' to generate one automatically without passphrase.
  "encryption-key"?: string;
  // NFS export path.
  export?: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  // Default image format.
  format?: "raw" | "qcow2" | "subvol" | "vmdk";
  // The Ceph filesystem name.
  "fs-name"?: string;
  // Mount CephFS through FUSE.
  fuse?: boolean;
  // Assume the given path is an externally managed mountpoint and consider the storage offline if it is not mounted. Using a boolean (yes/no) value serves as a shortcut to using the target path in this field.
  is_mountpoint?: string;
  // iscsi provider
  iscsiprovider?: string;
  // Client keyring contents (for external clusters).
  keyring?: string;
  // Always access rbd through krbd kernel module.
  krbd?: boolean;
  // target portal group for Linux LIO targets
  lio_tpg?: string;
  // Base64-encoded, PEM-formatted public RSA key. Used to encrypt a copy of the encryption-key which will be added to each encrypted backup.
  "master-pubkey"?: string;
  // Maximal number of protected backups per guest. Use '-1' for unlimited.
  "max-protected-backups"?: number;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per VM. Use '0' for unlimited.
  maxfiles?: number;
  // Create the directory if it doesn't exist and populate it with default sub-dirs. NOTE: Deprecated, use the 'create-base-path' and 'create-subdirs' options instead.
  mkdir?: boolean;
  // IP addresses of monitors (for external clusters).
  monhost?: string;
  // mount point
  mountpoint?: string;
  // Namespace.
  namespace?: string;
  // Set the NOCOW flag on files. Disables data checksumming and causes data errors to be unrecoverable from while allowing direct I/O. Only use this if data does not need to be any more safe than on a single ext4 formatted disk with no underlying raid system.
  nocow?: boolean;
  // List of nodes for which the storage configuration applies.
  nodes?: string;
  // disable write caching on the target
  nowritecache?: boolean;
  // NFS/CIFS mount options (see 'man nfs' or 'man mount.cifs')
  options?: string;
  // Password for accessing the share/datastore.
  password?: string;
  // File system path.
  path?: string;
  // Pool.
  pool?: string;
  // Use this port to connect to the storage instead of the default one (for example, with PBS or ESXi). For NFS and CIFS, use the 'options' option to configure the port via the mount options.
  port?: number;
  // iSCSI portal (IP or DNS name with optional port).
  portal?: string;
  // Preallocation mode for raw and qcow2 images. Using 'metadata' on raw images results in preallocation=off.
  preallocation?: "off" | "metadata" | "falloc" | "full";
  // The retention options with shorter intervals are processed first with --keep-last being the very first one. Each option covers a specific period of time. We say that backups within this period are covered by this option. The next option does not take care of already covered backups and only considers older backups.
  "prune-backups"?: string;
  // Zero-out data when removing LVs.
  saferemove?: boolean;
  // Wipe throughput (cstream -t parameter value).
  saferemove_throughput?: string;
  // Server IP or DNS name.
  server?: string;
  // Backup volfile server IP or DNS name.
  server2?: string;
  // CIFS share.
  share?: string;
  // Indicate that this is a single storage with the same contents on all nodes (or all listed in the 'nodes' option). It will not make the contents of a local storage automatically accessible to other nodes, it just marks an already shared storage as such!
  shared?: boolean;
  // Disable TLS certificate verification, only enable on fully trusted networks!
  "skip-cert-verification"?: boolean;
  // SMB protocol version. 'default' if not set, negotiates the highest SMB2+ version supported by both the client and server.
  smbversion?: "default" | "2.0" | "2.1" | "3" | "3.0" | "3.11";
  // use sparse volumes
  sparse?: boolean;
  // The storage identifier.
  storage: string;
  // Subdir to mount.
  subdir?: string;
  // Only use logical volumes tagged with 'pve-vm-ID'.
  tagged_only?: boolean;
  // iSCSI target.
  target?: string;
  // LVM thin pool LV name.
  thinpool?: string;
  // Gluster transport: tcp or rdma
  transport?: "tcp" | "rdma" | "unix";
  // Storage type.
  type:
    | "btrfs"
    | "cephfs"
    | "cifs"
    | "dir"
    | "esxi"
    | "glusterfs"
    | "iscsi"
    | "iscsidirect"
    | "lvm"
    | "lvmthin"
    | "nfs"
    | "pbs"
    | "rbd"
    | "zfs"
    | "zfspool";
  // RBD Id.
  username?: string;
  // Volume group name.
  vgname?: string;
  // Glusterfs Volume.
  volume?: string;
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
  storage: string;
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
  storage: string;
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
  blocksize?: string;
  // Set I/O bandwidth limit for various operations (in KiB/s).
  bwlimit?: string;
  // host group for comstar views
  comstar_hg?: string;
  // target group for comstar views
  comstar_tg?: string;
  // Allowed content types.  NOTE: the value 'rootdir' is used for Containers, and value 'images' for VMs.
  content?: string;
  // Overrides for default content type directories.
  "content-dirs"?: string;
  // Create the base directory if it doesn't exist.
  "create-base-path"?: boolean;
  // Populate the directory with the default structure.
  "create-subdirs"?: boolean;
  // Data Pool (for erasure coding only)
  "data-pool"?: string;
  // A list of settings you want to delete.
  delete?: string;
  // Prevent changes if current configuration file has a different digest. This can be used to prevent concurrent modifications.
  digest?: string;
  // Flag to disable the storage.
  disable?: boolean;
  // CIFS domain.
  domain?: string;
  // Encryption key. Use 'autogen' to generate one automatically without passphrase.
  "encryption-key"?: string;
  // Certificate SHA 256 fingerprint.
  fingerprint?: string;
  // Default image format.
  format?: "raw" | "qcow2" | "subvol" | "vmdk";
  // The Ceph filesystem name.
  "fs-name"?: string;
  // Mount CephFS through FUSE.
  fuse?: boolean;
  // Assume the given path is an externally managed mountpoint and consider the storage offline if it is not mounted. Using a boolean (yes/no) value serves as a shortcut to using the target path in this field.
  is_mountpoint?: string;
  // Client keyring contents (for external clusters).
  keyring?: string;
  // Always access rbd through krbd kernel module.
  krbd?: boolean;
  // target portal group for Linux LIO targets
  lio_tpg?: string;
  // Base64-encoded, PEM-formatted public RSA key. Used to encrypt a copy of the encryption-key which will be added to each encrypted backup.
  "master-pubkey"?: string;
  // Maximal number of protected backups per guest. Use '-1' for unlimited.
  "max-protected-backups"?: number;
  // Deprecated: use 'prune-backups' instead. Maximal number of backup files per VM. Use '0' for unlimited.
  maxfiles?: number;
  // Create the directory if it doesn't exist and populate it with default sub-dirs. NOTE: Deprecated, use the 'create-base-path' and 'create-subdirs' options instead.
  mkdir?: boolean;
  // IP addresses of monitors (for external clusters).
  monhost?: string;
  // mount point
  mountpoint?: string;
  // Namespace.
  namespace?: string;
  // Set the NOCOW flag on files. Disables data checksumming and causes data errors to be unrecoverable from while allowing direct I/O. Only use this if data does not need to be any more safe than on a single ext4 formatted disk with no underlying raid system.
  nocow?: boolean;
  // List of nodes for which the storage configuration applies.
  nodes?: string;
  // disable write caching on the target
  nowritecache?: boolean;
  // NFS/CIFS mount options (see 'man nfs' or 'man mount.cifs')
  options?: string;
  // Password for accessing the share/datastore.
  password?: string;
  // Pool.
  pool?: string;
  // Use this port to connect to the storage instead of the default one (for example, with PBS or ESXi). For NFS and CIFS, use the 'options' option to configure the port via the mount options.
  port?: number;
  // Preallocation mode for raw and qcow2 images. Using 'metadata' on raw images results in preallocation=off.
  preallocation?: "off" | "metadata" | "falloc" | "full";
  // The retention options with shorter intervals are processed first with --keep-last being the very first one. Each option covers a specific period of time. We say that backups within this period are covered by this option. The next option does not take care of already covered backups and only considers older backups.
  "prune-backups"?: string;
  // Zero-out data when removing LVs.
  saferemove?: boolean;
  // Wipe throughput (cstream -t parameter value).
  saferemove_throughput?: string;
  // Server IP or DNS name.
  server?: string;
  // Backup volfile server IP or DNS name.
  server2?: string;
  // Indicate that this is a single storage with the same contents on all nodes (or all listed in the 'nodes' option). It will not make the contents of a local storage automatically accessible to other nodes, it just marks an already shared storage as such!
  shared?: boolean;
  // Disable TLS certificate verification, only enable on fully trusted networks!
  "skip-cert-verification"?: boolean;
  // SMB protocol version. 'default' if not set, negotiates the highest SMB2+ version supported by both the client and server.
  smbversion?: "default" | "2.0" | "2.1" | "3" | "3.0" | "3.11";
  // use sparse volumes
  sparse?: boolean;
  // The storage identifier.
  storage: string;
  // Subdir to mount.
  subdir?: string;
  // Only use logical volumes tagged with 'pve-vm-ID'.
  tagged_only?: boolean;
  // Gluster transport: tcp or rdma
  transport?: "tcp" | "rdma" | "unix";
  // RBD Id.
  username?: string;
}
```

### Returns

```ts
type Returns = any;
```
