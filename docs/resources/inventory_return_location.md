---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "commercelayer_inventory_return_location Resource - terraform-provider-commercelayer"
subcategory: ""
description: |-
  Inventory return locations build a hierarchy of stock locations within an inventory model, determining the available options for the returns. In the case a SKU is available in more stock locations, it gets returned to those with the highest priority.
---

# commercelayer_inventory_return_location (Resource)

Inventory return locations build a hierarchy of stock locations within an inventory model, determining the available options for the returns. In the case a SKU is available in more stock locations, it gets returned to those with the highest priority.

## Example Usage

```terraform
resource "commercelayer_inventory_model" "incentro_inventory_model" {
  attributes {
    name                   = "Incentro Inventory Model"
    stock_locations_cutoff = 2
    strategy               = "split_shipments"
  }
}

resource "commercelayer_address" "incentro_address" {
  attributes {
    business     = true
    company      = "Incentro"
    line_1       = "Van Nelleweg 1"
    zip_code     = "3044 BC"
    country_code = "NL"
    city         = "Rotterdam"
    phone        = "+31(0)10 20 20 544"
    state_code   = "ZH"
  }
}

resource "commercelayer_stock_location" "incentro_stock_location" {
  attributes {
    name         = "Incentro Warehouse Location"
    label_format = "PNG"
    suppress_etd = true
  }

  relationships {
    address_id = commercelayer_address.incentro_address.id
  }
}

resource "commercelayer_inventory_return_location" "incentro_return_location" {
  attributes {
    priority = 1
  }

  relationships {
    inventory_model_id = commercelayer_inventory_model.incentro_inventory_model.id
    stock_location_id  = commercelayer_stock_location.incentro_stock_location.id
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `attributes` (Block List, Min: 1, Max: 1) Resource attributes (see [below for nested schema](#nestedblock--attributes))
- `relationships` (Block List, Min: 1, Max: 1) Resource relationships (see [below for nested schema](#nestedblock--relationships))

### Read-Only

- `id` (String) The inventory return location unique identifier
- `type` (String) The resource type

<a id="nestedblock--attributes"></a>
### Nested Schema for `attributes`

Required:

- `priority` (Number) The inventory model's internal name.

Optional:

- `metadata` (Map of String) Set of key-value pairs that you can attach to the resource. This can be useful for storing additional information about the resource in a structured format
- `reference` (String) A string that you can use to add any external identifier to the resource. This can be useful for integrating the resource to an external system, like an ERP, a InventoryReturnLocationing tool, a CRM, or whatever.
- `reference_origin` (String) Any identifier of the third party system that defines the reference code


<a id="nestedblock--relationships"></a>
### Nested Schema for `relationships`

Required:

- `inventory_model_id` (String) The associated inventory model id.
- `stock_location_id` (String) The associated stock location id.

