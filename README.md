# aws-cloudformation-helper

A Bash script to help run AWS CloudFormation CLI. This script provides the feature to run cloudformation commands and view a stack event history. You no longer have to switch between Terminal and Browser when running AWS CloudFormation.

Example of creating a stack.

```shell
$ my-cfn create-stack \
  --template examples/ec2.yaml \
  --parameter examples/ec2.json \
  --region us-east-1
```

Output. Stack events are displayed every 5 seconds.

```shell
{
    "StackId": "arn:aws:cloudformation:us-east-1:123456789012:stack/ec2/48d58b40-9a8e-11eb-ac25-0e211a4ad657"
}
"Timestamp"  "Logical Id"  "Status"  "Status reason"
"2021-05-19T06:22:26.346"  "ec2"  "CREATE_IN_PROGRESS"  "User Initiated"
"2021-05-19T06:22:31.609"  "EC2Instance"  "CREATE_IN_PROGRESS"
"2021-05-19T06:22:33.863"  "EC2Instance"  "CREATE_IN_PROGRESS"  "Resource creation Initiated"
"2021-05-19T06:22:49.731"  "EC2Instance"  "CREATE_COMPLETE"
"2021-05-19T06:22:51.016"  "ec2"  "CREATE_COMPLETE"
```

## Getting Started

### Prerequisites

- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- [jq](https://stedolan.github.io/jq/download/)

### Installation

1. Download the script to /usr/local/bin
   ```shell
   curl https://raw.githubusercontent.com/karakaram/aws-cloudformation-helper/main/my-cfn -o /usr/local/bin/my-cfn
   ```
1. Add execute permission
   ```shell
   chmod +x /usr/local/bin/my-cfn
   ```

## Usage

To create a CloudFormation stack.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  --region us-east-1
```

To create a CloudFormation stack with a parameter.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  -p examples/ec2.json \
  --region us-east-1
```

To update a stack.

```shell
my-cfn update-stack \
  -t examples/ec2.yaml \
  -p examples/ec2.json \
  --region us-east-1
```

To create change sets.

```shell
my-cfn create-change-set \
  -t examples/ec2.yaml \
  -p examples/ec2.json \
  --region us-east-1
```

To execute change sets.

```shell
my-cfn execute-change-set \
  -t examples/ec2.yaml \
  --region us-east-1
```

To delete a stack.

```shell
my-cfn delete-stack \
  -t examples/ec2.yaml \
  --region us-east-1
```

To omit the parameter if both the template and the parameter have the same name. In the following example, examples/ec2.json is automatically used as a parameter.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  --region us-east-1
```

Use `-f(--force)` option to delete a stack before creating it.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  -f \
  --region us-east-1
```

Use `-s(--stack-name)` option to specify a stack name.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  -s ec2-production \
  -p ec2-production.json \
  --region us-east-1
```

Use `-r(--role-arn)` option to specify a IAM Role ARN.

```shell
my-cfn create-stack \
  -t examples/ec2.yaml \
  -r arn:aws:iam::123456789012:role/my-role
  --region us-east-1
```

For more details, refer to `-h(--help)`.

```shell
my-cfn -h
```

## License

Distributed under the MIT License.
