---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: DCL     ***
#
# ----------------------------------------------------------------------------
#
#     This file is managed by Magic Modules (https:#github.com/GoogleCloudPlatform/magic-modules)
#     and is based on the DCL (https:#github.com/GoogleCloudPlatform/declarative-resource-client-library).
#     Changes will need to be made to the DCL or Magic Modules instead of here.
#
#     We are not currently able to accept contributions to this file. If changes
#     are required, please file an issue at https:#github.com/hashicorp/terraform-provider-google/issues/new/choose
#
# ----------------------------------------------------------------------------
subcategory: "ContainerAzure"
layout: "google"
page_title: "Google: google_container_azure_node_pool"
description: |-
An Anthos node pool running on Azure.
---

# google_container_azure_node_pool

An Anthos node pool running on Azure.

For more information, see:
* [Multicloud overview](https://cloud.google.com/anthos/clusters/docs/multi-cloud)
## Example Usage - basic_azure_node_pool
A basic example of a containerazure azure node pool
```hcl
data "google_container_azure_versions" "versions" {
  project = "my-project-name"
  location = "us-west1"
}

resource "google_container_azure_cluster" "primary" {
  authorization {
    admin_users {
      username = "mmv2@google.com"
    }
  }

  azure_region = "westus2"
  client       = "projects/my-project-number/locations/us-west1/azureClients/${google_container_azure_client.basic.name}"

  control_plane {
    ssh_config {
      authorized_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC8yaayO6lnb2v+SedxUMa2c8vtIEzCzBjM3EJJsv8Vm9zUDWR7dXWKoNGARUb2mNGXASvI6mFIDXTIlkQ0poDEPpMaXR0g2cb5xT8jAAJq7fqXL3+0rcJhY/uigQ+MrT6s+ub0BFVbsmGHNrMQttXX9gtmwkeAEvj3mra9e5pkNf90qlKnZz6U0SVArxVsLx07vHPHDIYrl0OPG4zUREF52igbBPiNrHJFDQJT/4YlDMJmo/QT/A1D6n9ocemvZSzhRx15/Arjowhr+VVKSbaxzPtEfY0oIg2SrqJnnr/l3Du5qIefwh5VmCZe4xopPUaDDoOIEFriZ88sB+3zz8ib8sk8zJJQCgeP78tQvXCgS+4e5W3TUg9mxjB6KjXTyHIVhDZqhqde0OI3Fy1UuVzRUwnBaLjBnAwP5EoFQGRmDYk/rEYe7HTmovLeEBUDQocBQKT4Ripm/xJkkWY7B07K/tfo56dGUCkvyIVXKBInCh+dLK7gZapnd4UWkY0xBYcwo1geMLRq58iFTLA2j/JmpmHXp7m0l7jJii7d44uD3tTIFYThn7NlOnvhLim/YcBK07GMGIN7XwrrKZKmxXaspw6KBWVhzuw1UPxctxshYEaMLfFg/bwOw8HvMPr9VtrElpSB7oiOh91PDIPdPBgHCi7N2QgQ5l/ZDBHieSpNrQ== thomasrodgers"
    }

    subnet_id = "/subscriptions/12345678-1234-1234-1234-123456789111/resourceGroups/my--dev-byo/providers/Microsoft.Network/virtualNetworks/my--dev-vnet/subnets/default"
    version   = "${data.google_container_azure_versions.versions.valid_versions[0]}"
  }

  fleet {
    project = "my-project-number"
  }

  location = "us-west1"
  name     = "name"

  networking {
    pod_address_cidr_blocks     = ["10.200.0.0/16"]
    service_address_cidr_blocks = ["10.32.0.0/24"]
    virtual_network_id          = "/subscriptions/12345678-1234-1234-1234-123456789111/resourceGroups/my--dev-byo/providers/Microsoft.Network/virtualNetworks/my--dev-vnet"
  }

  resource_group_id = "/subscriptions/12345678-1234-1234-1234-123456789111/resourceGroups/my--dev-cluster"
  project           = "my-project-name"
}

resource "google_container_azure_client" "basic" {
  application_id = "12345678-1234-1234-1234-123456789111"
  location       = "us-west1"
  name           = "client-name"
  tenant_id      = "12345678-1234-1234-1234-123456789111"
  project        = "my-project-name"
}

resource "google_container_azure_node_pool" "primary" {
  autoscaling {
    max_node_count = 3
    min_node_count = 2
  }

  cluster = google_container_azure_cluster.primary.name

  config {
    ssh_config {
      authorized_key = "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC8yaayO6lnb2v+SedxUMa2c8vtIEzCzBjM3EJJsv8Vm9zUDWR7dXWKoNGARUb2mNGXASvI6mFIDXTIlkQ0poDEPpMaXR0g2cb5xT8jAAJq7fqXL3+0rcJhY/uigQ+MrT6s+ub0BFVbsmGHNrMQttXX9gtmwkeAEvj3mra9e5pkNf90qlKnZz6U0SVArxVsLx07vHPHDIYrl0OPG4zUREF52igbBPiNrHJFDQJT/4YlDMJmo/QT/A1D6n9ocemvZSzhRx15/Arjowhr+VVKSbaxzPtEfY0oIg2SrqJnnr/l3Du5qIefwh5VmCZe4xopPUaDDoOIEFriZ88sB+3zz8ib8sk8zJJQCgeP78tQvXCgS+4e5W3TUg9mxjB6KjXTyHIVhDZqhqde0OI3Fy1UuVzRUwnBaLjBnAwP5EoFQGRmDYk/rEYe7HTmovLeEBUDQocBQKT4Ripm/xJkkWY7B07K/tfo56dGUCkvyIVXKBInCh+dLK7gZapnd4UWkY0xBYcwo1geMLRq58iFTLA2j/JmpmHXp7m0l7jJii7d44uD3tTIFYThn7NlOnvhLim/YcBK07GMGIN7XwrrKZKmxXaspw6KBWVhzuw1UPxctxshYEaMLfFg/bwOw8HvMPr9VtrElpSB7oiOh91PDIPdPBgHCi7N2QgQ5l/ZDBHieSpNrQ== thomasrodgers"
    }

    root_volume {
      size_gib = 32
    }

    tags = {
      owner = "mmv2"
    }

    vm_size = "Standard_DS2_v2"
  }

  location = "us-west1"

  max_pods_constraint {
    max_pods_per_node = 110
  }

  name      = "node-pool-name"
  subnet_id = "/subscriptions/12345678-1234-1234-1234-123456789111/resourceGroups/my--dev-byo/providers/Microsoft.Network/virtualNetworks/my--dev-vnet/subnets/default"
  version   = "${data.google_container_azure_versions.versions.valid_versions[0]}"

  annotations = {
    annotation-one = "value-one"
  }

  project = "my-project-name"
}


```

## Argument Reference

The following arguments are supported:

* `autoscaling` -
  (Required)
  Required. Autoscaler configuration for this node pool.
  
* `cluster` -
  (Required)
  The azureCluster for the resource
  
* `config` -
  (Required)
  Required. The node configuration of the node pool.
  
* `location` -
  (Required)
  The location for the resource
  
* `max_pods_constraint` -
  (Required)
  Required. The constraint on the maximum number of pods that can be run simultaneously on a node in the node pool.
  
* `name` -
  (Required)
  The name of this resource.
  
* `subnet_id` -
  (Required)
  Required. The ARM ID of the subnet where the node pool VMs run. Make sure it's a subnet under the virtual network in the cluster configuration.
  
* `version` -
  (Required)
  Required. The Kubernetes version (e.g. `1.19.10-gke.1000`) running on this node pool.
  


The `autoscaling` block supports:
    
* `max_node_count` -
  (Required)
  Required. Maximum number of nodes in the node pool. Must be >= min_node_count.
    
* `min_node_count` -
  (Required)
  Required. Minimum number of nodes in the node pool. Must be >= 1 and <= max_node_count.
    
The `config` block supports:
    
* `root_volume` -
  (Optional)
  Optional. Configuration related to the root volume provisioned for each node pool machine. When unspecified, it defaults to a 32-GiB Azure Disk.
    
* `ssh_config` -
  (Required)
  Required. SSH configuration for how to access the node pool machines.
    
* `tags` -
  (Optional)
  Optional. A set of tags to apply to all underlying Azure resources for this node pool. This currently only includes Virtual Machine Scale Sets. Specify at most 50 pairs containing alphanumerics, spaces, and symbols (.+-=_:@/). Keys can be up to 127 Unicode characters. Values can be up to 255 Unicode characters.
    
* `vm_size` -
  (Optional)
  Optional. The Azure VM size name. Example: `Standard_DS2_v2`. See (/anthos/clusters/docs/azure/reference/supported-vms) for options. When unspecified, it defaults to `Standard_DS2_v2`.
    
The `ssh_config` block supports:
    
* `authorized_key` -
  (Required)
  Required. The SSH public key data for VMs managed by Anthos. This accepts the authorized_keys file format used in OpenSSH according to the sshd(8) manual page.
    
The `max_pods_constraint` block supports:
    
* `max_pods_per_node` -
  (Required)
  Required. The maximum number of pods to schedule on a single node.
    
- - -

* `annotations` -
  (Optional)
  Optional. Annotations on the node pool. This field has the same restrictions as Kubernetes annotations. The total size of all keys and values combined is limited to 256k. Keys can have 2 segments: prefix (optional) and name (required), separated by a slash (/). Prefix must be a DNS subdomain. Name must be 63 characters or less, begin and end with alphanumerics, with dashes (-), underscores (_), dots (.), and alphanumerics between.
  
* `azure_availability_zone` -
  (Optional)
  Optional. The Azure availability zone of the nodes in this nodepool. When unspecified, it defaults to `1`.
  
* `project` -
  (Optional)
  The project for the resource
  


The `root_volume` block supports:
    
* `size_gib` -
  (Optional)
  Optional. The size of the disk, in GiBs. When unspecified, a default value is provided. See the specific reference in the parent resource.
    
## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `projects/{{project}}/locations/{{location}}/azureClusters/{{cluster}}/azureNodePools/{{name}}`

* `create_time` -
  Output only. The time at which this node pool was created.
  
* `etag` -
  Allows clients to perform consistent read-modify-writes through optimistic concurrency control. May be sent on update and delete requests to ensure the client has an up-to-date value before proceeding.
  
* `reconciling` -
  Output only. If set, there are currently pending changes to the node pool.
  
* `state` -
  Output only. The current state of the node pool. Possible values: STATE_UNSPECIFIED, PROVISIONING, RUNNING, RECONCILING, STOPPING, ERROR, DEGRADED
  
* `uid` -
  Output only. A globally unique identifier for the node pool.
  
* `update_time` -
  Output only. The time at which this node pool was last updated.
  
## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 10 minutes.
- `update` - Default is 10 minutes.
- `delete` - Default is 10 minutes.

## Import

NodePool can be imported using any of these accepted formats:

```
$ terraform import google_container_azure_node_pool.default projects/{{project}}/locations/{{location}}/azureClusters/{{cluster}}/azureNodePools/{{name}}
$ terraform import google_container_azure_node_pool.default {{project}}/{{location}}/{{cluster}}/{{name}}
$ terraform import google_container_azure_node_pool.default {{location}}/{{cluster}}/{{name}}
```



