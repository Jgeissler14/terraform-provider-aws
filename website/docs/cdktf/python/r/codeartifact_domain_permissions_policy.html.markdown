---
subcategory: "CodeArtifact"
layout: "aws"
page_title: "AWS: aws_codeartifact_domain_permissions_policy"
description: |-
  Provides a CodeArtifact Domain Permissions Policy resource.
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_codeartifact_domain_permissions_policy

Provides a CodeArtifact Domains Permissions Policy Resource.

## Example Usage

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Token, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.codeartifact_domain import CodeartifactDomain
from imports.aws.codeartifact_domain_permissions_policy import CodeartifactDomainPermissionsPolicy
from imports.aws.data_aws_iam_policy_document import DataAwsIamPolicyDocument
from imports.aws.kms_key import KmsKey
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        example = KmsKey(self, "example",
            description="domain key"
        )
        aws_codeartifact_domain_example = CodeartifactDomain(self, "example_1",
            domain="example",
            encryption_key=example.arn
        )
        # This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.
        aws_codeartifact_domain_example.override_logical_id("example")
        test = DataAwsIamPolicyDocument(self, "test",
            statement=[DataAwsIamPolicyDocumentStatement(
                actions=["codeartifact:CreateRepository"],
                effect="Allow",
                principals=[DataAwsIamPolicyDocumentStatementPrincipals(
                    identifiers=["*"],
                    type="*"
                )
                ],
                resources=[Token.as_string(aws_codeartifact_domain_example.arn)]
            )
            ]
        )
        aws_codeartifact_domain_permissions_policy_test =
        CodeartifactDomainPermissionsPolicy(self, "test_3",
            domain=Token.as_string(aws_codeartifact_domain_example.domain),
            policy_document=Token.as_string(test.json)
        )
        # This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.
        aws_codeartifact_domain_permissions_policy_test.override_logical_id("test")
```

## Argument Reference

This resource supports the following arguments:

* `domain` - (Required) The name of the domain on which to set the resource policy.
* `policy_document` - (Required) A JSON policy string to be set as the access control resource policy on the provided domain.
* `domain_owner` - (Optional) The account number of the AWS account that owns the domain.
* `policy_revision` - (Optional) The current revision of the resource policy to be set. This revision is used for optimistic locking, which prevents others from overwriting your changes to the domain's resource policy.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Name of Domain.
* `resource_arn` - The ARN of the resource associated with the resource policy.

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import CodeArtifact Domain Permissions Policies using the CodeArtifact Domain ARN. For example:

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformStack
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
```

Using `terraform import`, import CodeArtifact Domain Permissions Policies using the CodeArtifact Domain ARN. For example:

```console
% terraform import aws_codeartifact_domain_permissions_policy.example arn:aws:codeartifact:us-west-2:012345678912:domain/tf-acc-test-1928056699409417367
```

<!-- cache-key: cdktf-0.20.0 input-ad7db656ffa6152a6f3b17e85bd919f6f92ab7d824fe3b18d3dfdd0e0c9f5daf -->