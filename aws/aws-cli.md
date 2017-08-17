
## Resources

https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html

https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html

## Setting up a Role

edit ~/.aws/config

```
[profile admin]
role_arn = arn:aws:iam::1234567890:role/admin
source_profile = default
```

note: source profile must have permission to call sts:assume-role

(IAM)[https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html] needs to be setup correctly 

## Credential configuration

aws configure --profile <profile name>

The AWS CLI looks for credentials and configuration settings in the following order:

    Command Line Options – region, output format and profile can be specified as command options to override default settings.

    Environment Variables – AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, etc.

    The AWS credentials file – located at ~/.aws/credentials on Linux, macOS, or Unix, or at C:\Users\USERNAME \.aws\credentials on Windows. This file can contain multiple named profiles in addition to a default profile.

    The CLI configuration file – typically located at ~/.aws/config on Linux, macOS, or Unix, or at C:\Users\USERNAME \.aws\config on Windows. This file can contain a default profile, named profiles, and CLI specific configuration parameters for each.

    Instance profile credentials – these credentials can be used on EC2 instances with an assigned instance role, and are delivered through the Amazon EC2 metadata service.


## EC2

### Launch workflow 

#### Startup instance 

aws ec2 run-instances --image-id ami-6e1a0117 --security-group-ids sg-b018ced5 --count 1 --instance-type t2.micro --key-name devenv-key --query 'Instances[0].InstanceId'

will return instance id which can be used for further commands

#### Add block devices to instances

aws ec2 run-instances ... --block-device-mappings "[{\"DeviceName\":\"/dev/sdf\",\"Ebs\":{\"VolumeSize\":20,\"DeleteOnTermination\":false}}]"

#### Get public ip

aws ec2 describe-instances --instance-ids "......" --query 'Reservations[0].Instances[0].PublicIpAddress'

will return public ip addr

ssh -i keyfile.pem user@ip-addr

### Create key pair

aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem

### Create a security group

aws ec2 create-security-group --group-name <name> --description "<desc>"

### Listing instances

aws ec2 describe-instances ....

### Terminate instance

aws ec2 terminate-instances

