# /pools endpoints

## DELETE /api2/json/pools

Delete pool.

### Input Parameters

```ts
interface Params {
  poolid: string;
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
  poolid?: string;
  type?: "qemu" | "lxc" | "storage";
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
  comment?: string;
  poolid: string;
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
  comment?: string;
  // Remove the passed VMIDs and/or storage IDs instead of adding them.
  delete?: boolean;
  poolid: string;
  // List of storage IDs to add or remove from this pool.
  storage?: string;
  // List of guest VMIDs to add or remove from this pool.
  vms?: string;
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
  poolid: string;
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
  poolid: string;
  type?: "qemu" | "lxc" | "storage";
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
  comment?: string;
  // Remove the passed VMIDs and/or storage IDs instead of adding them.
  delete?: boolean;
  poolid: string;
  // List of storage IDs to add or remove from this pool.
  storage?: string;
  // List of guest VMIDs to add or remove from this pool.
  vms?: string;
}
```

### Returns

```ts
type Returns = any;
```
