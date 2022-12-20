---
page_title: "scp_file_storage Resource - scp"
subcategory: ""
description: |-
  Provides a File Storage resource.
---

# Resource: scp_file_storage

Provides a File Storage resource.


## Example Usage

```terraform
data "scp_region" "region" {
}

resource "scp_file_storage" "my_nfs_fs" {
  name            = var.name
  disk_type       = "SSD"
  protocol        = "NFS"
  is_encrypted    = false
  retention_count = 5
  region          = data.scp_region.region.location
}

resource "scp_file_storage" "my_cifs_fs" {
  name            = "fs_cifs_test"
  disk_type       = "HDD"
  protocol        = "CIFS"
  is_encrypted    = false
  cifs_password   = var.password

  snapshot_day_of_week = "SUN"
  snapshot_frequency   = "WEEKLY"
  snapshot_hour        = 11
  retention_count      = 1
  region               = data.scp_region.region.location
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `disk_type` (String) HDD / SSD / HP_SSD(Only Multi-node GPU Clusters)
- `name` (String) The file storage name to create. (3 to 28 lowercase characters with _)
- `protocol` (String) The file storage protocol type to create (NFS, CIFS)
- `region` (String) The file storage region name to create.

### Optional

- `cifs_password` (String) Cifs password is only available for CIFS protocol. (6 to 20 characters without following special characters ($, %, {, }, [, ], ", \)
- `is_encrypted` (Boolean) The file storage whether to use encryption.
- `retention_count` (Number) Snapshot archiving count
- `snapshot_day_of_week` (String) Snapshot creation cycle, It is only available when you use a Snapshot
- `snapshot_frequency` (String) Snapshot creation frequency, It is only available when you use a Snapshot
- `snapshot_hour` (Number) Snapshot creation hour, It is only available when you use a Snapshot

### Read-Only

- `id` (String) The ID of this resource.