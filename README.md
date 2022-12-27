# terraform-provider-awslambda

## Note

terraform-provider-awslambda was developed as a workaround to Terraform AWS provider. Terraform provider has the capability. Please use it. This plug-in is not maintained.

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_invocation

## Build

```console
$ go build -o terraform-provider-awslambda 
```

## Installation

```console
$ cp terraform-provider-awslambda ~/.terraform.d/plugins
```

## Usage

Defining the provider. This provider only supports `region` and `profile` variables.

```terraform
provider "awslambda" {
  region   = "us-west-1"
  profile  = "default"
}
```

Example:

```terraform
resource "aws_lambda_invocation" "example" {
  function_name = "${aws_lambda_function.lambda_function_test.function_name}"

  input = <<JSON
 {
   "key1": "value1",
   "key2": "value2"
 }
 JSON
}

output "result_entry" {
  value = jsondecode(aws_lambda_invocation.example.result)["key1"]
}
```

