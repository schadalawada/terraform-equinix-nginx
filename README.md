# Equinix Network Edge NGINX device creation Terraform module

[![Experimental](https://img.shields.io/badge/Stability-Experimental-red.svg)](https://github.com/equinix-labs/standards#about-uniform-standards)
[![terraform](https://github.com/equinix-labs/terraform-equinix-template/actions/workflows/integration.yaml/badge.svg)](https://github.com/equinix-labs/terraform-equinix-template/actions/workflows/integration.yaml)

`terraform-equinix-network-edge-nginx` is a Terraform module that
utilizes[Terraform provider for Equinix][equinix_terraform_provider_url] to
create Network Edge NGINX device.

This module creates a NGINX single device, HA pair and Cluster based on configuration.

## Usage

This project is experimental and supported by the user
community. Equinix does not provide support for this project.

Install Terraform using the official guides at <https://learn.hashicorp.com/tutorials/terraform/install-cli>.

This project may be forked, cloned, or downloaded and
modified as needed as the base in your integrations and deployments.

This project may also be used as a [Terraform module](https://learn.hashicorp.com/collections/terraform/modules).

To use this module in a new project, create a file such as:

```hcl
# main.tf
provider "equinix" {
  client_id     = var.equinix_client_id
  client_secret = var.equinix_client_secret
}

module "nginx-single" {
  source                 = "equinix-labs/network-edge-device-nginx/equinix"
  name                   = "terraform-test-NGINX"
  hostname               = "terraform-nginx"
  metro_code             = "AT"
  account_number         = "123456"
  platform               = "small"
  software_package       = "STD"
  term_length            = 1
  notifications          = ["test@test.com"]
  additional_bandwidth   = 50
  mgmt_acl_template_uuid = equinix_network_acl_template.nginx-pri.id
  ssh_key = {
    userName = "johndoe"
    keyName  = equinix_network_ssh_key.johndoe.name
  }
}

```

Run `terraform init -upgrade` and `terraform apply`.

## Variables

See <https://registry.terraform.io/modules/equinix-labs/network-edge-device-nginx/equinix/latest?tab=inputs>
for a description of all variables.

## Outputs

See <https://registry.terraform.io/modules/equinix-labs/network-edge-device-nginx/equinix/latest?tab=outputs>
for a description of all outputs.

## Resources

| Name | Type |
|------|------|
| [equinix_network_device.this][equinix_network_device_data_source_url] | resource |
| [equinix_network_device_type.this][equinix_network_device_type_data_source_url] | data source |
| [equinix_network_device_platform.this][equinix_network_device_platform_data_source_url] | data source |
| [equinix_network_device_software.this][equinix_network_device_software_data_source_url] | data source |

## Examples

<!-- TEMPLATE: The following block has been generated by terraform-docs util: https://github.com/terraform-docs/terraform-docs -->
<!-- BEGIN_TF_DOCS -->

- [Network Edge NGINX single device](https://registry.terraform.io/modules/equinix-labs/network-edge-device-nginx/equinix/latest/examples/nginx-single/)
- [Network Edge NGINX HA pair device](https://registry.terraform.io/modules/equinix-labs/network-edge-device-nginx/equinix/latest/examples/nginx-ha/)
- [Network Edge cluster device](https://registry.terraform.io/modules/equinix-labs/network-edge-device-nginx/equinix/latest/examples/nginx-cluster/)

<!-- END_TF_DOCS -->

[equinix_network_device_data_source_url]: (https://registry.terraform.io/providersequinix/equinix/latest/docs/resources/equinix_network_device)
[equinix_network_device_type_data_source_url]: (https://registry.terraform.io/providers/equinix/equinix/latest/docs/data-sources/equinix_network_device_type)
[equinix_network_device_platform_data_source_url]: (https://registry.terraform.io/providers/equinix/equinix/latest/docs/data-sources/equinix_network_device_platform)
[equinix_network_device_software_data_source_url]: (https://registry.terraform.io/providers/equinix/equinix/latest/docs/data-sources/equinix_network_device_software)
[equinix_terraform_provider_url]: (https://registry.terraform.io/providers/equinix/equinix/latest)
