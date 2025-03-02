<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS kafka
</h1>

<p align="center" style="font-size: 1.2rem;"> 
    Terraform module to create kafka resource on AWS.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v1.1.7-green" alt="Terraform">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-APACHE-blue.svg" alt="Licence">
</a>
<a href="https://github.com/clouddrove/terraform-aws-kafka/actions/workflows/tfsec.yml">
  <img src="https://github.com/clouddrove/terraform-aws-kafka/actions/workflows/tfsec.yml/badge.svg" alt="tfsec">
</a>
<a href="https://github.com/clouddrove/terraform-aws-kafka/actions/workflows/terraform.yml">
  <img src="https://github.com/clouddrove/terraform-aws-kafka/actions/workflows/terraform.yml/badge.svg" alt="static-checks">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-aws-kafka'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+AWS+kafka&url=https://github.com/clouddrove/terraform-aws-kafka'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+AWS+kafka&url=https://github.com/clouddrove/terraform-aws-kafka'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards strategies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure. 

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies: 

- [Terraform 1.x.x](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)
- [github.com/stretchr/testify/assert](https://github.com/stretchr/testify)
- [github.com/gruntwork-io/terratest/modules/terraform](https://github.com/gruntwork-io/terratest)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-kafka/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
```hcl
  module "kafka" {
     source      = "clouddrove/kafka/aws"

     name        = "kafka"
     environment = "test"
     label_order = ["name", "environment"]

     kafka_version          = "2.7.1"
     kafka_broker_number    = 3

     broker_node_client_subnets  = module.subnets.private_subnet_id
     broker_node_ebs_volume_size = 20
     broker_node_instance_type   = "kafka.t3.small"
     broker_node_security_groups = [module.ssh.security_group_ids]

     configuration_server_properties = {
     "auto.create.topics.enable" = true
     "delete.topic.enable"       = true
    }
  }
```






## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| broker\_node\_client\_subnets | A list of subnets to connect to in client VPC ([documentation](https://docs.aws.amazon.com/msk/1.0/apireference/clusters.html#clusters-prop-brokernodegroupinfo-clientsubnets)) | `list(string)` | `[]` | no |
| broker\_node\_ebs\_volume\_size | The size in GiB of the EBS volume for the data drive on each broker node | `number` | `null` | no |
| broker\_node\_instance\_type | Specify the instance type to use for the kafka brokers. e.g. kafka.m5.large. ([Pricing info](https://aws.amazon.com/msk/pricing/)) | `string` | `null` | no |
| broker\_node\_security\_groups | A list of the security groups to associate with the elastic network interfaces to control who can communicate with the cluster | `list(string)` | `[]` | no |
| client\_authentication\_sasl\_iam | Enables IAM client authentication | `bool` | `false` | no |
| client\_authentication\_sasl\_scram | Enables SCRAM client authentication via AWS Secrets Manager | `bool` | `false` | no |
| client\_authentication\_tls\_certificate\_authority\_arns | List of ACM Certificate Authority Amazon Resource Names (ARNs) | `list(string)` | `[]` | no |
| cloudwatch\_log\_group\_kms\_key\_id | The ARN of the KMS Key to use when encrypting log data | `string` | `null` | no |
| cloudwatch\_log\_group\_name | Name of the Cloudwatch Log Group to deliver logs to | `string` | `null` | no |
| cloudwatch\_log\_group\_retention\_in\_days | Specifies the number of days you want to retain log events in the log group | `number` | `0` | no |
| cloudwatch\_logs\_enabled | Indicates whether you want to enable or disable streaming broker logs to Cloudwatch Logs | `bool` | `false` | no |
| configuration\_description | Description of the configuration | `string` | `"Complete example configuration"` | no |
| configuration\_server\_properties | Contents of the server.properties file. Supported properties are documented in the [MSK Developer Guide](https://docs.aws.amazon.com/msk/latest/developerguide/msk-configuration-properties.html) | `map(string)` | `{}` | no |
| create\_cloudwatch\_log\_group | Determines whether to create a CloudWatch log group | `bool` | `true` | no |
| create\_schema\_registry | Determines whether to create a Glue schema registry for managing Avro schemas for the cluster | `bool` | `true` | no |
| create\_scram\_secret\_association | Determines whether to create SASL/SCRAM secret association | `bool` | `false` | no |
| encryption\_at\_rest\_kms\_key\_arn | You may specify a KMS key short ID or ARN (it will always output an ARN) to use for encrypting your data at rest. If no key is specified, an AWS managed KMS ('aws/msk' managed service) key will be used for encrypting the data at rest | `string` | `null` | no |
| encryption\_in\_transit\_client\_broker | Encryption setting for data in transit between clients and brokers. Valid values: `TLS`, `TLS_PLAINTEXT`, and `PLAINTEXT`. Default value is `TLS` | `string` | `null` | no |
| encryption\_in\_transit\_in\_cluster | Whether data communication among broker nodes is encrypted. Default value: `true` | `bool` | `null` | no |
| enhanced\_monitoring | Specify the desired enhanced MSK CloudWatch monitoring level. See [Monitoring Amazon MSK with Amazon CloudWatch](https://docs.aws.amazon.com/msk/latest/developerguide/monitoring.html) | `string` | `"PER_TOPIC_PER_PARTITION"` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| firehose\_delivery\_stream | Name of the Kinesis Data Firehose delivery stream to deliver logs to | `string` | `null` | no |
| firehose\_logs\_enabled | Indicates whether you want to enable or disable streaming broker logs to Kinesis Data Firehose | `bool` | `false` | no |
| jmx\_exporter\_enabled | Indicates whether you want to enable or disable the JMX Exporter | `bool` | `false` | no |
| kafka\_broker\_number | Kafka brokers per zone | `number` | `1` | no |
| kafka\_version | Version of Kafka brokers | `string` | `"2.2.1"` | no |
| label\_order | Label order, e.g. `name`,`application`. | `list(any)` | `[]` | no |
| managedby | ManagedBy, eg 'CloudDrove' | `string` | `"hello@clouddrove.com"` | no |
| msk\_cluster\_enabled | Flag to control the msk-cluster creation. | `bool` | `true` | no |
| name | Name  (e.g. `app` or `cluster`). | `string` | `""` | no |
| node\_exporter\_enabled | Indicates whether you want to enable or disable the Node Exporter | `bool` | `false` | no |
| s3\_logs\_bucket | Name of the S3 bucket to deliver logs to | `string` | `null` | no |
| s3\_logs\_enabled | Indicates whether you want to enable or disable streaming broker logs to S3 | `bool` | `false` | no |
| s3\_logs\_prefix | Prefix to append to the folder name | `string` | `null` | no |
| scaling\_max\_capacity | Max storage capacity for Kafka broker autoscaling | `number` | `250` | no |
| scaling\_role\_arn | The ARN of the IAM role that allows Application AutoScaling to modify your scalable target on your behalf. This defaults to an IAM Service-Linked Role | `string` | `null` | no |
| scaling\_target\_value | The Kafka broker storage utilization at which scaling is initiated | `number` | `70` | no |
| schema\_registries | A map of schema registries to be created | `map(any)` | `{}` | no |
| schemas | A map schemas to be created within the schema registry | `map(any)` | `{}` | no |
| scram\_secret\_association\_secret\_arn\_list | List of AWS Secrets Manager secret ARNs to associate with SCRAM | `list(string)` | <pre>[<br>  ""<br>]</pre> | no |
| timeouts | Create, update, and delete timeout configurations for the cluster | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | Amazon Resource Name (ARN) of the MSK cluster |
| configuration\_arn | Amazon Resource Name (ARN) of the configuration |
| configuration\_latest\_revision | Latest revision of the configuration |
| current\_version | Current version of the MSK Cluster used for updates, e.g. `K13V1IB3VIYZZH` |
| scram\_secret\_association\_id | Amazon Resource Name (ARN) of the MSK cluster |




## Testing
In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system. 

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback 
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-aws-kafka/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-aws-kafka)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=
