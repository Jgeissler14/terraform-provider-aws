---
subcategory: "GuardDuty"
layout: "aws"
page_title: "AWS: aws_guardduty_organization_configuration_feature"
description: |-
  Provides a resource to manage an Amazon GuardDuty organization configuration feature
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_guardduty_organization_configuration_feature

Provides a resource to manage a single Amazon GuardDuty [organization configuration feature](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty-features-activation-model.html#guardduty-features).

~> **NOTE:** Deleting this resource does not disable the organization configuration feature, the resource in simply removed from state instead.

## Example Usage

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { GuarddutyDetector } from "./.gen/providers/aws/guardduty-detector";
import { GuarddutyOrganizationConfigurationFeature } from "./.gen/providers/aws/guardduty-organization-configuration-feature";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    const example = new GuarddutyDetector(this, "example", {
      enable: true,
    });
    new GuarddutyOrganizationConfigurationFeature(
      this,
      "eks_runtime_monitoring",
      {
        additionalConfiguration: [
          {
            autoEnable: "NEW",
            name: "EKS_ADDON_MANAGEMENT",
          },
        ],
        autoEnable: "ALL",
        detectorId: example.id,
        name: "EKS_RUNTIME_MONITORING",
      }
    );
  }
}

```

## Argument Reference

This resource supports the following arguments:

* `autoEnable` - (Required) The status of the feature that is configured for the member accounts within the organization. Valid values: `NEW`, `ALL`, `NONE`.
* `detectorId` - (Required) The ID of the detector that configures the delegated administrator.
* `name` - (Required) The name of the feature that will be configured for the organization. Valid values: `S3_DATA_EVENTS`, `EKS_AUDIT_LOGS`, `EBS_MALWARE_PROTECTION`, `RDS_LOGIN_EVENTS`, `EKS_RUNTIME_MONITORING`, `LAMBDA_NETWORK_LOGS`.
* `additionalConfiguration` - (Optional) The additional information that will be configured for the organization See [below](#additional-configuration).

### Additional Configuration

The `additionalConfiguration` block supports the following:

* `autoEnable` - (Required) The status of the additional configuration that will be configured for the organization. Valid values: `NEW`, `ALL`, `NONE`.
* `name` - (Required) The name of the additional configuration that will be configured for the organization. Valid values: `EKS_ADDON_MANAGEMENT`.

## Attribute Reference

This resource exports no additional attributes.

<!-- cache-key: cdktf-0.20.0 input-af534c2b9dc87ad328aeada98eac41421489586c67758449e011a8a7d6b7e223 -->