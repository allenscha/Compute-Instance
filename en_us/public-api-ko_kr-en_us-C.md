## Compute > Instance > API v2 guide

To use the API, you need an API endpoint, token, etc. See [Preparing to use](/Compute/Compute/ko/identity-api/) the API to prepare the information needed to use the API.

The instance API uses a `compute` type endpoint. Refer to the `ServiceCatalog` in the token issuance response for the exact endpoint.

| type | region | endpoints |
|---|---|---|
| compute | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region<br>Japan region | https://kr1-api-instance.infrastructure.cloud.toast.com<br>https://kr2-api-instance.infrastructure.cloud.toast.com<br>https://jp1-api-instance.infrastructure.cloud.toast.com |

Fields not specified in the guide may appear in the API response. These fields are not used because they are for NHN Cloud internal use and are subject to change without prior notice.

## instance type

### View a list of types

```
GET /v2/{tenantId}/flavors
X-Auth-Token: {tokenId}
```

#### requisitions

This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |
| minDisk | Query | Integer | - | Minimum block storage size (GB)<br>Return only types whose block storage size is larger than the specified size |
| minRam | Query | Integer | - | Minimum RAM size (MB)<br>Return only types with RAM larger than the specified size |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| flavors | Body | Object | instance type list object |
| flavors.id | Body | UUID | Instance type ID |
| flavors.links | Body | Object | instance type path object |
| flavors.name | Body | String | Instance type name |


<details><summary>exemplify</summary>
<p>

```json
{
  "flavors": [
    {
      "id": "013bea75-8541-4c6f-9abe-a03fee3d74fe",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/013bea75-8541-4c6f-9abe-a03fee3d74fe",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/013bea75-8541-4c6f-9abe-a03fee3d74fe",
          "rel": "bookmark"
        }
      ],
      "name": "x1.c32m256"
    },
    {
      "id": "0f19a344-bc66-4228-8cb1-fb9ca82c54f5",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/0f19a344-bc66-4228-8cb1-fb9ca82c54f5",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/0f19a344-bc66-4228-8cb1-fb9ca82c54f5",
          "rel": "bookmark"
        }
      ],
      "name": "x1.c32m128"
    }
  ]
}
```

</p>
</details>

---

### View a detailed list of types

```
GET /v2/{tenantId}/flavors/detail
X-Auth-Token: {tokenId}
```

#### requisitions

This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |
| minDisk | Query | Integer | - | Minimum block storage size (GB)<br>Return only types whose block storage size is larger than the specified size |
| minRam | Query | Integer | - | Minimum RAM size (MB)<br>Return only types with RAM larger than the specified size |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| flavors | Body | Object | instance type list object |
| flavors.id | Body | UUID | Instance type ID |
| flavors.links | Body | Object | instance type path object |
| flavors.name | Body | String | Instance type name |
| flavors.ram | Body | Integer | Memory size (MB) |
| flavors.OS-FLV-DISABLED:disabled | Body | Boolean | Activated or not |
| flavors.vcpus | Body | Integer | Number of vCPUs |
| flavors.extra_specs | Body | Object | Extra spec objects |
| flavors.swap | Body | Integer | Swap area size (GB) |
| flavors.os-flavor-access:is_public | Body | Boolean | Whether to share |
| flavors.rxtx_factor | Body | Float | Network send/receive packet ratio |
| flavors.OS-FLV-EXT-DATA:ephemeral | Body | Integer | Temporary volume size (GB) |
| flavors.disk | Body | Integer | Default disk size (GB) |

<details><summary>exemplify</summary>
<p>

```json
{
  "flavors": [
    {
      "name": "x1.c32m256",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/97604802-a090-43fa-a5ce-c7cfd737fbba",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/97604802-a090-43fa-a5ce-c7cfd737fbba",
          "rel": "bookmark"
        }
      ],
      "ram": 262144,
      "OS-FLV-DISABLED:disabled": false,
      "vcpus": 32,
      "extra_specs": {
        "flavor_type": "performance"
      },
      "swap": "",
      "os-flavor-access:is_public": true,
      "rxtx_factor": 1.0,
      "OS-FLV-EXT-DATA:ephemeral": 0,
      "disk": 0,
      "id": "97604802-a090-43fa-a5ce-c7cfd737fbba"
    },
    {
      "name": "x1.c32m128",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/31fa632d-aeec-4f12-8a57-ce9d146228e5",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/31fa632d-aeec-4f12-8a57-ce9d146228e5",
          "rel": "bookmark"
        }
      ],
      "ram": 131072,
      "OS-FLV-DISABLED:disabled": false,
      "vcpus": 32,
      "extra_specs": {
        "flavor_type": "performance"
      },
      "swap": "",
      "os-flavor-access:is_public": true,
      "rxtx_factor": 1.0,
      "OS-FLV-EXT-DATA:ephemeral": 0,
      "disk": 0,
      "id": "31fa632d-aeec-4f12-8a57-ce9d146228e5"
    }
  ]
}
```

</p>
</details>

---

## Availability Zones

### View availability list

```
GET /v2/{tenantId}/os-availability-zone
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |

#### responsive
| names | variety | formats | illustrative |
|---|---|---|---|
| availabilityZoneInfo | Body | Object | availability zone information object |
| availabilityZoneInfo.zoneName | Body | String | Availability zone name |
| availabilityZoneInfo.zoneState | Body | Object | availability zone status information object |
| availabilityZoneInfo.available | Body | Object | Availability zone status |

<details><summary>exemplify</summary>
<p>

```json
{
    "availabilityZoneInfo": [
      {
        "zoneState": {
          "available": true
        },
        "zoneName": "kr-pub-a"
      },
      {
        "zoneState": {
          "available": true
        },
        "zoneName": "kr-pub-b"
      }
    ]
}
```

</p>
</details>

---

## Keypair

### View a list of key pairs
```
GET /v2/{tenantId}/os-keypairs
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| keypairs | Body | Array | List of keypair objects |
| keypairs.keypair | Body | Object | keypair object |
| keypairs.keypair.name | Body | String | Keypair name |
| keypairs.keypair.public_key | Body | String | public key |
| keypairs.keypair.fingerprint | Body | String | Keypair fingerprints |

<details><summary>exemplify</summary>
<p>

```json
{
  "keypairs": [
    {
      "keypair": {
        "public_key": "ssh-rsa ... Generated-by-Nova",
        "name": "keypair",
        "fingerprint": "SHA256:..."
      }
    }
  ]
}
```

</p>
</details>

---

### View Keypair
```
GET /v2/{tenantId}/os-keypairs/{keypairName}
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| keypairName | URL | String | O | Keypair name |
| tokenId | Header | String | O | Token ID |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| keypair | Body | Object | List of keypair objects |
| keypair.public_key | Body | String | public key |
| keypair.user_id | Body | String | Keypair owner ID |
| keypair.name | Body | String | Keypair name |
| keypair.deleted | Body | Boolean | Whether to delete a keypair |
| keypair.created_at | Body | Datetime | Keypair creation time<br>`YYYY-MM-DDThh:mm:ss.SSSSSS` |
| keypair.updated_at | Body | Datetime | Keypair modification time<br>`YYYY-MM-DDThh:mm:ss.SSSSSS` |
| keypair.deleted_at | Body | Datetime | Keypair deletion time<br>`YYYY-MM-DDThh:mm:ss.SSSSSS` |
| keypair.fingerprint | Body | String | Keypair fingerprints |
| keypair.id | Body | Integer | Keypair ID |

<details><summary>exemplify</summary>
<p>

```json
{
  "keypair": {
    "public_key": "ssh-rsa ... Generated-by-Nova",
    "user_id": "826a1213b3f746829515486965690dfe",
    "name": "keypair",
    "deleted": false,
    "created_at": "2020-02-07T03:46:48.000000",
    "updated_at": null,
    "fingerprint": "SHA256:...",
    "deleted_at": null,
    "id": 51
  }
}
```

</p>
</details>

---

### Create/register a key pair

```
POST /v2/{tenantId}/os-keypairs
X-Auth-Token: {tokenId}
```

#### requisitions

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |
| keypair | Body | Object | O | keypair object |
| keypair.name | Body | String | O | The name of the keypair to be created or registered |
| keypair.public_key | Body | String | - | The public key to register. If this field is omitted, a new key pair will be created. |

<details><summary>exemplify</summary>
<p>

```json
{
    "keypair": {
        "name": "keypair-d20a3d59-9433-4b79-8726-20b431d89c78",
        "public_key": "ssh-rsa ... Generated-by-Nova"
    }
}
```

</p>
</details>

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| keypair | Body | Object | keypair object |
| keypair.public_key | Body | String | public key |
| keypair.private_key | Body | String | Private key, if a new key pair is created, the private key is returned. |
| keypair.user_id | Body | String | Keypair owner ID |
| keypair.name | Body | String | Keypair name |
| keypair.fingerprint | Body | String | Keypair fingerprints |

<details><summary>exemplify</summary>
<p>

```json
{
    "keypair": {
        "fingerprint": "SHA256:+EZoD ... /DKiGnY4zf5tYrcix0",
        "name": "keypair",
        "public_key": "ssh-rsa ... Generated-by-Nova",
        "user_id": "436f727b7c9142f896ddd56be591dd7f"
    }
}
```

</p>
</details>

---

### Deleting a keypair
```
DELETE /v2/{tenantId}/os-keypairs/{keypairName}
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| keypairName | URL | String | O | Keypair name |
| tokenId | Header | String | O | Token ID |

#### responsive
This API does not return a response body.


## instance

### instance status

An instance has various states, and the actions that can be taken are determined by the state. The list of instance states is as follows:

| Status name | illustrative |
|--|--|
| `ACTIVE` | If the instance is active |
| `BUILDING` | If an instance is being created |
| `STOPPED`| If the instance is stopped |
| `DELETED`| If the instance has been deleted |
| `REBOOT`| If you restart an instance |
| `HARD_REBOOT`| When an instance is forcibly restarted<br> The same action as powering down a physical server and turning it back on |
| `RESIZED`| When you change the instance type or move an instance to a different host<br>The state where the instance was stopped and then restarted |
| `REVERT_RESIZE`| When recovering to return to the original state when the instance type changes or when the process of moving an instance to a different host fails |
| `VERIFY_RESIZE`| When an instance is in the process of changing its type or moving an instance to a different host and is waiting for user approval<br>NHN Cloud automatically becomes `ACTIVE` in this case |
| `ERROR`| If the action taken on the previous instance failed |
| `PAUSED`| If the instance is suspended<br>Suspended instances are stored in the hypervisor's memory |
| `REBUILD`| The state of creating a new instance from an image at the time of creation |
| `RESCUED`| The instance is running in recovery mode |
| `SUSPENDED`| If the instance has been put into hibernation mode by an administrator |
| `UNKNOWN`| If the state of the instance is unknown<br>`If the instance enters this state, contact the administrator.` |

### View a list of instances

```
GET /v2/{tenantId}/servers
X-Auth-Token: {tokenId}
```

#### requisitions

This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |
| reservation_id | Query | String | - | Instance creation reservation ID. <br>If a reservation ID is specified, only a list of instances created at the same time is returned |
| changes-since | Query | Datetime | - | Returns a list of instances that have changed since the specified time. The form `yyyy-mm-ddthh:mm:ss`. |
| image | Query | UUID | - | image ID<br>Returns a list of instances using the specified image |
| flavor | Query | UUID | - | Instance type ID<br>Returns a list of instances using the specified type |
| name | Query | String | - | instance name<br>Returns a list of instances with a specified name; can be queried with a regular expression |
| status | Query | Enum | - | instance status<br>Returns a list of instances with a specified state |
| limit | Query | Integer | - | Number of instance lists<br>Returns a list of the specified number of instances |
| marker | Query | UUID | - | The UUID of the first instance in the list<br>Returns a list of instances `equal to a `limit number` from the instance specified as a marker` according to the sorting criteria |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| servers | Body | Object | instance list object |
| id | Body | UUID | instance UUID |
| links | body | Object | instance path object |
| name | body | String | instance name |

<details><summary>exemplify</summary>
<p>

```json
{
  "servers": [
    {
      "id": "aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
          "rel": "bookmark"
        }
      ],
      "name": "Web-Server"
    }
  ]
}
```

</p>
</details>

---

### View instance list details

It returns a list of instances created for the current tenant in the same way as the instance list view. However, detailed information for each instance is also queried.

```
GET /v2/{tenantId}/servers/detail
X-Auth-Token: {tokenId}
```

#### requisitions

This is the same request format as the instance list view.

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| servers | body | Object | instance list object |
| status | body | Enum | instance status |
| servers.id | Body | UUID | instance ID |
| servers.name | Body | String | Instance name, 255 characters maximum |
| servers.updated | Body | Datetime | instance last modified time, `yyyy-mm-ddthh:mm:ssz` format |
| servers.hostId | Body | String | The ID of the host the instance is running on |
| servers.addresses | Body | Object | An instance IP list object. <br>A list was created based on the number of ports connected to the instance. |
| servers.addresses. “Network name” | Body | Object | Network-specific port information connected to the instance |
| servers.addresses. “network name” .os-ext-ips-mac:mac_addr | Body | String | The MAC address of the port connected to the instance |
| servers.addresses. “network name” .version | Body | Integer | The IP version of the port connected to the instance<br>NHN Cloud only supports IPv4 |
| servers.addresses. “Network name” .addr | Body | String | The IP address of the port connected to the instance |
| servers.addresses. “Network name” .os-ext-ips:type | Body | Enum | The IP address type of the port<br>`Either fixed` or `floating` |
| servers.links | Body | Object | instance path object |
| servers.key_name | Body | String | Instance keypair name |
| servers.image | Body | Object | instance image object |
| servers.image.id | Body | UUID | instance image id |
| servers.image.links | Body | Object | instance image path object |
| servers.OS-EXT-STS:task_state | Body | String | Instance task status<br>Notify the progress of the operation when an action is applied to the instance |
| servers.OS-EXT-STS:vm_state | Body | String | The current state of the instance |
| servers.OS-SRV-USG:launched_at | Body | Datetime | The time the instance last booted<br>`yyyy-mm-ddthh:mm:ss.ssssss` format |
| servers.OS-SRV-USG:terminated_at | Body | Datetime | Instance deletion time<br>`yyyy-mm-ddthh:mm:ssz` format |
| servers.flavor | Body | Object | instance type information object |
| servers.flavor.id | Body | UUID | Instance type ID |
| servers.flavor.links | Body | Object | instance type path object |
| servers.security_groups | Body | Object | Security group list object assigned to the instance |
| servers.security_groups.name | Body | String | The name of the security group assigned to the instance |
| servers.user_id | Body | String | The ID of the user who created the instance |
| servers.created | Body | Datetime | The time the instance was created. `yyyy-mm-ddthh:mm:ssz` format |
| servers.tenant_id | Body | String | The ID of the tenant to which the instance belongs |
| servers.OS-DCF:diskConfig | Body | Enum | Instance disk partitioning method, either `MANUAL` or `AUTO`<br>**AUTO**: automatically sets the entire disk to a single partition<br>**MANUAL**: Set up partitions as specified in the image. If the block storage size is larger than the size set in the image, leave it unused. NHN Cloud uses `MANUAL` |
| servers.os-extended-volumes:volumes_attached | Body | Object | Additional volume list object attached to the instance |
| servers.os-extended-volumes:volumes_attached.id | Body | UUID | Additional volume IDs attached to the instance |
| servers.OS-EXT-STS:power_state | Body | Integer | The instance's power state<br>- `1`: On<br>- `4`: Off |
| servers.metadata | Body | Object | instance metadata object<br>Store instance metadata as key-value pairs |

<details><summary>exemplify</summary>
<p>

```json
{
  "servers": [
    {
      "status": "ACTIVE",
      "updated": "2020-02-25T01:22:24Z",
      "hostId": "078d06f898889699f8731d030812e43d2c417edb2cf641dda598c7bd",
      "addresses": {
        "vpc2": [
          {
            "OS-EXT-IPS-MAC:mac_addr": "fa:16:3e:54:a7:64",
            "version": 4,
            "addr": "172.16.0.40",
            "OS-EXT-IPS:type": "fixed"
          }
        ]
      },
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
          "rel": "self"
        },
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
          "rel": "bookmark"
        }
      ],
      "key_name": "access-key",
      "image": {
        "id": "8b9f8d47-b89b-45af-b1d6-3f7ce7e06a11",
        "links": [
          {
            "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/images/8b9f8d47-b89b-45af-b1d6-3f7ce7e06a11",
            "rel": "bookmark"
          }
        ]
      },
      "OS-EXT-STS:task_state": null,
      "OS-EXT-STS:vm_state": "active",
      "OS-SRV-USG:launched_at": "2020-02-25T01:22:23.000000",
      "flavor": {
        "id": "35a73b57-58a7-434d-aa08-5249aaa95b3e",
        "links": [
          {
            "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/35a73b57-58a7-434d-aa08-5249aaa95b3e",
            "rel": "bookmark"
          }
        ]
      },
      "id": "aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
      "security_groups": [
        {
          "name": "default"
        }
      ],
      "OS-SRV-USG:terminated_at": null,
      "OS-EXT-AZ:availability_zone": "kr-pub-b",
      "user_id": "b6ab578c20c94306ac1f41ffc4415b29",
      "name": "Web-Server",
      "created": "2020-02-25T01:15:46Z",
      "tenant_id": "6cdebe3eb0094910bc41f1d42ebe4cb7",
      "OS-DCF:diskConfig": "MANUAL",
      "os-extended-volumes:volumes_attached": [
        {
          "id": "90712f4f-2faa-4e4f-8eb1-9313a8595570"
        }
      ],
      "accessIPv4": "",
      "accessIPv6": "",
      "progress": 0,
      "OS-EXT-STS:power_state": 1,
      "config_drive": "",
      "metadata": {
        "os_distro": "Windows",
        "description": "Windows 2012 R2 STD (2020.02.18)",
        "os_version": "2012 R2 STD",
        "project_domain": "NORMAL",
        "hypervisor_type": "qemu",
        "monitoring_agent": "sysmon",
        "image_name": "Windows 2012 R2 STD (2020.02.18) EN",
        "volume_size": "50",
        "os_architecture": "amd64",
        "login_username": "Administrator",
        "os_type": "Windows",
        "tc_env": "sysmon"
      }
    }
  ]
}
```

</p>
</details>

---

### View an instance

```
GET /v2/{tenantId}/servers/{serverId}
X-Auth-Token: {tokenId}
```

#### requisitions

This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | instance ID |
| tokenId | Header | String | O | Token ID |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| server | body | Object | instance object |
| status | body | Enum | instance status |
| server.id | Body | UUID | instance ID |
| server.name | Body | String | Instance name, 255 characters maximum |
| server.updated | Body | Datetime | instance last modified time, `yyyy-mm-ddthh:mm:ssz` format |
| server.hostId | Body | String | The ID of the host the instance is running on |
| server.addresses | Body | Object | instance IP list object <br>A list is generated based on the number of ports connected to the instance |
| server.addresses. “Network name” | Body | Object | Network-specific port information connected to the instance |
| server.addresses. “network name” .os-ext-ips-mac:mac_addr | Body | String | The MAC address of the port connected to the instance |
| server.addresses. “network name” .version | Body | Integer | The IP version of the port connected to the instance<br>NHN Cloud only supports IPv4 |
| server.addresses. “Network name” .addr | Body | String | The IP address of the port connected to the instance |
| server.addresses. “Network name” .os-ext-ips:type | Body | Enum | The IP address type of the port<br>`Either fixed` or `floating` |
| server.links | Body | Object | instance path object |
| server.key_name | Body | String | Instance keypair name |
| server.image | Body | Object | instance image object |
| server.image.id | Body | UUID | instance image id |
| server.image.links | Body | Object | instance image path object |
| server.OS-EXT-STS:task_state | Body | String | Instance task status<br>Notify the progress of an operation when an action is applied to an instance |
| server.OS-EXT-STS:vm_state | Body | String | The current state of the instance |
| server.OS-SRV-USG:launched_at | Body | Datetime | The time the instance last booted<br>`yyyy-mm-ddthh:mm:ss.ssssss` format |
| server.OS-SRV-USG:terminated_at | Body | Datetime | Instance deletion time<br>`yyyy-mm-ddthh:mm:ssz` format |
| server.flavor | Body | Object | instance type information object |
| server.flavor.id | Body | UUID | Instance type ID |
| server.flavor.links | Body | Object | instance type path object |
| server.security_groups | Body | Object | Security group list object assigned to the instance |
| server.security_groups.name | Body | String | The name of the security group assigned to the instance |
| server.user_id | Body | String | The ID of the user who created the instance |
| server.created | Body | Datetime | instance creation time, `yyyy-mm-ddthh:mm:ssz` format |
| server.tenant_id | Body | String | The ID of the tenant to which the instance belongs |
| server.OS-DCF:diskConfig | Body | Enum | Instance disk partitioning scheme. `Either MANUAL` or `AUTO`.<br>**AUTO**: automatically sets the entire disk to a single partition<br>**MANUAL**: Set up partitions as specified in the image. If the block storage size is larger than the size set in the image, leave it unused. NHN Cloud uses `MANUAL` |
| server.os-extended-volumes:volumes_attached | Body | Object | Additional volume list object attached to the instance |
| server.os-extended-volumes:volumes_attached.id | Body | UUID | Additional volume IDs attached to the instance |
| server.OS-EXT-STS:power_state | Body | Integer | The instance's power state<br>- `1`: On<br>- `4`: Off |
| server.metadata | Body | Object | instance metadata object<br>Store instance metadata as key-value pairs |
| server.NHN-EXT-ATTR:ephemeral_disk_size | Body | Integer | The amount of additional local block storage attached to the instance |

<details><summary>exemplify</summary>
<p>

```json
{
  "server": {
    "status": "ACTIVE",
    "updated": "2020-02-25T01:22:24Z",
    "hostId": "078d06f898889699f8731d030812e43d2c417edb2cf641dda598c7bd",
    "addresses": {
      "vpc2": [
        {
          "OS-EXT-IPS-MAC:mac_addr": "fa:16:3e:54:a7:64",
          "version": 4,
          "addr": "172.16.0.40",
          "OS-EXT-IPS:type": "fixed"
        }
      ]
    },
    "links": [
      {
        "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
        "rel": "self"
      },
      {
        "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
        "rel": "bookmark"
      }
    ],
    "key_name": "access-key",
    "image": {
      "id": "8b9f8d47-b89b-45af-b1d6-3f7ce7e06a11",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/images/8b9f8d47-b89b-45af-b1d6-3f7ce7e06a11",
          "rel": "bookmark"
        }
      ]
    },
    "OS-EXT-STS:task_state": null,
    "OS-EXT-STS:vm_state": "active",
    "OS-SRV-USG:launched_at": "2020-02-25T01:22:23.000000",
    "flavor": {
      "id": "35a73b57-58a7-434d-aa08-5249aaa95b3e",
      "links": [
        {
          "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/flavors/35a73b57-58a7-434d-aa08-5249aaa95b3e",
          "rel": "bookmark"
        }
      ]
    },
    "id": "aaf2778b-ea03-4ccc-8b1b-92f4b686c3ec",
    "security_groups": [
      {
        "name": "default"
      }
    ],
    "OS-SRV-USG:terminated_at": null,
    "OS-EXT-AZ:availability_zone": "kr-pub-b",
    "user_id": "b6ab578c20c94306ac1f41ffc4415b29",
    "name": "Web-Server",
    "created": "2020-02-25T01:15:46Z",
    "tenant_id": "6cdebe3eb0094910bc41f1d42ebe4cb7",
    "OS-DCF:diskConfig": "MANUAL",
    "os-extended-volumes:volumes_attached": [
      {
        "id": "90712f4f-2faa-4e4f-8eb1-9313a8595570"
      }
    ],
    "accessIPv4": "",
    "accessIPv6": "",
    "progress": 0,
    "OS-EXT-STS:power_state": 1,
    "config_drive": "",
    "metadata": {
      "os_distro": "Windows",
      "description": "Windows 2012 R2 STD (2020.02.18)",
      "os_version": "2012 R2 STD",
      "project_domain": "NORMAL",
      "hypervisor_type": "qemu",
      "monitoring_agent": "sysmon",
      "image_name": "Windows 2012 R2 STD (2020.02.18) EN",
      "volume_size": "50",
      "os_architecture": "amd64",
      "login_username": "Administrator",
      "os_type": "Windows",
      "tc_env": "sysmon"
    }
  }
}
```

</p>
</details>

---

### Creating an instance

Create an instance.

After calling the instance creation API, check the instance status by querying the instance.

* When the status of the instance becomes **ACTIVE**, the instance creation is completed normally.
* If the instance **state persists for a long time in BUILDING** or is **ERROR**, check the instance creation parameters and attempt to create it again.

Windows instances have the following creation constraints for stable operation:

* Use an instance type with at least 2 GB of RAM.
* A basic disk of 50 GB or more is required.
* Windows images cannot be used for U2 types.

The default disk size can be specified starting at 10 GB for Linux and 50 GB for Windows.


```
POST /v2/{tenantId}/servers
X-Auth-Token: {tokenId}
```

#### requisitions

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| tokenId | Header | String | O | Token ID |
| server.security_groups | body | Object | - | security group list object<br>If omitted, a `default` group is added |
| server.security_groups.name | body | String | - | The name of the security group to add to the instance |
| server.user_data | body | String | - | Scripts and settings to run after the instance boots<br>Base64 encoded string allows up to 65535 bytes |
| server.availability_zone | body | String | - | Availability zone in which to create an instance<br>If not specified, randomly selected |
| server.imageRef | Body | String | O | The image ID to use when creating an instance |
| server.flavorRef | Body | String | O | The instance type ID to use when creating an instance |
| server.networks | Body | Object | O | A network information object to use when creating an instance<br>A specified number of NICs are added and specified as a network ID, subnet ID, port ID, or static IP |
| server.networks.uuid | Body | UUID | - | The network ID to use when creating the instance |
| server.networks.subnet | Body | UUID | - | The subnet ID of the network to use when creating the instance |
| server.networks.port | Body | UUID | - | Port ID to use when creating an instance |
| server.networks.fixed_ip | Body | String | - | A static IP to use when creating an instance |
| server.name | Body | String | O | The name of the instance<br>Up to 255 English characters are allowed, but Windows images must be 15 characters or less |
| server.metadata | Body | Object | - | Metadata objects to add to the instance<br>Key-value pairs with a maximum length of 255 characters |
| server.block_device_mapping_v2 | Body | Object | - | An instance's block storage information object<br>**Must be specified when using an instance type other than U2 that uses a local disk** |
| server.block_device_mapping_v2.uuid | Body | String | - | Source ID for block storage <br>If it is a root volume, it must be a bootable source; you cannot use a volume or snapshot whose source is a WAF, MS-SQL, or MySQL image that cannot create an image<br> Sources other than `image` must have the same availability zone as the instance to be created |
| server.block_device_mapping_v2.source_type | Body | Enum | - | The type of block storage source to be created<br>`image`: Create block storage using images<br>`volume`: Use the volume that was previously created; the destination_type must be specified as volume<br>`snapshot`: Create block storage using a snapshot; destination_type must be specified as volume |
| server.block_device_mapping_v2.destination_type | Body | Enum | - | Different settings are required depending on the location and instance type of the instance volume.<br>- `local`: When using the U2 instance type<br>- `volume`: When using an instance type other than U2 |
| server.block_device_mapping_v2.volume_type | Body | String | - | The type of volume being created<br>- `General HDD`: HDD type volume<br>- `General SSD`: SSD-type volume<br> If omitted, it will be applied as `General HDD` |
| server.block_device_mapping_v2.delete_on_termination | Body | Boolean | - | Whether to process volumes when deleting an instance; the default value is `false`.<br>If `true`, delete`; false` keep |
| server.block_device_mapping_v2.boot_index | Body | Integer | - | The boot order for the specified volume<br>- If `0`, the root volume<br>- Other than that, extra volume<br>The larger the size, the lower the boot order |
| server.key_name | Body | String | O | The key pair to use to connect to the instance |
| server.min_count | Body | Integer | - | The minimum number of instances to be created by the current request.<br>The default value is 1. |
| server.max_count | Body | Integer | - | The maximum number of instances to be created by the current request.<br>The default value is min_count, and the maximum value is 10. |
| server.return_reservation_id | Body | Boolean | - | Instance creation request reservation ID.<br>If set to True, the instance creation information will be returned instead of the reservation ID.<br>Default value is False |

<details><summary>exemplify</summary>
<p>

```json
{
  "server": {
    "name": "DB-Master",
    "imageRef": "9956f822-29c9-4f81-9410-0c392d9c8c24",
    "flavorRef": "a4b6a0f7-aeff-4d78-a8d5-7de9f007012d",
    "networks": [{
      "subnet": "b83863ff-0355-4c73-8c10-0bdf66a69aab"
    }],
    "availability_zone": "kr-pub-a",
    "key_name": "access-key",
    "max_count": 1,
    "min_count": 1,
    "block_device_mapping_v2": [{
      "uuid": "9956f822-29c9-4f81-9410-0c392d9c8c24",
      "boot_index": 0,
      "volume_size": 1000,
      "device_name": "vda",
      "source_type": "image",
      "destination_type": "volume",
      "delete_on_termination": 1
    }],
    "security_groups": [{
      "name": "default"
    }]
  }
}
```

</p>
</details>

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| server.security_groups.name | Body | String | The name of the security group for the instance you created |
| server.OS-DCF:diskConfig | Body | Enum | Instance disk partitioning scheme. `Either MANUAL` or `AUTO`. Set to `MANUAL` on NHN Cloud.<br>**AUTO**: automatically sets the entire disk to a single partition<br>**MANUAL**: Set up partitions as specified in the image. If the block storage size is larger than the size set in the image, leave it unused. |
| server.id | Body | UUID | The ID of the instance you created |

<details><summary>exemplify</summary>
<p>

```json
{
  "server": {
    "security_groups": [
      {
        "name": "default"
      }
    ],
    "OS-DCF:diskConfig": "MANUAL",
    "id": "3a005d5b-63cf-4493-bfc6-49db990b5b50",
    "links": [
      {
        "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/v2/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/3a005d5b-63cf-4493-bfc6-49db990b5b50",
        "rel": "self"
      },
      {
        "href": "https://kr1-api-instance.infrastructure.cloud.toast.com/6cdebe3eb0094910bc41f1d42ebe4cb7/servers/3a005d5b-63cf-4493-bfc6-49db990b5b50",
        "rel": "bookmark"
      }
    ]
  }
}
```

</p>
</details>

---

### Modifying an instance
Modify the instance that was created. The attributes that can be changed are limited to some items.

```
PUT /v2/{tenantId}/servers/{serverId}
X-Auth-Token: {tokenId}
```

#### requisitions

| names | variety | formats | required | illustrative |
|---|---|---|---|---|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| server | Body | Object | O | instance change request object |
| server.name | Body | String | - | The new name for the instance |

<details><summary>exemplify</summary>
<p>

```json
{
    "server": {
        "name": "new-server-test"
    }
}
```

</p>
</details>

#### responsive
This is the same as the instance view.

---

### Deleting an instance
Delete the instance that was created.

```
DELETE /v2/{tenantId}/servers/{serverId}
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The ID of the instance to delete |
| tokenId | Header | String | O | Token ID |

#### responsive
This API does not return a response body.

---

## Managing volume connections
### View a list of volumes attached to an instance
```
GET /v2/{tenantId}/servers/{serverId}/os-volume_attachments
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| limit | Query | Integer | - | Number of lists to view |
| offset | Query | Integer | - | The starting point of the list to be returned<br>Return the offsetth volume in the entire list |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| volumeAttachments | Body | Array | List of connection information objects |
| volumeAttachments.device | Body | String | The instance's volume name<br>Example: `/dev/vdb` |
| volumeAttachments.id | Body | UUID | Connection info ID |
| volumeAttachments.serverId | Body | UUID | instance ID |
| volumeAttachments.volumeId | Body | UUID | volume id |

<details><summary>exemplify</summary>
<p>

```json
{
    "volumeAttachments": [
        {
            "device": "/dev/vda",
            "id": "227cc671-f30b-4488-96fd-7d0bf13648d8",
            "serverId": "4b293d31-ebd5-4a7f-be03-874b90021e54",
            "volumeId": "227cc671-f30b-4488-96fd-7d0bf13648d8"
        },
        {
            "device": "/dev/vdb",
            "id": "a07f71dc-8151-4e7d-a0cc-cd24a3f11113",
            "serverId": "4b293d31-ebd5-4a7f-be03-874b90021e54",
            "volumeId": "a07f71dc-8151-4e7d-a0cc-cd24a3f11113"
        }
    ]
}
```

</p>
</details>

---

### View volumes attached to an instance
```
GET /v2/{tenantId}/servers/{serverId}/os-volume_attachments/{volumeId}
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | instance ID |
| volumeId | URL | UUID | O | The ID of the volume to be queried |
| tokenId | Header | String | O | Token ID |

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| volumeAttachment | Body | Object | connection information object |
| volumeAttachment.device | Body | String | The instance's volume name<br>Example: `/dev/vdb` |
| volumeAttachment.id | Body | UUID | Connection info ID |
| volumeAttachment.serverId | Body | UUID | instance ID |
| volumeAttachment.volumeId | Body | UUID | volume id |

<details><summary>exemplify</summary>
<p>

```json
{
    "volumeAttachment": {
        "device": "/dev/sdb",
        "id": "a07f71dc-8151-4e7d-a0cc-cd24a3f11113",
        "serverId": "1ad6852e-6605-4510-b639-d0bff864b49a",
        "volumeId": "a07f71dc-8151-4e7d-a0cc-cd24a3f11113"
    }
}
```

</p>
</details>

---

### Attaching additional volumes to an instance
```
POST /v2/{tenantId}/servers/{serverId}/os-volume_attachments
X-Auth-Token: {tokenId}
```

#### requisitions

| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| volumeAttachment | Body | Object | O | volume connection request object |
| volumeAttachment.volumeId | Body | UUID | O | Volume ID to connect |

<details><summary>exemplify</summary>
<p>

```json
{
  "volumeAttachment": {
      "volumeId": "a07f71dc-8151-4e7d-a0cc-cd24a3f11113"
  }
}
```

</p>
</details>

#### responsive

| names | variety | formats | illustrative |
|---|---|---|---|
| volumeAttachment | Body | Object | connection information object |
| volumeAttachment.device | Body | String | The instance's volume name<br>Example: `/dev/vdb` |
| volumeAttachment.id | Body | UUID | Connection info ID |
| volumeAttachment.serverId | Body | UUID | instance ID |
| volumeAttachment.volumeId | Body | UUID | volume id |

<details><summary>exemplify</summary>
<p>

```json
{
    "volumeAttachment": {
        "device": "/dev/vdc",
        "id": "227cc671-f30b-4488-96fd-7d0bf13648d8",
        "serverId": "4b293d31-ebd5-4a7f-be03-874b90021e54",
        "volumeId": "227cc671-f30b-4488-96fd-7d0bf13648d8"
    }
}
```

</p>
</details>

---

### Disconnect an instance volume
```
DELETE /v2/{tenantId}/servers/{serverId}/os-volume_attachments/{volumeId}
X-Auth-Token: {tokenId}
```

#### requisitions
This API does not require a request body.

| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | instance ID |
| volumeId | URL | UUID | O | Volume ID to disconnect |
| tokenId | Header | String | O | Token ID |

#### responsive
This API does not return a response body.

---

## Instance addition function
NHN Cloud provides the following instance controls and additional features:

* Start, stop, and restart an instance
* Change the instance type
* Create an instance image
* Adding and Removing Security Groups

### Start an instance

Restart the stopped instance and change its status to **ACTIVE**. To call this API, the instance must be in **SHUTOFF** state.

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| os-start | Body | none | O | Request to launch an instance |

<details><summary>exemplify</summary>
<p>

```json
{
  "os-start" : null
}
```

</p>
</details>

---

#### responsive
This API does not return a response body.

### Stop an instance

Stop the instance and change its status to **SHUTOFF**. To call this API, the instance must be in an **ACTIVE** or **ERROR** state.

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| os-stop | Body | none | O | Request to stop an instance |

<details><summary>exemplify</summary>
<p>

```json
{
  "os-stop" : null
}
```

</p>
</details>

#### responsive
This API does not return a response body.

---

### Restart an instance

Restart the instance Restart methods can be divided into **SOFT** and **HARD**.

* **SOFT** method: Stop and restart the instance via **"Graceful Shutdown"**. The instance must be in an **ACTIVE** state.
* **HARD** method: Force stop and then restart the instance. This is the same action as powering off a physical server and then turning it back on. An instance can only be forcibly stopped when it is in the following state:
    * **ACTIVE**
    * **ERROR**
    * **HARD_REBOOT**
    * **PAUSED**
    * **REBOOT**
    * **SHUTOFF**
    * **SUSPENDED**

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| reboot | Body | Object | O | instance reboot request object |
| reboot.type | Body | Enum | O | Reboot method, **SOFT** or **HARD** |

<details><summary>exemplify</summary>
<p>

```json
{
  "reboot" : {
    "type": "SOFT"
  }
}
```

</p>
</details>

#### responsive
This API does not return a response body.

---

### Change the instance type

Change the instance type. You can change the instance type only when the instance is **ACTIVE** or **SHUTOFF**. If the instance's state is **ACTIVE**, the instance is stopped and restarted during the instance type change.

The types that can be changed may be limited depending on the image or instance type you use. Refer to the console user guide for detailed change restrictions.


```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| resize | Body | Object | O | Request to change the instance type |
| resize.flavorRef | Body | UUID | O | The ID of the instance type to be changed |
| resize.OS-DCF:diskConfig | Body | Enum | - | The default disk partitioning method after changing the type. `Either MANUAL` or `AUTO`. Set to `MANUAL` on NHN Cloud.<br>**AUTO**: automatically sets the entire disk to a single partition<br>**MANUAL**: Set up partitions as specified in the image. If the block storage size is larger than the size set in the image, leave it unused. |

<details><summary>exemplify</summary>
<p>

```json
{
  "resize" : {
    "flavorRef": "b5f1c148-732c-417d-9d1b-1dffca105dbe"
  }
}
```

</p>
</details>

#### responsive
This API does not return a response body.

---

### Create an instance image

Generates an image from an instance. Only instances of type `U2` can generate images through this API. For instance image creation other than `U2` type, see [Block Storage API] (/Storage/Block Storage/ko/public-api/ #_22).

**An image can only be created when the instance is in **ACTIVE**, **SHUTOFF**, **DECIDED, PAUSED** state.** It is recommended that the image generation proceed while the instance is stopped to ensure data consistency.

If the image creation succeeds, the image state changes to `active`. To confirm that image creation is complete, check the status continuously through the image query API.

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| createImage | Body | Object | O | Request to create an image |
| createImage.name | Body | String | O | The name of the image to create |
| createImage.metadata | Body | Object | - | Metadata of the image to be created<br>Technology in the form of key-value |

<details><summary>exemplify</summary>
<p>

```json
{
  "createImage" : {
      "name" : "foo-image",
      "metadata": {
          "meta_var": "meta_val"
      }
  }
}
```

</p>
</details>


#### responsive

This API does not return a response body. The generated image is checked with `Location` in the response header.

| names | variety | formats | illustrative |
|--|--|--|--|
| Location | Header | String | URL of the image you created |

---

### Adding a security group

Add a security group to the instance. The security group you add applies to all ports on the instance.

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| addSecurityGroup | Body | Object | O | Security Group Addition Request Object |
| addSecurityGroup.name | Body | String | O | The name of the security group to add |

<details><summary>exemplify</summary>
<p>

```json
{
    "addSecurityGroup": {
        "name": "test"
    }
}
```

</p>
</details>


#### responsive
This API does not return a response body.

---

### Delete a security group

Delete a security group from an instance. The specified security group is removed from all ports on the instance.

```
POST /v2/{tenantId}/servers/{serverId}/action
X-Auth-Token: {tokenId}
```

#### requisitions
| names | variety | formats | required | illustrative |
|---|---|---|---|--|
| tenantId | URL | String | O | Tenant ID |
| serverId | URL | UUID | O | The instance ID you want to change |
| tokenId | Header | String | O | Token ID |
| removeSecurityGroup | Body | Object | O | Security Group Deletion Request Object |
| removeSecurityGroup.name | Body | String | O | The name of the security group to delete |

<details><summary>exemplify</summary>
<p>

```json
{
    "removeSecurityGroup": {
        "name": "test"
    }
}
```

</p>
</details>


#### responsive
This API does not return a response body.
