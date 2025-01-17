---
subcategory: "Managed Streaming for Kafka Connect"
layout: "aws"
page_title: "AWS: aws_mskconnect_connector"
description: |-
  Provides an Amazon MSK Connect Connector resource.
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_mskconnect_connector

Provides an Amazon MSK Connect Connector resource.

## Example Usage

### Basic configuration

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Token, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.mskconnect_connector import MskconnectConnector
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        MskconnectConnector(self, "example",
            capacity=MskconnectConnectorCapacity(
                autoscaling=MskconnectConnectorCapacityAutoscaling(
                    max_worker_count=2,
                    mcu_count=1,
                    min_worker_count=1,
                    scale_in_policy=MskconnectConnectorCapacityAutoscalingScaleInPolicy(
                        cpu_utilization_percentage=20
                    ),
                    scale_out_policy=MskconnectConnectorCapacityAutoscalingScaleOutPolicy(
                        cpu_utilization_percentage=80
                    )
                )
            ),
            connector_configuration={
                "connector.class": "com.github.jcustenborder.kafka.connect.simulator.SimulatorSinkConnector",
                "tasks.max": "1",
                "topics": "example"
            },
            kafka_cluster=MskconnectConnectorKafkaCluster(
                apache_kafka_cluster=MskconnectConnectorKafkaClusterApacheKafkaCluster(
                    bootstrap_servers=Token.as_string(aws_msk_cluster_example.bootstrap_brokers_tls),
                    vpc=MskconnectConnectorKafkaClusterApacheKafkaClusterVpc(
                        security_groups=[Token.as_string(aws_security_group_example.id)],
                        subnets=[example1.id, example2.id, example3.id]
                    )
                )
            ),
            kafka_cluster_client_authentication=MskconnectConnectorKafkaClusterClientAuthentication(
                authentication_type="NONE"
            ),
            kafka_cluster_encryption_in_transit=MskconnectConnectorKafkaClusterEncryptionInTransit(
                encryption_type="TLS"
            ),
            kafkaconnect_version="2.7.1",
            name="example",
            plugin=[MskconnectConnectorPlugin(
                custom_plugin=MskconnectConnectorPluginCustomPlugin(
                    arn=Token.as_string(aws_mskconnect_custom_plugin_example.arn),
                    revision=Token.as_number(aws_mskconnect_custom_plugin_example.latest_revision)
                )
            )
            ],
            service_execution_role_arn=Token.as_string(aws_iam_role_example.arn)
        )
```

## Argument Reference

This resource supports the following arguments:

* `capacity` - (Required) Information about the capacity allocated to the connector. See below.
* `connector_configuration` - (Required) A map of keys to values that represent the configuration for the connector.
* `description` - (Optional) A summary description of the connector.
* `kafka_cluster` - (Required) Specifies which Apache Kafka cluster to connect to. See below.
* `kafka_cluster_client_authentication` - (Required) Details of the client authentication used by the Apache Kafka cluster. See below.
* `kafka_cluster_encryption_in_transit` - (Required) Details of encryption in transit to the Apache Kafka cluster. See below.
* `kafkaconnect_version` - (Required) The version of Kafka Connect. It has to be compatible with both the Apache Kafka cluster's version and the plugins.
* `log_delivery` - (Optional) Details about log delivery. See below.
* `name` - (Required) The name of the connector.
* `plugin` - (Required) Specifies which plugins to use for the connector. See below.
* `service_execution_role_arn` - (Required) The Amazon Resource Name (ARN) of the IAM role used by the connector to access the Amazon Web Services resources that it needs. The types of resources depends on the logic of the connector. For example, a connector that has Amazon S3 as a destination must have permissions that allow it to write to the S3 destination bucket.
* `worker_configuration` - (Optional) Specifies which worker configuration to use with the connector. See below.

### capacity Configuration Block

* `autoscaling` - (Optional) Information about the auto scaling parameters for the connector. See below.
* `provisioned_capacity` - (Optional) Details about a fixed capacity allocated to a connector. See below.

### autoscaling Configuration Block

* `max_worker_count` - (Required) The maximum number of workers allocated to the connector.
* `mcu_count` - (Optional) The number of microcontroller units (MCUs) allocated to each connector worker. Valid values: `1`, `2`, `4`, `8`. The default value is `1`.
* `min_worker_count` - (Required) The minimum number of workers allocated to the connector.
* `scale_in_policy` - (Optional) The scale-in policy for the connector. See below.
* `scale_out_policy` - (Optional) The scale-out policy for the connector. See below.

### scale_in_policy Configuration Block

* `cpu_utilization_percentage` - (Required) Specifies the CPU utilization percentage threshold at which you want connector scale in to be triggered.

### scale_out_policy Configuration Block

* `cpu_utilization_percentage` - (Required) The CPU utilization percentage threshold at which you want connector scale out to be triggered.

### provisioned_capacity Configuration Block

* `mcu_count` - (Optional) The number of microcontroller units (MCUs) allocated to each connector worker. Valid values: `1`, `2`, `4`, `8`. The default value is `1`.
* `worker_count` - (Required) The number of workers that are allocated to the connector.

### kafka_cluster Configuration Block

* `apache_kafka_cluster` - (Required) The Apache Kafka cluster to which the connector is connected.

### apache_kafka_cluster Configuration Block

* `bootstrap_servers` - (Required) The bootstrap servers of the cluster.
* `vpc` - (Required) Details of an Amazon VPC which has network connectivity to the Apache Kafka cluster.

### vpc Configuration Block

* `security_groups` - (Required) The security groups for the connector.
* `subnets` - (Required) The subnets for the connector.

### kafka_cluster_client_authentication Configuration Block

* `authentication_type` - (Optional) The type of client authentication used to connect to the Apache Kafka cluster. Valid values: `IAM`, `NONE`. A value of `NONE` means that no client authentication is used. The default value is `NONE`.

### kafka_cluster_encryption_in_transit Configuration Block

* `encryption_type` - (Optional) The type of encryption in transit to the Apache Kafka cluster. Valid values: `PLAINTEXT`, `TLS`. The default values is `PLAINTEXT`.

### log_delivery Configuration Block

* `worker_log_delivery` - (Required) The workers can send worker logs to different destination types. This configuration specifies the details of these destinations. See below.

### worker_log_delivery Configuration Block

* `cloudwatch_logs` - (Optional) Details about delivering logs to Amazon CloudWatch Logs. See below.
* `firehose` - (Optional) Details about delivering logs to Amazon Kinesis Data Firehose. See below.
* `s3` - (Optional) Details about delivering logs to Amazon S3. See below.

### cloudwatch_logs Configuration Block

* `enabled` - (Optional) Whether log delivery to Amazon CloudWatch Logs is enabled.
* `log_group` - (Required) The name of the CloudWatch log group that is the destination for log delivery.

### firehose Configuration Block

* `delivery_stream` - (Optional) The name of the Kinesis Data Firehose delivery stream that is the destination for log delivery.
* `enabled` - (Required) Specifies whether connector logs get delivered to Amazon Kinesis Data Firehose.

### s3 Configuration Block

* `bucket` - (Optional) The name of the S3 bucket that is the destination for log delivery.
* `enabled` - (Required) Specifies whether connector logs get sent to the specified Amazon S3 destination.
* `prefix` - (Optional) The S3 prefix that is the destination for log delivery.

### plugin Configuration Block

* `custom_plugin` - (Required) Details about a custom plugin. See below.

### custom_plugin Configuration Block

* `arn` - (Required) The Amazon Resource Name (ARN) of the custom plugin.
* `revision` - (Required) The revision of the custom plugin.

### worker_configuration Configuration Block

* `arn` - (Required) The Amazon Resource Name (ARN) of the worker configuration.
* `revision` - (Required) The revision of the worker configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the connector.
* `version` - The current version of the connector.

## Timeouts

[Configuration options](https://developer.hashicorp.com/terraform/language/resources/syntax#operation-timeouts):

* `create` - (Default `20m`)
* `update` - (Default `20m`)
* `delete` - (Default `10m`)

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import MSK Connect Connector using the connector's `arn`. For example:

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformStack
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
```

Using `terraform import`, import MSK Connect Connector using the connector's `arn`. For example:

```console
% terraform import aws_mskconnect_connector.example 'arn:aws:kafkaconnect:eu-central-1:123456789012:connector/example/264edee4-17a3-412e-bd76-6681cfc93805-3'
```

<!-- cache-key: cdktf-0.20.0 input-40619f08de26cd7fcad3cf70d7685484652ad1f0806e16438690dce5d953aa3a -->