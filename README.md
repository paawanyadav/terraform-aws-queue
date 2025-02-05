# terraform-aws-queue

## Usage

```
module "message_queue" {
  source              = "git::https://github.com/tothenew/terraform-aws-queue.git"
  ec2_subnet_id = "subnet-99999999999"
  key_name = "tothenew"
  vpc_id  = "vpc-xxxxxxxx"
  vpc_cidr_block = "0.0.0.0/0"
  instance_type = "t3.medium"
  disable_api_termination = true
  disable_api_stop        = true
  subnet_ids          = ["subnet-99999999999","subnet-99999999999"]
  apply_immediately = false
  host_instance_type = "mq.t3.micro"
  deployment_mode    = "ACTIVE_STANDBY_MULTI_AZ"
  storage_type = "efs"
  console_access = true
  publicly_accessible = true
  engine_type = "ActiveMQ"
  engine_version = "5.15.14"
  auto_minor_version_upgrade = false
  activemq_username   = "username"
  activemq_password   = "password"
  audit_logs = false
  general_logs = false
  root_volume_size = 50
  region  = "us-east-1"
  vpc_cidr_block = "0.0.0.0/0"  //This is for SG egress rules
  worker  = 1
  master  = 1
  
  create_aws_activemq     = true
  create_aws_ec2_rabbitmq = false

  common_tags         = {
    "Project"     = "ToTheNew",
    "Environment" = "dev"
  }
  project_name_prefix = "TTN"
}
}
```

## Requirements

Before this module can be used on a project, you must ensure that the following pre-requisites are fulfilled:

1. Terraform is [installed](#software-dependencies) on the machine where Terraform is executed.
2. Make sure you had access to launch the resources in aws.

### Software Dependencies
## Terraform
- [Terraform](https://www.terraform.io/downloads.html) >= 1.3.0

## Providers

| Name | Version |
|------|---------|
| aws | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| create_aws_activemq | If you want to create the AWS active-mq enable this check | `bool` | `bool` | no |
| create_aws_ec2_rabbitmq | If you want to create the AWS EC2 instance rabbit-mq enable this check | `bool` | `true` | no |
| project_name_prefix | A string value to describe prefix of all the resources | `string` | `n/a` | yes |
| engine_type | Type of broker engine, `ActiveMQ` or `RabbitMQ` | `sting` | `ActiveMQ` | yes |
| engine_version | The version of the broker engine | `string` | 5.15.14 | yes |
| create\_aws\_ec2\_elasticsearch | If you want to create the AWS EC2 instance elasticsearch enable this check | `bool` | `true` | no |
| storage_type | Type of storage | `string` | `ebs` | no |
| auto_minor_version_upgrade | Enables automatic upgrades to new minor versions for brokers, as Apache releases the versions. | `bool` | `false` | no |
| apply_immediately | Specifies whether any cluster modifications are applied immediately, or during the next maintenance window | `bool` | `false` | no |
| host_instance_type | The broker's instance type. e.g. mq.t2.micro or mq.m4.large | `string` | `mq.m5.large` | no |
| security\_group\_ids | A string value for Security Group ID | `list(string)` | `n/a` | yes |
| deployment_mode | The deployment mode of the broker. Supported: SINGLE_INSTANCE and ACTIVE_STANDBY_MULTI_AZ | `string` | `SINGLE_INSTANCE` | no |
| subnet\_ids | Subnet Ids where server will be launched | `list(string)` | `n/a` | yes |
| publicly_accessible| Whether to enable connections from applications outside of the VPC that hosts the broker's subnets | `bool` | `true` | no |
| activemq_username | Admin username | `string` | `n/a` | yes |
| activemq_password | Admin password | `string` | `n/a` | yes |
| console_access | Whether to enable console access | `bool` | `true` | no |
| environment | environment where services need to be run | `string` | `dev` | no |
| common_tags | A map to add common tags to all the resources	 | `map(string)` | `n/a` | yes |
| master\_user\_password | Password of the security option enabled | `string` | `n/a` | no |
| project | A string value to describe project of all the resources | `string` | `test` | yes |
| ec2_subnet_id | Subnet Ids where server will be launched | `string` | `n/a` | yes |
| key_name | Key name of the Key Pair to use for the instance | `string` | `n/a` | yes |
| subnet\_ids | Subnet Ids where server will be launched | `list(string)` | n/a | yes |
| iam_instance_profile | IAM Instance Profile to launch the instance with. Specified as the name of the Instance Profile | `sting` | `n/a` | yes |
| instance_type | EC2 Instance Type | `string` | `t3a.medium` | yes |
| disable\_api\_termination | Disable API termination means disable instance termination | `bool` | `true` | no |
| disable_api_stop | If true, enables EC2 Instance Stop Protection | `bool` | `false` | no |
| ebs_optimized | If true, the launched EC2 instance will be EBS-optimized | `bool` | `true` | no |
| source_dest_check | Source destination Check. Used for NAT or VPNs | `bool` | `true` | no |
| delete_on_termination | Whether EBS volume will be deleted when instance gets deleted | `bool` | `true` | no |
| kms_key_id | KMS key ID for creating AWS resources | `string` | `n/a` | yes |
| encrypted | Whether EBS volume will be encrypted | `bool` | `true` | yes |
| root_volume_size | Root volume size of the EC2 instance | `number` | `50` | yes |
| volume_type | Volume type for EC2 instance default latest type | `string` | `gp3` | no |
| audit_logs | KMS key ID for creating AWS resources | `bool` | `false` | no |
| general_logs | KMS key ID for creating AWS resources | `bool` | `false` | no |
| vpc_cidr_block | CIDR range of sg | `string` | `0.0.0.0/0` | yes |
| vpc_id | vpc id for rabbit sg | `string` | `n/a` | yes |
| rabbit_sg_name | SG name for rabbit | `string` | `rabbit-sg` | no |
| region | Region where resources will deploy | `string` | `us-east-1` | yes |
| environment_name | Environment name | `string` | `dev` | yes |
| root_volume_size | Root volume size of the EC2 instance | `number` | `50` | no |



## Outputs

| Name | Description |
|------|-------------|
| activemq_id | `n/a` |
| activemq_url | `n/a` |
| activemq_arn | `n/a` |
| ec2_rabbitmq_private_ip | `n/a` |


