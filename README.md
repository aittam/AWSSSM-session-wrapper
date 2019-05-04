# AWSSSM-session-wrapper
AWS SSM Session wrapper. A simple wrapper script to simplify the starting of SSM sessions.
It lists all your running EC2 instances in your default region and let you select which instance to connect to.

## Requirements

To use this tool you need to install the following tools:

* Python 3
* [AWS cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
* [Session Manager Plugin](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)

## How to use it

This wrapper use the standard authentication chain used in boto3 hence you can take advantage of your profiles defined in *~/.aws/credentials* and 
*~/.aws/config* as explained [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html).

You can optionally provide a profile as a command line argument, use the default profile or the AWS_PROFILE environment variable.

### Examples

#### Example 1

```bash
python3 ./ssmSessionWrapper.py --profile my-profile-dev
List of running instances:
[0]: linux-test1 - i-06bc4b6ce3c3c18e5
[1]: linux-test2 - i-01dc627cbfe388d77
Type the number of the instance you want to connect to: 1
Connecting to i-01dc627cbfe388d77

Starting session with SessionId: botocore-session-1556723767-06ea4aec0cb66907e
sh-4.2$
```

#### Example 2

```bash
export AWS_PROFILE=my-profile-stg
python3 ./ssmSessionWrapper.py --region eu-west-1
Enter MFA code for arn:aws:iam::123456789:mfa/name.surname:
List of running instances:
[0]: linux-test1 - i-02bz4b6de4c3c18f3
[1]: linux-test2 - i-03dc727cbfe388dd4
[3]: linux-test3 - i-07gc763cffe368df5
Type the number of the instance you want to connect to: 0
```

### Command line arguments

```bash
python3 ssmSessionWrapper.py -h
usage: ssmSessionWrapper.py [-h] [--profile PROFILE]

optional arguments:
  -h, --help         show this help message and exit
  --profile PROFILE  AWS profile
  --region REGION    AWS region
```


