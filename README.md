# Temporal Cloud Terraform Provider

## Requirements

- [Terraform](https://developer.hashicorp.com/terraform/downloads) >= 1.0
- [Go](https://golang.org/doc/install) >= 1.19

## Building The Provider

1. Clone the repository
1. Enter the repository directory
1. Build the provider using the Go `install` command:

```shell
go install
```

## Adding Dependencies

This provider uses [Go modules](https://github.com/golang/go/wiki/Modules).
Please see the Go documentation for the most up to date information about using Go modules.

To add a new dependency `github.com/author/dependency` to your Terraform provider:

```shell
go get github.com/author/dependency
go mod tidy
```

Then commit the changes to `go.mod` and `go.sum`.

## Using the provider

Fill this in for each provider

## Developing the Provider

If you wish to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine (see [Requirements](#requirements) above).

To compile the provider, run `go install`. This will build the provider and put the provider binary in the `$GOPATH/bin` directory.

To generate or update documentation, run `go generate`.

In order to run the full suite of Acceptance tests, run `make testacc`.

*Note:* Acceptance tests create real resources, and often cost money to run.

```shell
make testacc
```

## Testing with Terraform

In order to test your code you need an api key for temporal cloud. Docs on how to generate this is here:
https://github.com/temporalio/tcld/tree/release/apikeys#api-key-management-preview

Then you need to make the provider binary available to `terraform` itself.

```
go build -o terraform-provider-temporalcloud
mkdir -p ~/.terraform.d/plugins/temporal.io/provider-temporalcloud/temporalcloud/1.0.0/darwin_arm64/
mv terraform-provider-temporalcloud ~/.terraform.d/plugins/temporal.io/provider-temporalcloud/temporalcloud/1.0.0/darwin_arm64
```

Finally, your terraform configuration files need to know about this provider.

```
provider "temporalcloud" {
  api_key = "<API_KEY>"

}

terraform {
  required_providers {
    temporalcloud = {
      version = "~> 1.0.0"
      source  = "temporal.io/provider-temporalcloud/temporalcloud"
    }
  }
}
```

Now you can start testing your provider with `terraform`!

